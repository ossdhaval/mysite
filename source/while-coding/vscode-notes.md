# VSCode Notes

## Essential setup items
- install gitlens from gitkraken for git history visualization
- in settings(ctrl+,), search for `gpg` and enable commit signing for both (user and workspace)
- in settings(ctrl+,), search for `signoff` and enable the `Git: always sign off` for both (user and workspace)

## Shortcuts


- ctrl+shit+p: command palette

## cloning a new project from Github

- From explorer, open the parent folder where you want to store the code
- now you can either use the command palette and search for `git clone` to get the code, or use terminal and use git commands to get the code
  - command palette: If you use this, the VScode will require login to the github
  - using terminal it is easy.
    - go to the parent folder where you want to clone the repo. For example `/home/xyz/vscode`
    - then check if you have a `.git` directory already there. If it exists, then the parent directory is already initialized. You don't have to run `git init`. Else run `git init`
    - then run `git clone <https-url-for-cloning-the-repo>`
    - This will create a new directory under the parent with the code from github `/home/xyz/vscode/my-repo`
- in vscode, you should download extension from microsoft `extension pack for java`. This extension pack installs 6 extensions to support java development.

## Enabling settings sync

When you turn on sync, your settings are linked to a Microsoft(outlook) or github account. Suppose you have a VSCode on your desktop and you also want same settings on GitHub codespaces. Do the following:

- On desktop VSCode
  - Go to `settings` > `backup and sync settings`
  - Choose what you want to sync and Click on `sign in`
  - Select GH or microsoft account (I have used ossdhavalATTHERATEoutlookDOTcom)
  - and done. You settings sync is turned-on on desktop VSCode
- On GH codespaces
  - to make sure your codespaces are using the same settings as desktop VScode do following
  - go to GH web
  - settings
  - go to `Code, planning, and automation` > `codespaces` section
  - there is a section for `settings sync`, enable it
  - also, since codespaces open for a particular repo, you have to add repo in the trusted repo list on the same page. Now when you open the codespace for that repo, settings will be synced. 

## References
- msft doc for using java in VScode: https://code.visualstudio.com/docs/java/java-tutorial
- keyboard shortcuts(OS vise): https://code.visualstudio.com/docs/getstarted/tips-and-tricks#_keyboard-reference-sheets
