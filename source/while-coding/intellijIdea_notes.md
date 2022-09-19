# intellijIdea notes

Good beginner tutorials :

https://www.youtube.com/watch?v=S764o0mAXhg&list=PLs5n5nYB22fI83_UAFbPLC-Mg9Uc6jeU4&index=3&t=0s



https://www.youtube.com/watch?v=1bCgzjatcr4&list=PLs5n5nYB22fI83_UAFbPLC-Mg9Uc6jeU4&index=3



https://www.youtube.com/watch?v=uUzRMOCBorg&list=PLs5n5nYB22fI83_UAFbPLC-Mg9Uc6jeU4&index=4





eclipse to intellij



workspace -> project

project -> module

facet -> facet

library -> library

jre -> sdk

classpath variable -> path variable

Intellij shortcuts ( to see all shortcuts go to settings (ctrl+alt+s) and select 'keymap'):

alt+7 -> structure(or outline in eclispse)

ctrl+f -> search in file

ctrl+r -> replace in file

ctrl+shift+f -> find global ( equivalent to ctrl+H in eclipse )

ctrl+shift+r -> replace global

ctrl+f3 -> go to next occurance of selected word in a file (equivalent to ctrl+k in eclipse)

all these and more options under edit->find

shift+shift -> search for anything, including Idea menu options and settings etc

ctrl+n -> search for classes ( part of dialogue with above shortcut )



alt+f12 -> open terminal

all these options under view->tool windowns ( like 'show view' in eclipse )



press 'escape' from anywhere to bring control back to editor window

Shift+Escape moves the focus to the editor and hides the current or the last active tool window.

F12 moves the focus from the editor to the last focused tool window.

ctrl+shift+f12 : minimize or maximize editor window

ctrl+alt+s : opens settings window

ctrl+alt+y : reload all from disk

ctrl+H : open class hierarchy

ctrl+shift+H : highlight a method name and this will show which class defines it and which ones implement or override it

ctrl+alt+H : Method call tree. Highlight method name and this will show other methods which are calling this method (top-left first icon on the tool window), and methods being called by this method are recursively (second icon on tool window)

ctrl+click: on a method or variable will take you to declaration of it. To navigate backwards use : alt+shift+left key. To navigate forward, use alt+shift+right.



Custom settings:

> go to keymap and remove `shift+esc` from `hide active tool window`. This is because same short cut is used for focusing back on editor. After removing this, you'll be able to switch to editor without hiding the current tool window.

> in keymap, under `terminal`, remove `esc` from `switch focus to editor`. This is because many times to break terminal commands we use `esc` instead of `q`. This accidental press of `esc` moves focus to editor and then whatever you type gets written to editor file by mistake. To avoid this, change this setting.



In order to integrate with Github

- go to vcs menu and use 'get from version control' 

in order to start getting content assist

- setup sdk

- make directory as source root or test root

in order to build project

- setup output path in project structure screen





ERROR fixing :

'Java 14 not supported' error on 'build output' when trying to build a project.

- Root cause was in 'project structure' dialogue where it was mentioned that 'Project language level' was java 14. And the SDK I had was java 11. Error solved once i selected 'SDK default' in the language level.



To see which SDK(JDK) you are using :

file->project structure->project settings->project



to remove a module from project :

file > project structure > select the module and then click '-' at the top of the panel



ctrl+f12 : open list of members of current class that you can search ( like ctrl+o in eclipse )



ctrl+i : to see what are the interface methods you need to implement in implementing class



formatting json :

if you have a JSON text  and you want to view it in proper format, you can do it in intellij :

>    create a scrap file with .json extention.

>    paste your Json in it

>    press ctrl+alt+L



Setting for intellij will ask which project to open at the starup :

shift+shift : search for 'startup'

you'll see option 'reopen project at startup', go there and setup as you wish



Intellij debug keys :

f7 : step into

f8 : step over

f9 : resume programe



> make a simple project or module a java module :

Right click on project/module name > "add framework support" > check 'maven'

this will enable all the java related things in that project, including context help and compilation 

errors etc. 



Searching using ctrl+shift+f

How to search a string in files accept files with `Test` in its name:
enable file mask -> put pattern like `!*Test.java`
now give the search string.
How to search with in files of a directory only
click on `directory` and then give path of your choice.
Use `scopes` for more granular control
use `module` if you want to see occurrence of a string only within one module of project
Now once you have the results, to browse the results it is easier in find window, so press `ctrl+enter` or click `open in find window`
In the find window, to easy browsing, make sure the group-by settings are correct
click on icon on left bar in find window
ensure that only `module`, `flatten module` and `package` are enabled.


Structure and properties:

when you are viewing structure of a class (alt+7), it will show all the getters and setters also. This makes spotting real methods difficult in the structure. To avoid this, always keep `show properties` on (purple botton on top bar of the structure tool). This will club all the setters and getters with its relevant field and call it properties. Now you have clear view of all the fields and real methods of the class in the structure tool





#### auto generate UML sequence diagram from code

 - install `sequenceDiagram` plug in for intellij. ( install may fail couple of times )



### how to get problem analysis on entire project and not just one file

This was required when I wanted to find out how many problems are there in all the .md files across the project. By default, the `problem` view only shows problems for currently selected file. 

To see the problems in all files, you have to click on `project errors` tab in `problems` view. Then click on `inspect` the project (if you are not able to build it). It'll list all the issues in entire project.

### opening a file while working in intellij terminal

There is no direct way, but you can select the file name (with path if possible) and then click ctrl+shift+N, this will automatically search for the file in the text selection along with the path.

#### Troubleshooting:

scenario: I was working on one branch of project. Then I switched the branch. suddenly, Idea stopped giving context help, or stopped showing hyperlink in name of classes in code where you can click on it and go to that class. Even you can't find class using ctrl+n.

solution:

I noticed that pom file for all the child projects were shown as ignored ( greyed out and strikethrough ). On searching I found that they were ignored under ( settings (ctrt+alt+s) > build,executing,deployment > maven > ignored files). There is a list of files with checkbox which are ignored. I unchecked all and everything started working.
