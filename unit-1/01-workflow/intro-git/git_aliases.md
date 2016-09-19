# Git Aliases

Git aliases allow us to replace run long, complicated commands with short, simple ones. We use git a lot, so having aliases can really save you effort in the long run!

Just run the commands below to add the aliases you 
want.

## Common Commands
###`cm = commit -m`
`git config --global alias.cm "commit -m"`

###`a = add`
`git config --global alias.a add`

### `co = checkout`
`git config --global alias.co checkout`

## Fancy things
###`lg`: pretty log

![Example](http://i.imgur.com/tSgaU.jpg)
`git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"`

Replaces the ugly `git log` with a version that is shorter, more colorful and looks like a graph.

