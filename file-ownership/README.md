# Research file ownership

## Why is managing file ownership important?

Managing file ownership is important in order to maintain data security by preventing unauthorized access.
It is also important for avoiding users who have different permissions to edit or overwrite current files.

## What is the command to view file ownership?

In Linux, the command to view ownership is `ls -l`.

## What permissions are set when a user creates a file or directory? 

The permissions for a file or directory are represented by a three-digit octal number, such as 644 or 755. These digits represent the read, write, and execute permissions for the owner, group, and others:

* Read (r): The user can read the contents of the file or directory.
* Write (w): The user can modify the contents of the file. For directories, this permission allows the creation of new files and subdirectories within the directory.
* Execute (x): The user can execute the file or change into the directory. For directories, this permission allows the user to list the contents of the directory.

The default permissions for newly created files are 644, which means the owner has read and write permissions, the group has read permissions, and others have read permissions. The default permissions for newly created directories are 755, which means the owner has read, write, and execute permissions, the group has read and execute permissions, and others have read and execute permissions.

The default permissions for files in Linux are 644 for text files and 755 for executable files. However, these permissions can be changed to any combination of read, write, and execute permissions for the owner, group, and other users.

![Screenshot permissions-file-directory.png](<../readme-images/Screenshot permissions-file-directory.png>)

### Who does file or directory belong to?


The ownership of a file or directory is determined by the user who creates it. The user who creates the file or directory is automatically made the owner of the file or directory. The owner can also change the ownership of the file or directory to another user or group.

For example, if user henrique creates a file named <myfile>, the permissions for the file will be 644, and the owner of the file will be henrique. User richard cannot read or modify the file unless he is granted permission by henrique.

## Why does the owner, by default, not receive X permissions when they create a file?

The owner of a file in Linux does not receive execute permissions by default when creating a file due to the concept of the umask.
Umask is a user-defined mask that restricts the default permissions assigned to files and directories when they are created. The umask is typically set when a user logs in and is stored in the user's /something/profile or ~/.bashrc file. 

* A typical umask for a standard user is 0022, which masks out the execute permission for others (o) and for group members (g), leaving only read and write permissions for the owner (u).
* This default setting is intended to enhance security by preventing users from accidentally granting execute permissions to files or directories that should not be executable.

For example, if a user creates a script file and does not explicitly set the execute permission, it will be readable and writable to the owner but not executable by anyone else. This helps prevent unauthorized users from running the script without the owner's knowledge or intent.nano

If the owner needs to grant execute permissions to a file or directory, they can use the chmod command to explicitly set the x permission:
* `chmod u+x filename` -> This overrides the umask and sets the execute permission for the owner (u).

To grant execute permisions to the group and others: 
* `chmod ug+x filename` ->This overrides the umask and sets the execute permission for the owner (u) and the group (g).

To grant execute permissions to everyone at the same time:
* `sudo chmod +x filename`

![Screenshot-file-permissions-owner.png](../readme-images/Screenshot-file-permissions-owner.png)

## What command is used to change the owner of a file or directory?

The `chown` (change owner) command is used to change the owner of a file or directory. 
If I wanted to change the owner of bad_jokes.txt to Richard, I would write it as so:
* `chown richard bad_jokes.txt`

If I want to change the owner of a directory, do the `-R` flag after as it will recursively change the owner of the directory and all its contents.
* `chown -R richard bad_jokes.txt`



