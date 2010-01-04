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

    git checkout -b <branchname>
  

You can either keep that branch private on your own repo, or choose to share it with collaborators.

Also, you don't change directories when switching branches. When you checkout a different git branch, you are still in the same directory, just with a different snapshot applied.  This works similar to (but _much_ faster than) `svn switch`

Why is it so fast? Because a branch in subversion is complete copy of all the code, in git it's a complete copy of all the differences.  Git manages the differences between the revisions and the branches it doesn't make new copies of the files when you branch like subversion does.  This means switching branches is as fast as applying a patch, not downloading a new file from a remote server.

### merging is fast and painless ###

When creating git, Linus Torvalds asserted that the creators of Subversion solved the wrong problem by making branching easy.  In his opinion, it was never branching that was the problem, it was _merging_.  So, in git merging has been made simple and manageable.

In git merges are:

* easy
* frequent

As a git user, merges will become second nature, and will be so easy you won't even think about them.

For example, if you want to pull down new code from a remote repository into your local branch you might do the following:

    git pull

As a git user you will use this command many times a day without issue.  What you may not realize is that this command is running a merge. Under the hood, git will run something like this (which you can also run maually):

    git fetch origin
    git merge origin/master

The first command, `fetch` will get all the snapshot from the origin branch, the second merges origin's `master` branch into your `master` branch.

### Why is merging easier? ###

You know where the branch came from!  Ever tried to figure out where a branch cuts off from trunk in subversion?  This information what be very useful when merging or even reviewing a large change set but is aggravatingly difficult to figure out in subversion.

Don't merge code that's already merged!  When you merge a branch, git knows what has already been merged so it only merges what's new.  Here's an example of why this is so powerful:

  Say you have your trunk and a dev branch.  Trunk is the code you have in production and you add a feature that takes 5 commits to complete (not hard to do when you commit early and often).  You merge dev back into trunk after revision 5 then continue work on the next feature.  Meanwhile another developer discovers a bug in the first feature.  It's an easy fix so they implement it in revision 6 by removing the bogus line of code.  Now you've completed feature 2 and it again takes a few commits.  You want to merge this new feature to the trunk so it can go to production but you don't remember when you last merged.  You have two choices, you can hunt through the logs and sort out where you last merged or you can merge the whole thing.  What if others were committing too?  You have to sort out all their commits as well.  If you just merge the whole branch back you'll re-implement the broken code that your co-worker already fixed (Ah! Regression!).

Git makes the above scenario simple by making the merge simple.  It knows where you last merged and where your branch came from thus keeping you from overwriting other people's work.

### For the record ###

When merging code in subversion, all the new content shows up in the history as being authored by the user that merged it.  Git tracks both the user that merged it (in the log) and the developer who wrote the code (in the "blame").  So when code is reviewed by a peer and merged into the stable codebase the log correctly shows that user 1 wrote the code and user 2 merged it.


It's Distributed
----------------


It's Secure
-----------


Benefits
--------

* You pull code to you instead of code being pushed on you.
* You can check in various save points locally without being required to merge other people's work ("hassle free early and often").
** If you're not ready to merge but want to keep save points for your own sanity, you can.

### Context switching is easy ###

When you're in the middle of feature development and an urgent production support request comes in, you can easily stash your work for later and dive right in to a clean version of the code.

  ex: stash the code on your dev branch and switch to production support mode
      git stash
        save all your uncommited work in tmp space for later
      git checkout master
        switch to your clean branch (a mirror of production)
      git checkout -b support
        create and switch to a new branch called "support" which contains a clean copy from master
      Get to work!
      
When you're done solving the world's production support issues you're two commands away from being right back where you left off:
      git checkout dev
      git stash pop
