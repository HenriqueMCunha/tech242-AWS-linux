# Building a Script in Linux

### Create a new script file

Create a filen empty file with the file extension `.sh` (sh for shell).
We can ither create this file by using `touch` or `nano` commands.

### Plan our script

One of the imporatnt steps of creating a script is to plan how the script is going to work, or what steps it will take before starting to write our script.
* Example:
  ```
  # update

  # upgrade

  # install nginx

  # restart nginx

  # enable nginx
  ```

Note:

* Upgrade to the latest packages is pottentially dangerous as it will isntall latest versions to the OS that could break something.

### Manual Testing

The next step is to test every command we are going to use manually. 
    * This is imporatnt because we need to make sure that the commands are working as intended before adding them to the script / automate them.

Order of test:

* `sudo apt update -y`
* `sudo apt upgrade -y` 
* `sudo apt install nginx -y`
* `sudo systemctl status nginx` - To check a system process is running. We can also check this process by going to the EC2 instance and get the public IPv4 address, then copy and paste it into the browser. `ctrl + z, Enter Key` to exit and regain control of the terminal or `ctrl + c` 
* `sudo systemctl restart nginx` 
* `sudo systemctl enable nginx`

`apt` -> Relates to package manager
`systemctl` -> System control, manages system processes

### How to run a script file

Need to provide the path for that script - need to tell it where that script is.

./ - tells the shell to look for the file in the current working directory
file needs the permission to be executed

sudo chmod +x <filename> - gives executing permission to all users - colour also changes


Best practice is to edit script file to make sure we have a bit more assistance to help with troubleshooting.
echo is print
echo "I'm feeling great" - more than one word use quotation marks
echo hello - one word fine

there's two sitations in 2 situations
1 - you want them to run on a fresh virtual machine (it's to do with the concept of idempotency (or idempotent)
When we run a script, for the first time, but also, it runs no matter how many times we want it to and work. If that is the case, it means that script is idempotent.
We have to understand whether a script is idempotent. If it doesn't run after the first one, it is not idempotent.
A lot of devops tools are idempotent, will achieve the desired outcome/ output at the end.
2 - it runs no matter how many times we want it to and work.


### Environment Variables



printenv - prints environment
variable is something you want to store in memory
it shows certain values attached to those variable names
pwd outputs PWD = /home/ubuntu value for example

environment variables are often used to store sensitive information
program looks for that inforamtion
to then access the credentials that we need

never hardcode credentials!
you would use envi var to store those credentials
probably wouldn't have them in memory, just temporary


usual convention is to define them in capital letters and refer to them as well

printenv USER instead of printenv user for example
if we do sudo printenv USER will display user as root 
root has its own set of environment vairables


create an enviroment variable
store a variable - MYNAME=henrique  (JUST A VARIABLE; NOT ENV VARIABLE)
echo $MYNAME will output it

if you want to use something a lot in your script, variables are imporatnt

export MYNAME=Maria 
will save it as an environemtn variable
it's not only an env var but also a regular variable
it replaces the previous one in memory because we exported it

environment variable is not persistent so it will disappear after that session
add it to a file that loads up when we begin the session
add export command to bottom of .bashrc file

source .bashrc will reload the bashrc file

often we won't need env var to be persistent
a lot of times you'll need to create envi variables to access them later through scripts


