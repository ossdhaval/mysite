# Python notes

## installing Anaconda 3

```
argument to control this behavior.
installation finished.
Do you wish to update your shell profile to automatically initialize conda?
This will activate conda on startup and change the command prompt when activated.
If you'd prefer that conda's base environment not be activated on startup,
   run the following command when conda is activated:

conda config --set auto_activate_base false

You can undo this by running `conda init --reverse $SHELL`? [yes|no]

```

## Python variables and objects

- Python is completely object oriented, and not "statically typed". You do not need to declare variables before using them, or declare their type. Every variable in Python is an object.
      ```
      myfloat = 7.0
      print(myfloat)
      myfloat = float(7)
      print(myfloat)
      ```
  Both will print the same output. 7.0.
- Strings are defined either with a single quote or a double quotes. Double quotes makes it easy to include apostrophes
- Assignments can be done on more than one variable "simultaneously" on the same line like this `a, b = 3, 4`
- Lists are very similar to arrays. They can contain any type of variable, and they can contain as many variables as you wish. Lists can also be iterated over in a very simple manner.
      ```
      mylist = []
      mylist.append(1)
      mylist.append(2)
      mylist.append(3)
      print(mylist[0]) # prints 1
      print(mylist[1]) # prints 2
      print(mylist[2]) # prints 3
      for x in mylist:
      print(x)
      ```
## conditions

- If, else, and elif are followed by a `:`

     ```
      statement = False
      another_statement = True
      if statement is True:
          # do something
          pass
      elif another_statement is True: # else if
          # do something else
          pass
      else:
          # do another thing
          pass

     ```

#### How to run python code locally:

- activate the python environment. For example, `conda activate base`
- run python program: `python3 /tmp/p1-self.py`

  
#### indentation and spaces rules

- Blank lines are ignored
- Indentation is mandatory in Python to indicate blocks of code such as those following statements like if, for, while, def, and class.
- Each indented block must use consistent whitespace; mixing the number of spaces or tabs within the same block causes errors.
- The standard convention is to use 4 spaces per indentation level.

In summary, Python uses indentation not just for readability but as a core part of the syntax to define program structure, with 4 spaces per level being the widely accepted standard.


Indentation applies to all lines that belong to the same block and must be uniform in that block.

