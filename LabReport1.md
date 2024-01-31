# CSE 15L Lab Report 1
## Remote Access and FileSystem
### Flora Kang

The commands *cd*, *ls*, and *cat* were used in the workspace created week 1 to learn about the basic filesystem commands.

## 1. cd

Screenshot:
<img width="648" alt="Screen Shot 2024-01-30 at 10 13 10 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/d4c0cdd2-6553-42cd-8913-4082f03db939">

**command with no arguments**

The command *$ cd* was used and no output was given. No error message was given. The working directory was */home*. There was no output because the command *cd* changes the working directory. Therefore, a path to a directory must be provided to change to. With no valid argument, the working directory remains the same.

**command with a path to a directory as an argument**

The command *$ cd lecture1* was used to change the working directory from */home* to */home/lecture1*. There was no output but we can see from the prompt shown on the next line *[user@sahara ~/lecture1]* that the working directory was properly changed. There was no error.

**command with a path to a file as an argument**

The command *$ cd /home/lecture1/messages/en-us.txt* was used to change the working directory from */home/lecture1* to the *en-us.txt* text file. This resulted in an error message stating that the provided argument is not a valid directory that can be used as a working directory. The working directory remained the same.

## 2. ls

Screenshot:
<img width="548" alt="Screen Shot 2024-01-30 at 10 16 18 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/e4d3c25d-e9af-4af7-8535-c73174a3fea2">

**command with no arguments**

The command *$ ls* gave the output *lecture1*, the folder in the current path. The working directory was */home* and no errors were given.

**command with a path to a directory as an argument**

The command *$ ls /home/lecture1* was used with the output *Hello.class Hello.java messages README workthru.txt*, listing the files and folders within the directory the given path led to. The working directory remained */home* and there was no error.

**command with a path to a file as an argument**

The command *$ ls /home/lecture1/messages/en-us.txt* was used to list any files or folders of the given path. Since the path led to a text file, the output simply stated the path itself as there were no files or folders within. The working directory remained */home* and there was no error.

## 3. cat

Screenshot:
<img width="513" alt="Screen Shot 2024-01-30 at 10 15 24 PM" src="https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/82da6fde-4a17-4ab8-a955-f8994e53c40f">

**command with no arguments**

The command *$ cat* was used in the last line of the screenshot above and no output was given. No error message was given, but the terminal ceased to prompt further commands. The working directory was */home*. 

**command with a path to a directory as an argument**

The command *$ cat /home/lecture1* was used to print the contents of the files given by the path. The output gave an error message that the given path is a directory, not a file with specific contents to print. The working directory was */home*.

**command with a path to a file as an argument**

The command *$ cat /home/lecture1/messages/en-us.txt* was used with the output *Hello World!*, the contents of the text file of the given path. The working directory was */home/lecture1*. There was no error message as the command was used correctly.
