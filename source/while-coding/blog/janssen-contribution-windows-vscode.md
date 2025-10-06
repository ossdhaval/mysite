# Contribute to Janssen Project

## Windows workspace setup

## Prerequisites

- VSCode

## Steps

1. Install VS Code
2. Setup GPG key
   1. https://gpg4win.org/download.html. Donate if you want else, click on $0 and download.
   2. open powershell
   3. gpg --full-generate-key
   4. gpg --list-secret-keys --keyid-format=long
   5. copy the key from the `sec` section and after the `/`. For example: `82TT34089E33256B`
   6. gpg --armor --export 82TT34089E33256B
   7. copy entire output. including the `-- begin ` and ` end --`. 
   8. go to github.com -> settings -> `ssh and gpg keys` -> add new gpg key with any title and content you copied.
   9. git config --global user.signingkey 82TT34089E33256B
   10. git config --global commit.gpgsign true
3. Setup VS code
   1. Open settings `ctrl+,`
   2. search for `gpg` and enable commit signing for both (user and workspace)
   3. search for `signoff` and enable the Git: always sign off for both (user and workspace)
