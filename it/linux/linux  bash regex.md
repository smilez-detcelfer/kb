
**start with** ^text 
**end with** text$
`*` - any number of any symbols
`?` - any symbol
`[abc]` - a **or** b **or** c
`[0-9]` - from 0 to 9
`!` - negative


starts with 'abc' `egrep '^abc'`
end with 'abc' `egrep '^abc'`
start with 'abc' or 'def' `egrep '^(abc | def)'`
start with digit `egrep '^[0-9]'`
start with letter `egrep '^([a-z]|[A-Z])'`
start with digits (3 in row) `egrep '^[0-9]{3}'`

fgrep to find special sympols: `fgrep c$`
