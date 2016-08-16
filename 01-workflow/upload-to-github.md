# How to Upload Code to GitHub

## Create A New Repo on GitHub
Go to http://github.com and create a new repository. Name it
whatever you like. Configure it to be Public and do not choose
to initialize the project with a README.

Click `Create repository`.

![]

## Creating a new repo once

```
git init
git remote add origin COPY_YOUR_OWN_URL
```

## Making changes to a repo

- tell git what files to watch
- commit the changes
- upload the changes

```
git add -A
git commit -m "changed color of links with CSS"
git push -u origin master
```
