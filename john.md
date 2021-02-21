# John the Ripper (Cracking)

## Send password protected zip to john
`zip2john filename.zip > hash`

## Crack
`john hash --fork=4 -w=/usr/bin/wordlists/rockyou.txt`

## Check for passwords
`john --show hash`