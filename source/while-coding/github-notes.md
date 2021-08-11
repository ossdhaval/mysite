### setting up github commit signature verification:
- First check that your email id is verified:
  - go to github->user settings->emails->see if it mentions 'unverified' below your email id
  - ref [here](https://docs.github.com/en/github/getting-started-with-github/signing-up-for-github/verifying-your-email-address)
- Check if you have a GPG key (private-public key pair) already generated for this email id on your machine
  - `gpg --list-secret-keys --keyid-format LONG`
- if you don't have a key generate it
  - while generating the key, it'll ask for inputs, most of it is ok to keep default and email is your github (preferrably private, or public) email id.
  - `gpg --full-generate-key`
  - ref [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/generating-a-new-gpg-key)
- Now check the key that got generated
  - `gpg --list-secret-keys --keyid-format LONG`
  - output have a line similar to `sec   rsa4096/<your key> 2021-06-02 [SC]`
- Now, set GPG key in your local git client
  - `git config --global user.signingkey <your key>`
- Now we need to add same key to your github account
  - get public key block
    - `gpg --armor --export <your key>`
    - copy the entire text that got printed on your screen, starting from first '-' to last '-'
  - now go to github->profile->settings->SSH and GPG keys->New GPG key. Paste public key block that you copied in step above.
- after this whenever you want to sign a commit add `-S` flag
  - `git commit -S -m your commit message` 


Above steps were derived from links given [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification)

### issues vs PRs
  
  #### Issues
  - Used for raising bug or feature requests or tracking large development work
  - Focus is around requesting, planning and tracking tasks and work

  #### PRs
  - Used for tracking, discussing code changes 
  - Focus is on code and not planning or tracking work
