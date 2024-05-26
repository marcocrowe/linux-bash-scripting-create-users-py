
# OS Scripting and Python Assignment

Creating a Python Script to Generate User Account

## Requirements

- **Programming Language:**
  - [Python &ge; 3.8.0](https://www.python.org/downloads/ "Python Downloads"): Python Programming Language
- **Integrated Development Environments (IDE):**
  - [VS Code](https://code.visualstudio.com/ "Visual Studio Code"): [Python](https://code.visualstudio.com/docs/languages/python "Python in Visual Studio Code") [^vs-code]: A code editor redefined and optimized for building and debugging modern web and cloud applications.
  - [PyCharm](https://www.jetbrains.com/pycharm/ "PyCharm"): The Python IDE for Professional Developers by JetBrains. Community Edition is free.
- **Version Control:**
  - [Git](https://git-scm.com/): Version Control System
  - [GitHub Desktop](https://desktop.github.com/ "GitHub Desktop"): Version Control System
  - [GitHub](https://github.com/ "GitHub"): A version control service that hosts Git repositories and provides a web-based graphical interface
  - [GitLab](https://gitlab.com/ "GitLab"): A complete DevOps platform, delivered as a single application
  - [Toptal - gitignore.io](https://www.toptal.com/developers/gitignore "Create Useful .gitignore Files For Your Project"): Create Useful .gitignore Files For Your Project
- **Operating System:**
  - [Windows 11](https://www.microsoft.com/en-us/windows/windows-11 "Windows 11"): Windows Operating System
  - [Ubuntu Desktop](https://ubuntu.com/download/desktop "Ubuntu Desktop") 20.04.3 LTS: Linux Distribution
  - [OpenSUSE Leap](https://www.opensuse.org/#Leap "OpenSUSE Leap") 15.6: Linux Distribution, generally choose *Intel or AMD 64-bit desktops, laptops, and servers (x86_64)*
- **Virtualization:**
  - [VirtualBox](https://www.virtualbox.org/ "VirtualBox"): Open-source Virtualization Software
  - [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install "Install Windows Subsystem for Linux"): Run Linux on Windows 10/11
- **Utilities:**
  - [tar](https://www.gnu.org/software/tar/ "GNU tar"): GNU tar - archiving utility

[^vs-code]: The VS Code Extensions recommended for Python and this project are in [extensions.json](./.vscode/extensions.json)

## Run

Clone the repository

```bash
git clone https://github.com/marcocrowe/linux-bash-scripting-create-users-py.git
```

Open a terminal set in the project root directory and run

```bash
python main.py assets/user-list.csv
```

or for a test run

```bash
python main.py assets/small-user-list.csv
```

---

## Assignment

Create a Python script that creates a Bash script to create user accounts on a Linux system.

### Python Script

Create a Python script [main.py](./main.py "Starter Python Script") which will take a CSV text file containing a list of users and generate a Bash script which will create Linux local user accounts for the listed users. You must run the script and save the required results. *This assignment is mostly about reading and writing files, and processing text strings.*

- The Bash script should be called `bash_create_users.sh`
- The Bash script should be written to the current directory.
- Your Python program should write helpful messages to the terminal as it runs, showing progress. Content of the messages is up to you.
- The input file of users should be given as a command line argument to the Python program. If no argument is given, the program should print a suitable message and exit.
- At the end, your Python program should indicate how many users have been processed.
- Your solution must include appropriate error handling and comments.

### The Input File

The input file is a plain text CSV file. The first line of the file contains the column headings. Each line contains the details of one user, as follows:

| surname | first_name | password | id_number | first_appearance | URL                                           |
|---------|------------|----------|-----------|------------------|-----------------------------------------------|
| Simpson | Marge      | 6MgR6xww | C00001001 | 1                | <https://simpsonswiki.com/wiki/Marge_Simpson> |
| Simpson | Homer      | 6MgR6xww | C00001002 | 1                | <https://simpsonswiki.com/wiki/Homer_Simpson> |

The fields are separated by commas. For example:

```cvs
surname,first_name,password,id_number,first_appearance,URL
Simpson,Marge,6MgR6xww,C00001001,1,https://simpsonswiki.com/wiki/Marge_Simpson
Simpson,Homer,6MgR6xww,C00001002,1,https://simpsonswiki.com/wiki/Homer_Simpson
```

### The Bash Script

The Bash script should use the [useradd(8)](https://linux.die.net/man/8/useradd "useradd(8") and [chpasswd(8)](https://linux.die.net/man/8/chpasswd, "chpasswd") commands to set up the accounts, using the system default settings for most things such as default files and shell. Refer to your Semester 1 notes for more information on these commands.

- User accounts should be named `first_name.surname` and be lowercase, e.g. `homer.simpson`.
- Each user should have a home directory in the usual `/home` location.
- The [Gecos field](https://en.wikipedia.org/wiki/Gecos_field "Gecos field") (user information) field in the password file should be set to the user's name and id number.
- Each user should be in their own private group (use options to useradd to do this).
- The generated script should be ready to run from the Bash command line, apart from execute permission needing to be set.

### Hints

The main program `main.py` should check the command line arguments, create and open and close files, write out error messages and status messages, loop through the CSV file and write the lines in the Bash script.

Build up your program slowly, tackling each task on its own, e.g.

- Check if a command line argument has been given, give an error if it hasn't and exit, otherwise accept the parameter.
- Create the Bash files and write the shebang lines (#!) with associated error handling.
- Loop through a small CSV file and call a function to simply print out each of the fields on each line of the CSV file. Try changing the order of the output e.g. the CSV file is in the order of surname, first name, password, id number - so print them out in reverse order.

Create a test input file with two entries so that you can easily test your Python program without creating a large number of accounts.

Test out the user creation commands before you code them in Python to make sure you know the necessary options.

[Remember the manual](/ "manual").

```bash
useradd --help # Run help
useradd homer.simpson --comment "Homer Simpson, C00001002"  --create-home --uid 1002  
echo "homer.simpson:password" | chpasswd
usermod # -- don't really need this one as options to useradd do everything.
userdel --remove homer.simpson
groupdel homer.simpson
```

**The output files are just plain text files** containing the commands for Bash.

### Grading criteria

You should upload a tar file containing the following.

1. Your Python program which is in two files:
   - the main program – named `main.py`
   - a `scripting_utility.py` module containing the functions to write to the two Bash scripts
2. A terminal session showing the Python program running (captured in a text file, not a screenshot). The progress messages should be in this.
3. The Bash create user script which your Python program created and the following files from manually executing/testing:
   - The `/etc/passwd` file showing the created accounts.
   - The `/etc/shadow` file showing the created accounts.
   - The `/etc/group` file showing the new user groups.
   - The output from `ls -l` of the `/home` directory showing the created home directories (in a text file as well)
4. The Bash delete user script which your Python program created and the following files from manually executing/testing
   - The `/etc/passwd` file showing the accounts no longer exist
   - The `/etc/shadow` file showing the accounts no longer exist
   - The `/etc/group` file showing the user groups no longer exist
   - The output from `ls -l` of the `/home` directory showing the home directories no longer exist (in a text file as well)

### Mark Breakdown

| Feature                                                                                                                                                                                     | Maximum Score |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------:|
| Structure and coding of Python scripts: use of functions, variables etc; import; printing messages and count of users; reading input file; error checking; command line arguments; comments |            30 |
| Modules for Python script: modules created and correctly used with import                                                                                                                   |            10 |
| Bash scripts generated and correct: `adduser`, `chpasswd` for each user; `userdel`, `groupdel` etc for deleting accounts. Correct options to create accounts as specified.                  |            15 |
| Terminal session running the Python scripts: shows they run, progress messages, final count.                                                                                                |            10 |
| A *Before and after* `/etc/passwd` files showing new accounts created and deleted: correct user names; fields filled in as specified.                                                       |            10 |
| A *Before and after* `/etc/shadow` files showing new accounts with passwords set; created and deleted                                                                                       |            10 |
| `/etc/groups` files showing user private groups created and deleted                                                                                                                         |            10 |
| Two `ls -l` outputs of `/home` showing the home directories of the new users, "before and after"                                                                                            |             5 |

### To Submit

You should save a [tar](https://www.gnu.org/software/tar/ "GNU tar") file containing the following.

1. Your Python program.
2. A terminal session showing the Python program running (captured in a text file, not a screenshot). The progress messages should be in this.
3. The Bash create user script which your Python program created and the following files after running the Bash script:
   - The `/etc/passwd` file showing the created accounts.
   - The `/etc/shadow` file showing the created accounts.
   - The `/etc/group` file showing the new user groups.
   - The output from `ls -l` of `/home` showing the created home directories (in a text file as well)

---
