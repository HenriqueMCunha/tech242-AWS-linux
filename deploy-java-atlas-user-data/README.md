# Deploy Java Atlas App Using User Data

One of the important things to consider when using user data to deploy Java App is location of directories.
The reason for that is that when using user data to deploy app rather than using a script manually, the default user is going to be the root user.

* Taking that into account, the script was edited to create a directory in `/home` called `ec2-user` and to move into that directory.
* From then, everything was installed in `/home/ec2-user` directory.
* Cloning of git repository was made into that same directory, creating a folder called `repo` to store the repository.
* To start the app, moved into `repo/springapi` and then executed the `mvn spring-boot:start`.


### Before Editing

```
#!/bin/bash

# update & upgrade
echo "UPDATING..."
sudo apt update -y
echo "DONE!"
echo "UPGRADING..."
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo "DONE!"
# install maven
echo "INSTALLING MAVEN..."
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
echo "DONE!"
# check maven is installed
echo "CHECKING MAVEN VERSION..."
mvn -version
echo "DONE!"
# Install JDK (Java) 17
echo "INSTALLING JDK 17..."
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo "DONE!"
# check java is installed
echo "CHECKING JAVA VERSION..."
java -version
echo "DONE!"
# copy the app code to this VM
echo "CLONING REPOSITORY..."
git clone https://HenriqueMCunha@github.com/HenriqueMCunha/tech242-jsonvoorhees-app.git
echo "DONE!"
# move to springapi
echo "MOVING TO SPRINGAPI DIRECTORY..."
cd tech242-jsonvoorhees-app/springapi
echo "DONE!"
# start program
echo "STARTING PROGRAM..."
mvn spring-boot:start
echo "DONE!"

```

### After Editing

```
#!/bin/bash

# make and move into new directory
mkdir /home/ec2-user
cd /home/ec2-user
# update & upgrade
mkdir /home/ec2-user
cd /home/ec2-user
echo "UPDATING..."
sudo apt update -y
echo "DONE!"
echo "UPGRADING..."
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo "DONE!"
# install maven
echo "INSTALLING MAVEN..."
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
echo "DONE!"
# check maven is installed
echo "CHECKING MAVEN VERSION..."
mvn -version
echo "DONE!"
# Install JDK (Java) 17
echo "INSTALLING JDK 17..."
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo "DONE!"
# check java is installed
echo "CHECKING JAVA VERSION..."
java -version
echo "DONE!"
# copy the app code to this VM
echo "CLONING REPOSITORY..."
git clone https://HenriqueMCunha@github.com/HenriqueMCunha/tech242-jsonvoorhees-app.git repo
echo "DONE!"
# move to springapi
echo "MOVING TO SPRINGAPI DIRECTORY..."
cd repo/springapi
echo "DONE!"
# start program
echo "STARTING PROGRAM..."
mvn spring-boot:start
echo "DONE!"

```