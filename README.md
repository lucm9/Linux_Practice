# Linux System Administration Assignment: Onboarding New Users
**Objective:** 

We need to onboard three new users to our Linux server: `James, Matthew Peter, and John`. 
This involves creating individual user accounts for each of them, securely configuring their ability to access the server, and granting them the necessary privileges to execute administrative commands via `sudo`.

**User Account Creation:** 
We need to run the following commands 
```
sudo useradd -m James
sudo useradd -m MatthewPeter
sudo useradd -m John

the option `-m` ensure the user home directory gets created if it doesn't exist already.
```
![1 create_user_and_verify](https://github.com/lucm9/Linux_Practice/assets/96879757/e90d9f9c-f4f8-4c8d-916b-61cd9f6eef71)

**Sudo privileges:** 
Add each user to the sudo group in order for them to execute administrative commands via `sudo`
![6 sudo_vi_error](https://github.com/lucm9/Linux_Practice/assets/96879757/57097621-dc70-41a6-83ee-b04b362e15aa)

before adding the user to the sudo group we have an error. Lets go ahead and add the user by running the following command:

`sudo usermod -aG root James`

also verify the visudo the `sudoers` file ensure the configuration are set correctly. Also verify which group we need to add our user to in order for our users to have `sudo` previleges.
**Public Key Upload:** 

For this exercise we will make use of `EC2 Instaces`
![5 James_VM](https://github.com/lucm9/Linux_Practice/assets/96879757/5de5dc02-8118-4482-93d3-95ae5b26d1a6)

![4 generate_ssh_keygen](https://github.com/lucm9/Linux_Practice/assets/96879757/f9f38d9b-e27e-4700-ab1a-53a26f79470d)

I have created an Ec2 instance names `JamesVM` this instance will have its own `Public-key`. To generate the public key we need to run `ssh-keygen`. 
Each new user will provide you with their public SSH key. You are required to set up SSH key-based authentication for each user.

![2 switch_user](https://github.com/lucm9/Linux_Practice/assets/96879757/7c6d9be0-523b-4b92-a2ed-a3b3d95c1d82)

Place each user's public key in the appropriate location within their home directory to enable secure SSH access.
```
mkdir .ssh
cd .ssh
touch authorized_key
vi authorized_key - copy and paste the public key from the users machine. 
```
![3 authorized_key](https://github.com/lucm9/Linux_Practice/assets/96879757/9a5f26da-c0d2-43ed-9b40-260ae939b9d0)

**Successful Connection:**

![7 Successfully_login](https://github.com/lucm9/Linux_Practice/assets/96879757/325895ec-206b-4be7-867a-689dc520b8e3)

*Deliverables:
**Reflection:** 

During the process of setting up a new user and granting them sudo access, I encountered a couple of challenges. Firstly, there was the issue of determining the appropriate group to grant sudo privileges, as it varied depending on the Linux distribution being used.
In this case, the standard sudo group didn't exist, so I had to identify the equivalent group (wheel in this instance) to add the user to.

Key-based authentication plays a vital role in enhancing security when accessing a server remotely. By generating and using SSH key pairs, users can authenticate without the need for passwords, significantly reducing the risk of unauthorized access through brute-force attacks or password guessing. 
It also simplifies the authentication process for users, as they don't need to remember complex passwords.


Assignment 2:
**Objective:** 
The goal of this assignment is to reinforce your understanding of the Linux filesystem, including file and directory creation, navigation, and basic manipulation. You will practice using essential command line tools to work with the filesystem effectively.
*Requirements:
*Directory Structure Setup:
Create a new directory named `MyWorkspace` in your home directory.
`mkdir MyWorkspace`

Inside `MyWorkspace`, create three directories: `Projects`, `Templates`, and `Notes`.
```
cd /MyWorkspace
mkdir Projects Templates Notes
```
In `Projects`, create two empty directories named `ProjectA` and `ProjectB`.
```
cd /MyWorkspace/Projects
mkdir ProjectA ProjetB
```

*File Creation and Organization:
In the `Notes` directory, create an empty text file named `meeting_notes.txt`.

```
cd /MyWorkspace/Notes
touch meeting_notes.txt
```
In the `Templates` directory, create two empty files: `report_template.doc` and `invoice_template.xls`.
```
cd /MyWorkspace/Templates
touch report_template.doc
touch invoice_template.xls
```
*Navigating the Filesystem:
Navigate to the `Templates` directory and list the files it contains.
From the `Templates` directory, change your current directory to `Projects` using a single command.
`cd /home/ec2-user/MyWorkspace/Projects`

*Modifying Filesystem Contents:
Move `meeting_notes.txt` from the `Notes` directory to `ProjectA`.
```
cd  /home/ec2-user/MyWorkspace/Notes
mv meeting_notes.txt /home/ec2-user/MyWorkspace/Projects/ProjectA
```
Copy the `report_template.doc` from `Templates` to both `ProjectA` and `ProjectB`.
```
cd  /home/ec2-user/MyWorkspace/Templates
cp -R report_template.doc /home/ec2-user/MyWorkspace/Projects/ProjectA /home/ec2-user/MyWorkspace/Projects/ProjectB
```
*Cleanup:
Delete the `invoice_template.xls` file from the `Templates` directory.

`rm invoice_template.xls`

Remove the `ProjectB` directory and all its contents, ensuring you do not receive any error messages even if it's not empty.

`rm -rf ProjectB`


Creating Directories and Files:
Create a directory named `ProjectData` in your home directory.

Inside `ProjectData`, create two directories: `Reports` and `Data`.
Within `Reports`, create an empty file named `Summary.txt`.
In the `Data` directory, create three empty files: `data1.csv`, `data2.csv`, and `log.txt`.
*Navigating the Filesystem:
Use the command line to navigate to the `Reports` directory from your home directory.
Then, navigate to the `Data` directory using a relative path.
*Viewing Directory Contents:
Display the contents of the `ProjectData` directory in a detailed list format, including hidden files.
Explain what the information in this detailed list means (file permissions, number of links, owner name, group name, file size, and date of last modification).
*Copying and Moving Files:
Copy `log.txt` from `Data` to `Reports`.
Move `data1.csv` from `Data` to `Reports`, and rename it to `report1.csv`.
*Deleting Files and Directories:
Delete the `log.txt` file from the `Reports` directory.
Remove the `Data` directory and all of its contents.

![image](https://github.com/lucm9/Linux_Practice/assets/96879757/ecf5af90-6e04-4a7f-804b-75f308a7507c)

![image](https://github.com/lucm9/Linux_Practice/assets/96879757/fcea5a15-5a52-4007-ae40-966bf7de8def)

