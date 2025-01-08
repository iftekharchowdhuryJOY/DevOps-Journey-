# What is git?
Before git, you have to know version control system.

## What is version control system?
Just imagine you made a website which is bunch of html, css, javascript. The whole website is made of code. Now, when we built house we need to maintain the house, sometimes we
change the colors, kitchen stuff, washroom or bricks. Same goes for your software. So, you need something to manage your source code. That's where VCS comes. VCS is a source 
code management system software. **to manage your code or software we need version control system.**

## Types of version control system?
1. Distributed
2. Centralized
3. Lock-based
4. Optimistic

## Name of VCS tools?
1. Git
2. Supervision(SVN)
3. Mercurial

## configure git
git --version
To configure Git, you must define some global variables: user.name and user.email. Both are required for you to make commits.
`git config --global user.name "<USER_NAME>"`
Now, use this command to create a user.email configuration variable, replacing <USER_EMAIL> with your e-mail address: git config --global user.email "<USER_EMAIL>"

Run the following command to check that your changes worked:git config --list

## Set up your Git repository
git --version
git config --global user.name "<USER_NAME>"
git config --global user.email "<USER_EMAIL>"
git config --list
mkdir Cats
cd Cats


Now, initialize your new repository and set the name of the default branch to main: git init --initial-branch=main
git init
git checkout -b main
Now, use a git status command to show the status of the working tree:git status

## Basic Git Commands
1. git status - display the state of working tree. just to check what is happening in the tree.
2. git add - to stage changes to prepare for a commit
3. git commit - As a verb, committing changes means you put a copy (of the file, directory, or other "stuff") in the repository as a new version. As a noun, a commit is the small chunk of data that gives the changes you committed a unique identity. The data that's saved in a commit includes the author's name and e-mail address, the date, comments about what you did (and why), an optional digital signature, and the unique identifier of the preceding commit.
4. **git log** - The git log command allows you to see information about previous commits.


## Introduction to Github
1. Github is a platform.
2. it's for software developer those who wants to share, contribute and help other software people project.
3. GitHub provides an AI powered developer platform to build, scale, and deliver secure software.
4. AI - The GitHub Enterprise platform is enhancing collaboration through AI-powered pull requests and issues,
productivity through Copilot, and security by automating security checks faster.
5. Collaboration - Repositories, Issues, Pull Requests, and other tools help to enable developers, project managers, operation leaders, and others at the same company. It enables them to work faster together, cut down approval times, and ship more quickly.
6. Productivity - With built-in CI/CD (Continuous Integration and Continuous Delivery) tools directly integrated into the workflow, the platform gives users the ability to set tasks and forget them, taking care of routine administration and speeding up day-to-day work. This gives your developers more time to focus on what matters most, creating innovative solutions.
7. Security - code remains private.
8. Scale

# Introduction to Repositories 
### What is a repository?
- storage location for your project's files and folders. It contains all the project-related content, including source code, documentation, and other necessary files.
- through repo i can collaborate with other people
- repo can be public or private.
## How to create a repository
using git cli
1. git init <repository-name>
2. cd <repository-name>
3. touch README.md
4. Link to the Github: git remote add origin https://github.com/username/repository-name.git
5. push code to the Github: git push -u origin main

## Adding Files to a Repository
Using git cli
- git add <file-name>
- git commit -m "Add your commit message"
- git push

## How to Search for Repositories
1. using github search
2. Explore section
3. tags

## Introduction to Gists, Wikis, and GitHub Pages
### Gists
- Gists are a way to share snippets of code or text.
- Public gists can be viewed by anyone; private gists are only accessible via a specific URL.
- Create a gist by clicking your profile picture and selecting Your gists.
## Wikis
- Wikis are collaborative spaces within a repository for documenting your project.
- Accessible via the Wiki tab in the repository.
Useful for:
- Writing project documentation.
- Collaborating on ideas and notes.

## GitHub Pages
A feature to host static websites directly from your repository.Uses the content from a branch (often gh-pages) or a folder.
Set up GitHub Pages:
- Go to Settings in your repository.
- Scroll to the Pages section.
- Choose a branch or folder to host your site.
- Customize your domain or use the default GitHub-provided URL.

