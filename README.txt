# -*-org-*-
* GIT HOOKS

The hooks can contain different implementations.
At the moment there is [[default]] and [[empty]].

[[empty]] implementation is empty. It is for selecting No hooks at all.

Which hooks implementation to use set the HOOKS environment variable.
Eg. on the command line:
#+begin_src bash
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
'branch'[@host_id]:
Where
'branch' is the name of the branch.
- If 'branch' is 'master' only m is printed (no '')
- If no branch a - is printed (no '')
- Else the branch name in '' is printed
[@host_id] "@host_id" is optional
(included if GIT_HOOKS_HOST_ID is set) [] just shows that it is
optional.
The @ is prepended to the content in GIT_HOOKS_HOST_ID.

* Usage
** Set GIT_HOOKS_ROOT
Set environment variable GIT_HOOKS_ROOT to the root of this package -
this folder.

** Optionally Set GIT_HOOKS_HOST_ID
Set environment variable GIT_HOOKS_HOST_ID if you want to include
a host ID, e.g. hostname:
#+begin_src bash
export GIT_HOOKS_HOST_ID=`hostname`
#+end_src

** Optionally disable the hooks
This is intended to be a switch to set for single commands where the
hooks is not wanted, then set the variable HOOKS=empty (or any
non-existing impl ... but more implementations might come in the
future.

#+begin_src bash
HOOKS=empty git ...
#+end_src

* Implementations
** empty
Contains no hooks - and will newer contain any hooks.

** default
*** commit-msg
The commit-msg hook implements the above functionality.

