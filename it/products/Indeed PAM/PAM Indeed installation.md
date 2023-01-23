Add role:
 
Добавляем Active directory domain service > Install

Выполняем настройку:
![[Pasted image 20220930132216.png]]
Настраиваем домен, перезагружаемся.
Савим роль Certification Authtority
Выполняем настройку из того же меню
Enterprise CA

AD Users and comps: View > Advansed features
Создаем 2 уч записи в AD:
account1, account2 - превилигированнаые уч. записи, PAM будет знать пароли, сбрасывать их.
Создаем группу IPAMAccounts, вводим в нее две уч записи созданные выше.
Используется для поиска учетных записей AD (в данном случае привелигерованные).
Так же создаем уч. записи
IPAMRead - для работы с каталогом пользователей
IPAMService - для сервисных операций в AD
IPAMStorage - для работы с медиахранилищем
IPAMService - уч запись, которая будет сбрасывать пароли от прив уч записей (acc1,2)
ей нужно выдать права на группу IPAMAccounts (сбрасывание пароля)  
![[Pasted image 20220930185859.png]]

Вводим тачку в домен
ставим ms sql server
установить mixer authentication (IPAM работает с MS SQL только с встроенной SQL учеткой)
обязательно включить поддержку TCP/IP для ms sql server (SQL server configuration manager)
Устанавливаем SQL server management studio
через него создаем БД:
IPAMCore - основная логическая БД
IPAMIdP -  база данных для хранения аутентификационных данных, второго фактора
IPAMJobs -  БД для сервисного выполнения задач по расписанию
ILS - БД для хранения событий происходящих в системе
Создаем уч запись (тип SQL): IPAMSQLService 
User mapping:
для всех 4х созданных баз выставляем права
![[Pasted image 20220930180545.png]]
owner нужен для создания таблиц и их структуры при установке IPAM, в последствии можно снять эту роль.


установить postgresql
в конце файла pg_hba.conf:
![[Pasted image 20220930175120.png]]
host для win тачек
local для unix
в address указываем пулл IP с которым можно подключаться к базе


заходим в pgadmin
создаем пользователя IPAMSQLService
![[Pasted image 20220930181301.png]]

создаем базу:
![[Pasted image 20220930181357.png]]
IPAMCore - основная логическая БД
IPAMIdP -  база данных для хранения аутентификационных данных, второго фактора
IPAMJobs -  БД для сервисного выполнения задач по расписанию
ILS - БД для хранения событий происходящих в системе


Переходим к настройке IPAMA (access server):
добавляем роль:
Intallation type - Remote desctop services installation
Standart deploy
session base desktop deployment
перезагружаем машину
через DEPLOYMENT servers > tasks можно добавить новые машины к RDS, если какой-то из сервисов стоит удаленно

создать коллекцию (имя кллекции с четным колличеством знаков) иначе mRemote не увидит эту коллекцию
![[Pasted image 20220930184341.png]]
User Groups: кто может пользоваться RDS службой
Выключить хранение профилей на диске

### Установка PAM Indeed
##### Установка сервера управления (IPAMM)
IPAMM дистриб, запускаем PSH `.\IPAMInstaller.exe` выбираем '1' (сервер управления)
IPAMA > дистриб, запускаем PSH `.\IPAMInstaller.exe` выбираем '2' (сервер доступа)
##### Генерируем 2 ключа для Core БД и IdP БД
MISK>Keygen> keygen.exe: Algorythm: AES
Сохраняем ключи, выходим
##### Создаем секреты для серверов (5шт):
MISC> ConsoleApp > PSH
`.\Pam.ConsoleApp.exe generate-secret` x5
 `.\Pam.ConsoleApp.exe generate-host-key --size 4096`
Сохраняем ключи, выходим

##### Создаем сертификат из CA:
run > mmc > file > add snap > certificates > computer acc > local > finish > ok
ПКМ personal > all tasks > request new cert
Next>Next> choose cert > Enroll > Close

##### Создаем самоподписанный сертификат:
PSH:
`New-SelfSignedCertificate -DnsName win_2019_ipamm.company.com -CertStoreLocation cert:\LocalMachine\My`
Экспортируем самоподписанный сертификат из MMC (do not export Private Key)
Импортируем его в Trusted Root Cert Auth (по умолчанию)

##### Устанавливаем сертификат в IIS:
IIS>Sites>DefaultWebsite>Actions>Bindings>ADD>HTTPS>SSL cert > CA cert > Ok > Close

Создать папку 'C:\IPAM\ILS' для временного хранения событий до отправки в БД
##### Настройка компонентов:
`С:\intepub\wwwroot\pam\core\appsettings.json`

