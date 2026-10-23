

# Commands
---
To create a new key from scratch use the  command to fill in the info. 

```
# Fill in the info command asks for
gpg --full-generate-key

```

To see the secret for the key to add to gh or other platform use the following: 
CAUTION
DANGEROUS COMMAND ITS SECRET FOR A REASON
``` bash
#!/bin/bash

sleepytime='sleep 5'

warndatatext=$(warndata)

function warndata {
  printf "Dangerous information, can potentially expose sensitive information to terminal or log files, use with extreme caution. Some small mitigations are meant to protect your information."
  printf ""
}
read -p 
gpg --list-secret-keys --keyid-format=long > secret_delete_quickly.txt 

clear

cat secret_delete_quickly.txt 

printf ""
printf "If you need the info copy it now."
printf ""
sleep 5

```