#Git Team Workflow Part 1

### Objectives
- Describe the git flow model to organize code changes and collaborate as a team
- Use branches to isolate changes tied to specific features
- Efficiently and correctly resolve merge conflicts

### Prerequisites
Please read through the following: http://rogerdudler.github.io/git-guide/
## Review Basic Git Workflow - Intro

Although you've all been using Git and GitHub for almost a month, it's still worthwhile to take a look at some of the core ideas of Git. 

#### Why Use Version Control?
When you're working on a project, you sometimes want to be able to retrace your steps, or even revert your project to a previous state.  And often (particularly in the workplace) you need a way to effectively collaborate on a single project without stepping on each others' toes. Version control tools address all of these needs.

#### Why Git?
Git, apart from being free and open source, is also in many ways a uperior system to many older version control tools (such as Subversion) because it is a "distributed" version control tool. This means that there is no centralized approval structure for making changes to the project; instead, every student who clones the repository has their own complete copy, which they can then edit and change. This makes it much easier to use when working in groups.

>In addition, Git is much better at handling branching and merging, two big topics we'll be covering today.

#### How Does Git Work?
Git works by creating ['snapshots'](https://git-scm.com/book/en/v1/Getting-Started-Git-Basics) (i.e. commits), which record the current state of a repo. Each snapshot represents the state of the project at some moment in time.

To create a new snapshot, we use `git add` to select (or "stage") a file or files that have changed since our last snapshot, and `git commit` to actually create a new snapshot which includes those changes.

## Structure of a Git Repo with Branching

#### Commits

Remember, a Git repository can be imagined as a tree of interconnected nodes, each representing a commit/snapshot. Each of these nodes refers back to one (usually) previous node, which represents the state of the repository before that commit was made.

![Git Repo with Two Commits](https://i.imgur.com/pUWMfdy.png)

Each commit also has a unique name (which allows us to identify it) and a commit message (which tells us what changes the commit makes). The names are the unintelligble strings you see above: `61d2e60...` or `e01bb26…` . These are the strings you see when you perform a `git log`.

#### Branching

We also have branches, a reference pointing to some commit in the 'tree' of our repository. In the above example, we have one branch:`master`.  New commits can only be made at the end of a branch.


![Branching, Part 1](https://i.imgur.com/OqSxDt2.png)

In the diagram above, there's another reference called `HEAD`. `HEAD` indicates the point on the repository that we're reading from. When we run **`git branch`**, new branches get added at wherever `HEAD` points. For instance, if we were to run `git branch structure` on the repo above, here's what would happen.

![Branching, Part 2](https://i.imgur.com/XeGw114.png)

In addition to specifying where new branches go, if HEAD is pointing at the end of a branch, it also means that new commits will be added to that branch. If we want to start adding commits to our new `structure` branch instead of our `master` branch, we have to move `HEAD`. This is done using the command **`git checkout`**. In particular, we want to checkout the `structure` branch, so we would run `git checkout structure`.  

We could have done all of that previously `structure branch` and switched the head to that branch all in one command with `git checkout -b structure`.

![Branching, Part 3](https://i.imgur.com/PblGpkm.png)

New commits would then be placed onto the `structure` branch:

```bash
git add .
git commit -m 'Adds a folder for holding images'
```

![Branching, Part 4](https://i.imgur.com/i1jhpYU.png)

## Merging

Take a look at the GitHub repository - new branches are created for you when you push from your local branches!  Now, you'll need a way to bring your changes to one version of the project. One way that Git allows us to do this is by __merging__ branches.

![Merging - Separate Branches](https://i.imgur.com/oIx2ou1.png)

Merging creates a **new commit on your *current* branch** (on top of existing commits) that includes all of the changes made by another branch. The syntax for doing this is `git merge some_branch`; in context of this example, you'd have to `git checkout master` first because `some_branch` is the branch that you're pulling into your master branch.

![Merging - Merged](https://i.imgur.com/C9osnhd.png)

This doesn't destroy your original branch; all those commits are still there. However, they're not carried over to the current branch, only their data is.

But wait!  GitHub has made a sweet web interface, that utilizes Pull Requests, to make this more approachable...

## Merge Conflicts and Fetch - Demo (10 mins)

Let's revisit our `master/structure` example.  What if someone got overzealous and made a change to `master` before we merged in `structure`? Well, if the change doesn't conflict with anything in `structure` - as in, we didn't edit the same files being worked on in `structure` probably nothing! 

Git tries very hard to merge automatically. Often, Git is able to combine changes that do not affect the same parts of the file. For example, if Dev1 adds some lines to the start and Dev2 adds some lines to the end, Git can combine these changes. However, sometimes there are conflicts that Git can't resolve on its own. This often happens when two commits contain changes to the same lines of code.

![Merging - Conflict](https://i.imgur.com/MlwCPN5.png)

You'll know you have a merge conflict when you see something like the following:

```
Auto-merging style.css
CONFLICT (content): Merge conflict in style.css
Automatic merge failed; fix conflicts and then commit the result.
```

And it looks a little like this when you run `git status`

```
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   style.css
```

In those cases, instead of directly merging, Git asks the user to manually resolve the conflicts. In your project files, after trying to merge, those conflicts usually look something like this:

```javascript
  <<<<<<< HEAD
//first section
  var x = 1, 
      y = 2;
  =======
//second section
  var x;
  >>>>>>> other_branch
```

The first section is the version that exists on the current branch; the second section is the version that exists on the branch you're trying to pull in. Figure out which version of the code makes the most sense moving forward, delete the version that doesn't and all the extra stuff that Git adds (`<<<<<<<`, `=======`, etc.) and run `git commit` to finalize the merge.

For example, if we decided we only needed `var x`, delete the other "stuff":

```javascript
  var x;
```

Now, we have only the code we need. We need to `git add` the amended files and then create the merge commit using `git commit`.  

>If, for whatever reason, you hit a merge conflict, Git and GitHub are _super_ helpful in helping you resolve your conflicts.

## Conclusion

- Describe why branching is important in a team workflow.
- Identify the syntax needed to create a new branch. How about creating a new branch and switching to it?
- Why should you never work on the same files on different branches?




### Lab

[Git Merging Exercise](https://github.com/glencbz/git-merging)


## Extra Readings

* [Using branches](https://www.atlassian.com/git/tutorials/using-branches)
* [Git workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)
* [Merging vs Rebasing  ('Conceptual Overview' section)](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
* [A Git branching model in the wild](http://nvie.com/posts/a-successful-git-branching-model/)
