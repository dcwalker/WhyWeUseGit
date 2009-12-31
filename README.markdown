Why We (Should) Use Git
=======================

It's Fast
---------
### literally ###
* Diffs are lightning fast. (Linus can diff the linux kernel in < 1 second )
* The git protocol is optimized for network transmission of history/packages.
* Every checkout is a clone of the repo.  Meaning checkins are done locally, rather than requiring a network.
* Most operations are an order of magnitude faster than subversion or better.

### branching is fast ###
Here is the code to create a new branch:

  `
  git checkout -b <branchname>`

You can either keep that branch private on your own repo, or choose to share it with collaborators.

Also, you don't change directories when switching branches. When you checkout a different git branch, you are still in the same directory, just with a different snapshot applied.  This works similar to (but _much_ faster than) `svn switch`

### merging is fast and painless ###

When creating git, Linus Torvalds asserted that the creators of Subversion solved the wrong problem by making branching easy.  In his opinion, it was never branching that was the problem, it was _merging_.  So, in git merging has been made simple and manageable.

In git merges are:

* easy
* frequent

As a git user, merges will become second nature, and will be so easy you won't even think about them.

For example, if you want to pull down new code from a remote repository into your local branch you might do the following:

  `
  git pull
  `

As a git user you will use this command many times a day without issue.  What you may not realize is that this command is running a merge. Under the hood, git will run something like this (which you can also run maually):

  `
  git fetch origin
  git merge origin/master
  `

The first command, `fetch` will get all the snapshot from the origin branch, the second merges origin's `master` branch into your `master` branch.

It's Distributed
----------------


It's Secure
-----------