gitmergefix
=====

Fixes a certain kind of git merge conflict easily via a ruby script that can be run at command-line.

### Requirements

Requires Ruby and *nix. To see whether you have ruby installed, try:

    ruby -v

### Usage

Put the directory containing the gitmergefix script on your path, and then do:

    gitmergefix

That should show a line indicating usage followed by all of the files with git conflicts in the current git repo. If it doesn't make it executable:

    chmod +x gitmergefix

Lets say you have the following conflicts in all of your files:

    <<<<<<< HEAD
      <version>1.2.3-SNAPSHOT</version>
    =======
      <version>1.2.4-SNAPSHOT</version>
    >>>>>>> some_branch

And you'd like to replace these with:

      <version>something_else</version>

and then git add that file if all conflicts are resolved.

To do this just use:

    gitmergefix "some_branch" "  <version>1.2.3-SNAPSHOT</version>" "  <version>1.2.4-SNAPSHOT</version>" "  <version>something_else</version>"

Notice the white space. Really what this does is to exactly replace merge conflicts that are a result of the exact two lines you specify with the line you specify, and if there that file or any other file is marked as having a conflict but doesn't, then it does a `git add` on those files.

That is all it does, but it may save you some time vs. using mergetool or having to construct a regex.

### License

Copyright (c) 2013 Gary S. Weaver, released under the [MIT license][lic].

[lic]: http://github.com/garysweaver/gitmergetool/blob/master/LICENSE