* "ConnectionStrings": {
    "PamCore": "Меняем строки подключения (примеры есть в confluence)",
    "JobsQueue": "Меняем строки подключения (примеры есть в confluence)"
    

* *"Database": {
    "Provider": "mssql(указываем нужную)",

* *"Auth": {
    "IdpUrls": [
    https://ipamm.comapany.com/pam/idp
    ], обязательно маленькими буквами! ^

* *"ApiSecret": "вставляем наш секрет core",
 
* "PamGatewayIpAddresses": "IP адрес IPAMA",

* *"Encryption": {
    "Algorithm": "AES",
    "HashAlgorithm": "SHA512",
    "Key": "вставляем сгенерированнык ключ aes",

* "EnableSwagger": false, (поставить true, если нужна консоль с api)
* 
* "LogServer": {
    "AppId": "pam",
    "Component": "server",
    "EventCache": {
      "Directory": "C:\\IPAM\\ILS", (путь с экранированным слешом)

"Server": {
      "Url": "https://ipamm.comapany.com/ls/api",

"ManagementConsole": {
    "Url": ""Server": {
      "Url": "https://ipamm.comapany.com/pam/mc","

  "UserCatalog": {
    "RootProvider": "ad",
    "Providers": {
      "ActiveDirectory":
        "Id": "ad",
           "ServerName": "company.com", // address dc or DNS name
          "ContainerPath": "CN=Users,DC=company,DC=com", // LDAP path to container with users
		  // OU Users > properties > attribute editor > distinguishedName
          "UserName": "IPAMDARead", //ad user
          "Password": "1qazXSW@CDE#", // pass

IdP config:
`c:\inetpub\wwwroot\pam\idp\appsetting.json`
"ConnectionStrings": { //set Database IPAMIdP
    "DefaultConnection": "Server=win_2019_ipamm.company.com;Database=IPAMIdP;Integrated Security=False;User ID=IPAMSQLService;Password=1qazXSW@CDE#"

"IdentitySettings": {
    "AdminSids": 
      "S-1-5-21-2443327199-3145051135-2350685551-500" // PSH: whoami /user

"IdpUrls": 
      "https://ipamm.comapany.com/pam/idp" //copy from core json

"SigningCertificate": "PAM_IDP_CERTIFICATE_THUMBPRINT", // for balanser
    "GatewaySecret": "NWINZb/oMm6E5lzYtu0Oqe3Dm9v/c/3CtgoiF3Ny9fw=",
    "ConsoleAppClientSecret": "+cnf/um6up/i2plRVlmSK53o7+ixMFE7P4hmillBPx8=",
    "SshProxyClientSecret": "8kgpKU4fSgp0HWc/Xzn2+sovx4wol5RdXCNLMMTxlb8=",
    "CoreApiSecret": "8MJFOhNZMTB3fa0trDvio8LRLb3PbfM44OK9w8XoH44=",
    "IdpApiSecret": "nT8SGoimq+gUK9Lxxlxn+sC9qtgFlNVs3Sxe/+NbHo8=",
    "RemoteInstallerClientSecret": "оставляем пустым (для тестирования)",

"Encryption": {
	"Algorithm": "AES",
	"Key": "b71a745bd49e17b6b0448afbddde13549c4f8f8f2f492632a12af5fe0d4d48ca" //IdP AES key
  "PamSettings": {
    "ManagementConsoleUrls": [
      "https://ipamm.comapany.com/pam/mc"
    ],
    "UserConsoleUrls": [
      "https://ipamm.comapany.com/pam/uc"
    ],
    "CoreUrls": [
      "https://ipamm.comapany.com/pam/core"

Копируем остаток файла от UserCatalog  из файла параметров core

MC: `C:\inetpub\wwwroot\pam\mc\assets\config`:
Подставляем URL:
https://ipamm.comapany.com/pam/mc
https://ipamm.comapany.com/pam/core
https://ipamm.comapany.com/pam/idp
UC: `C:\inetpub\wwwroot\pam\uc\assets\config`:
Подставляем URL:
https://ipamm.comapany.com/pam/uc
https://ipamm.comapany.com/pam/core
https://ipamm.comapany.com/pam/idp

`C:\inetpub\wwwroot\ls\clientApps.config`
Внизу раскоментировать блок `<Application Id="pam" SchemaId="Pam.Schema">`
и закоментировать то, что внутри блока `<AccessControl>`
`<ReadTargetId>sampleDb</ReadTargetId>`
`<TargetId>sampleDb</TargetId>`

`C:\inetpub\wwwroot\ls\targetConfigs\sambleDb.config`
вставляем строкуподключения из core appsettings.json
меняем `Database=ILS`

добавляем браузер в доверенные (IE settings)
Выполняем запуск.
иногда надо править строку подключения, убирая домен, только название хоста.
https:/fqdn/pam/mc

IPAMA:

##### Правим конфиги:
* `C:\Program Files\Indeed\Indeed PAM\Gateway\ProxyApp\appsettings.json`
указываем URL'ки и секрет gateway
* `C:\Program Files\Indeed\Indeed PAM\SSH Proxy\appsettings.json`
указываем URL'ки, секрет ssh, host key

##### открыть порт для SSH PROXY (22 по дефолту):
win defender firewall > advanced settings > Inbound rule > new > port > 22 > allow > all  > IPAM SSH PROXY

##### Перезагрузка IPAMA сервера
##### Настройка служб:
* Проверяем запустились ли RDS и SSH proxy сервисы, если нет - включаем
* RDS > Collections > IID1 > Publish remote app programs > Add > 
`\\Win_2019_ipama.company.com\c$\Program Files\Indeed\Indeed PAM\Gateway\ProxyApp\Pam.Proxy.App.exe` > Next > Publish
* RDS > Collections > IID1 > Remoteapp programs > pam пкм > edit properties > parameters > allow any command-line parameters > apply > ok
##### Проверяем proxyapp
запускаем:
`C:\Program Files\Indeed\Indeed PAM\Gateway\ProxyApp\Pam.Proxy.App.exe`  руками
![[Pasted image 20221006151329.png]]
Заходим на IPAMM, создаем 3 шары:
`C:\IPAM\` с правами read write для пользователя IPAMADStorage
* MediaData
* Screencasts
* Shadowcopy

добавляем путь в консоли:
MC > конфигурация > системные настройки > путь к хранилищу
![[Pasted image 20221006152013.png]]
![[Pasted image 20221006152110.png]]
После этого сохранить и проверить proxyApp с IPAMA
Так же проверяем SSH proxy: `ssh win_2019_ipama.company.com`