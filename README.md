# Getting Started with Git and Submitting Your Work for the Assigment

## Installing Git

### If you are using a USB stick

- Go to https://git-scm.com/download/win
- Download 64-bit Git for Windows Portable. Make sure it is the portable version!
- Run the downloaded _.exe_ file.
  - It will ask you where you want to install git.
  - Enter the drive letter of your USB stick followed by _git_ e.g. _D:\git_
  - Select 'ok'
  - Git will install. It may take a bit of time, be patient.
- Open the _git_ folder and start _git-bash.exe_.

### On your home machine

- Go to https://git-scm.com/downloads.
- Select the latest version of Git for Windows/Mac.
- On Windows accept the default settings during the install.
  - I can't test this for Mac.
- At the end of the install open _git-bash_.

### Enter Some Basic Settings

Enter the following user settings, making sure you use your own student number and name

```
git config --global core.autocrlf true
git config --global user.email "u01234567@unimail.hud.ac.uk"
git config --global user.name "firstname lastname"
```

- You should now be set up with Git.

## Sign up to GitHub

GitHub is a cloud based service that allows us to back-up and share our code.

- Go to https://classroom.github.com/
- Select 'sign in'
- Select 'Create an account'
- Complete the form using your university email address.

## Register for the assignment

- On Brightspace, under _Assessment>Assignment 1_ click on the _Assignment GitHub_ link.
- Join the classroom by finding your student number in the list.
- Accept the Assignment
- You should get confirmation that you've accepted the assignment and a link to your own individual private repository.
  > Repository or 'repo' is simply a storage area for all your project's file.
- Click on the link to your repo, you should find it contains a single README.md file.

## How to upload your Laravel Assignment to the Assignment Repository

- Open _git-bash_
- Navigate to your Laravel Assignment Project e.g.

```
cd D:/xampp/htdocs/assignment1
```

> On your home machine you can probably right-click in your project folder and open _git-bash_.

- Enter `ls` to check you are in the correct folder
- One at a time, enter the following commands into git-bash, make sure you enter the URL of your repository.

```
git init
git branch -M main
git remote add origin https://github.com/CHT2520/assignment-1-change-this-for-your-url
git add --all
git commit -m "Initial commit"
git push -u origin main --force
```

- A pop-up box may appear saying 'Select a credential helper'
  - Select manager (you may be asked to login in to GitHub in a browser)
- Your files should upload to your GitHub repository
- Back in a web browser refresh your GitHub repository's homepage, you should find that all the files from your local repository have been uploaded to the remote.

We have to use the `--force` flag because your remote already contains a README file. `--force` means we will overwrite the remote README file with the one that is your Laravel project. Normally, when push to a remote we don't use `--force`.

> You may get an error stating _fatal: detected dubious ownership in repository_. If you do you need to declare the folder as being safe e.g.
> `git config --global --add safe.directory D:/xampp/htdocs/assignment1`

## To Make Further Changes

You will probably want to make further changes to your Laravel app.
Everytime you've made a significant change e.g. added a new feature, you'll want to commit these changes and push them to your remote. To do this make sure Git Bash is in your project folder and use the following commands:

```
git add --all
git commit -m "Enter a meaningful message that describes the new feature"
git push -u origin main
```

- Double check to make sure the remote contains the updated code.

> Important
> Git doesn't upload all the files. This is intentional e.g. we don't want to move all files in the _vendor_ folder, and by default we don't want to copy sensitive data like passwords so the _.env_ file isn't copied. In your repo there is a special file call _.gitignore_ that tells Git which files shouldn't be uploaded. Open this in VS Code to see how it specifies files and folder that should be ignored.

## Moving work from one machine to another

For example you might be working on a USB stick at university, you've uploaded your project to GitHub and then you want to continue working on it on your home PC.

### At home (the machine you want to copy to)

- In your _htdocs_ folder.
- Open git-bash in this folder enter the following command making sure you enter the URL of your repo.

```
git clone https://github.com/CHT2520/assignment-1-change-this-for-your-url
```

- The files should download to this folder
- Enter the following Composer command:
  ```
  composer install
  ```
- The project's dependencies should now download and install.
- Change the _DocumentRoot_ setting in your _httpd.conf_ file to point to the _public_ folder of your Laravel project.
- Save a copy of _env.example_ as _.env_.
- Edit the _.env_ file to specify the correct settings for the database on the local machine.
- Make sure your shell/terminal is in your Laravel project folder.
- Enter the following to set up your database tables
  ```
  php artisan migrate:fresh --seed
  ```
- You should then be ready to continue with your work.

### Moving the changes back to the USB

On your home PC you should now have the most up to date version of the project. So commit these changes and push to the remote e.g.

```
git add --all
git commit -m "Added a new feature"
git push -u origin main
```

- Check the changes can be viewed on the remote repository.
- On your USB
  - Open git-bash
  - navigate to your project folder.
  - Enter the following
  ```
    git pull origin main
  ```
- This will download the changes you made from home.
- Open the project in VS Code to check the changes are present.
