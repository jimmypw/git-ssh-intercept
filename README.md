git-ssh-intercept
=================

git-ssh-intercept is a piece of software that will intercept requests
over ssh to access a git repositry and prefix a path on to the initial
request so that it reflects the same kind of path structure that 
bitbucket utilises. For example.

normal:
  ``git@git:repo.git``

in notmal situations the above repository will reference a repository
in the home directory for a user. 

bitbucket:
  ``git@git:/group/repo.git``

In bitbucket this becomes an issue because of the repository urls's 
that are provided will be absolute paths, relative to root.

This is a problem as in our situation we have a requirement to mirror
a bitbucket server so that the repository path is reliably replicated.
This is not easy to accomplish using jails and other fancy tricks so
instead I wrote a command that can be used with SSH in order to 
rewrite paths before the git software is run.

using this software you can use a git url like:
  ``git@git:/group/repo.git``

and reference a repo on fisk called:
  ``/home/git/gitrepos/group/repo.git``

There is also the ability to do some basic permissions cheching to allow
the user to write to a repo or not depending on the SSH key that was
used to connect to the git server. In instances when the SSH key is use
access to a shell over SSH is actively denied.


Install
-------

1. Download the code in a sensible location.
1. Ensure script has the execute bit set.
1. Add the command to either an existing SSH key or a new key.
  ``command="/usr/local/bin/git-ssh-intercept" ssh-rsa AAAAB3NzaC1yc2EAAA....``
1. If so desired you can add 'rw' to the options so that the user is allowd
to write too the repository. eg:
  ``command="/usr/local/bin/git-ssh-intercept rw" ssh-rsa AAAAB3NzaC1yc2EAAA....``

