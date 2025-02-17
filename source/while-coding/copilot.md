# Copilot

Copilot = cp

- Open cp chat in VSCode : ctrl+alt+i
- Open inline chat in code: ctrl+i

## VS code: Copilot chat Vs Copilot Edits

These are two different views in copilot. While copilot chat is your natural language companion, the copilot edits is where the code editing happens. For example, if you want to create a new file, you have to go to copilot edits(ctrl+alt+shift+i). Then type `/new <relative path to file from project root>`

## Usecases

#### ask explain something in terminal

In this case it understood the git message in the terminal and correctly pointed out the file that was reported to be in conflict.

![image](https://github.com/user-attachments/assets/36956eeb-e5da-4c8f-995f-a2b8fd3acc75)


#### ask to uncomment code

In this, the first simple prompt didn't work. But when used with `/fix` it worked.

![image](https://github.com/user-attachments/assets/fb3ebf2e-61ca-4f1a-bbd7-7ec792797415)


#### ask to create new files

 - Go to copilot edits (ctrl+shift+alt+i)
 - `/new <path relative to project root>`
 - If your project root is `jans` and you want to create a file under `jans/docs/` the give command `/new docs/cedarling/quick-start.md`

#### find the missing files from a list of files

  -  problem: in mkdocs.yml, there are file paths listed like shown below. Ideally, All these files should be available under `docs/`. But some of these files don't. This leads to 404 when corresponding link is clicked on the doc site. Solution is to create these files. CP can help identify which files are missing.

  - Select the part of the code which you want CP to analyse
  -  Go to CP chat `ctrl+alt+i`
  - prompt `separate out file paths from #selection`

      ![image](https://github.com/user-attachments/assets/51bfe0ef-b983-4f26-82db-9a8572855ddd)
  - prompt: `prepend docs/ to these paths`

    ![image](https://github.com/user-attachments/assets/a9622d54-e308-4861-84fb-86ae4c540cf5)
  - as you can see above, some of the files are still not identified as files. Those are the missing ones.
  - I couldn't get copilot to create these files automatically.
    
