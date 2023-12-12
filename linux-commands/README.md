# Linux Commands

## Navigating Commands

* `cd ~` Takes user back to home directory
* `cd <folder-name>` Moves present working directory to the specified folder
* `cd /` Moves present working directory to root
* `cd ..` Moves pwd to parent folder
* `cd /home/user/folder` Would be moving to a folder via an absolute path 

## File Commands

Note: The way Linux understands a file is very important. Even if we rename a file and change its extension, Linux will still look at the file and know what type it is.
Note: Linux treats everything like a file, whether it's a folder or not.

* `mkdir <name-of-folder>` Create a new directory in current working directory. (Can create more than one directory in the same command)
* `curl <link>` To Download a file into virtual machine. Very Important!
* `rmdir <directory-name>` Deletes specified directory.
* `rm -r <directory-name>` Deletes a specified directory recursively (Dangerous to use).
* `touch <file-name>` Creates an empty file.
* `rm <file-name>` Deletes the specified file.
* `nano <file-name>` Edits the file (It can be used without having a file created already). Use `ctrl + S` to Save and `Ctrl + X` to Exit editor.
* `cat <file-name>` Shows the content of the file.
* `head -<number-of-lines>` Get lines from the beginning of the file.
* `tail -<number-of-lines>` Get lines from the end of the file. Useful to find the last entries on a log file, for example.
* `nl <file-name>` Numbers lines in a file.
* `grep <string>` Finds a string in a file and highlights it. Returns the whole line in which string is found.
* `cat <file-name> ! grep <string>`
* `mv <file-name> <new-file-name>` Rename a file.
* `mv <file-name> <location>` Moves a file to location of our choosing. Can use absolute paths, `~` for home directory or `..` for parent folder for example.

## Super User

There's a user called root, which has super permissions, meaning permissions to do anything on the system.
Not being root user stops regular users from accidentally doing things only super users should be able to do.
To do certain actions(i.e. install tree) we'll need to have permissions of root user. 
To temporarily login as a root user:
  * `sudo su` Super user.
  * `exit` will stop temporary user status and return to regular user.