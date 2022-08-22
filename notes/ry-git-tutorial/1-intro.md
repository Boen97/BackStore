# The Git Intro

- Git is a `version control system(VCS)`
- managing `changes` to your files

## a brief history of `revision control`

the evolution of version control systems in general

### files and folders

before the advent of revision control software, there were only files and folders
the only way to track revisions of a project was to copy the entire project and give it a new name

what happens if you mis-label a foler?
or if you overwrite the wrong file?
how would you even know that you lost an important piece of code?

### local VCS

instead of keeping old versions as independent files, these new VCSs stored them in a database.
when you needed to look at an old version, you used the VCS instead of accessing the file directly
that way, you would only have a single `checked out` copy of the project at any given time.
eliminating the possibility of mixing up or losing revisions

at this point, versioning only took place on the develper's `local computer`,
there was no way to `efficiently share code` amongest several programmers.

### centralized VCS (CVCS)

the new CVCS programs stored everything on a server.
develpers checked out files and saved them back into the project over a network
this setup let several programmers collaborate on a project by giving them a `singel point of entry`

> but how do multiple users work on the same files at the same time?

just imagine a scenario where two people fix the same bug and try to commit their updates to the central server.
whose changes should be accepted?

CVCS addressed this issue by preventing users from overriding other's work.
if two changes conflicted, someone had to manually go in and merge the differences.
this solution proved cumbersome for projects with dozens of active contributors.
development couldn't continue until all merge conflicts were resolved and made available to the entire development team.

### Distributed VCS

give every developer their own `local copy` of the entire project
now the conflict resolution problem of CVCS had a much more elegant solution.

since there is no longer a central repository, everyone could develop at their own pace,
store the updates locally, and put off merging conflicts until their convenience.

DCVS focused on efficient management of separate branches of development
which made it much eaiser to share code, merge conflicts and experiment with new ideas.

the local nature of DVCS
1. much faster, since you no longer had to perform actions over a network
2. much safer from data loss, since every user has a complete copy of the project.
