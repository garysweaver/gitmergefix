gitmergefix
=====

Fixes simple but volumnous git merge conflicts easily via a ruby script that can be run at command-line in *nix.

This is not a replacement for git mergetool or other more complex merge conflict resolution tools, but may do better than those tools when you have a lot of the same conflicts.

Backup your repo and all other files before using; Use at your own risk.

### Requirements

Requires Ruby and *nix. To see whether you have ruby installed, try:

    ruby -v

### Setup

If needed, make it executable:

    chmod +x gitmergefix

### Usage

#### List

Put the directory containing the gitmergefix script on your path, and then do:

    gitmergefix list

That should list files with git conflicts in the current git repo (it runs `git diff --name-only --diff-filter=U`). 

#### Resolve

To git add conflicted files that don't contain '<<<<<<< HEAD':

    gitmergefix resolve

#### Replace

Lets say you have the following conflict in some or all of your files:

    <<<<<<< HEAD
      <version>1.2.3-SNAPSHOT</version>
    =======
      <version>1.2.4-SNAPSHOT</version>
    >>>>>>> some_branch

And you'd like to replace these with:

      <version>something_else</version>

And finally you'd like to git add all files that no longer have conflicts.

To do this just use:

    gitmergefix "some_branch" "  <version>1.2.3-SNAPSHOT</version>" "  <version>1.2.4-SNAPSHOT</version>" "  <version>something_else</version>"

Notice the white space. Really what this does is to exactly replace merge conflicts that are a result of the exact two lines you specify with the line you specify, and if there that file or any other file is marked as having a conflict but doesn't, then it does a `git add` on those files.

### License

Copyright (c) 2013 Gary S. Weaver, released under the [MIT license][lic].

[lic]: http://github.com/garysweaver/gitmergetool/blob/master/LICENSE