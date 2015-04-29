# -*-org-*-
#+TITLE: SLBS @@html:<br>@@Git Template

* SLBS Git Template
This is an alternative git template folder, actually it only contains
special hooks, but might change in the future.

* GIT HOOKS

The hooks can contain different implementations.
At the moment there is [[default]] and [[empty]].

[[empty]] implementation is empty. It is for selecting No hooks at all.

Which hooks implementation to use set the HOOKS environment variable.
Eg. on the command line:
#+begin_src sh
HOOKS=empty git ...
#+end_src

** The behavior for impl/[[default]]

Those git hooks are for prefix first line with a commit message with
the branch that the commit is made on.

Further an optional ID for the host the commit is created on can be
included.

Add hostId (optional) and branch to the beginning of the first line of
commit messages.

The id have this form:
='branch'[@host_id]:=
Where
'branch' is the name of the branch.
- If 'branch' is 'master' only m is printed (no '')
- If no branch a - is printed (no '')
- Else the branch name in '' is printed
=[@host_id]= "=@host_id=" is optional
(included if =GIT_HOOKS_HOST_ID= is set) [] just shows that it is
optional.
The @ is prepended to the content in =GIT_HOOKS_HOST_ID=.

** Usage
*** Set =GIT_HOOKS_ROOT=
Set environment variable =GIT_HOOKS_ROOT= to the root of this package -
this folder.

*** Optionally Set =GIT_HOOKS_HOST_ID=
Set environment variable =GIT_HOOKS_HOST_ID= if you want to include
a host ID, e.g. hostname:
#+begin_src sh
export GIT_HOOKS_HOST_ID=`hostname`
#+end_src

*** Use the hooks for new git repositories
Add the following code to ~/.gitconfig:
#+begin_src conf
[init]
     templatedir = /path/to/slbs-git-template/template
#+end_src

Note: The templates does not include a description file, like normal
templates does, this is to prevent overwriting repository description
files during git init on existing repository.

The default content for =.git/description= is:

#+begin_src
Unnamed repository; edit this file 'description' to name the repository.
#+end_src

*** Use the hooks for existing git repositories
- Do the steps in [[Use the hooks for new git repositories]].
- Run git init in each git repository you want to use those hooks.
- Note existing files will not be deleted, but overwritten, e.g. the

*** Optionally disable the hooks (for single commands)
This is intended to be a switch to set for single commands where the
hooks is not wanted, then set the variable =HOOKS=empty= (or any
non-existing impl ... but more implementations might come in the
future.

#+begin_src sh
HOOKS=empty git ...
#+end_src

** Implementations
*** empty
Contains no hooks - and will newer contain any hooks.

*** default
**** commit-msg
The commit-msg hook implements the above functionality.
