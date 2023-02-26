# How to generate diff of Bitcoin Core and the Drivechain project

Clone drivechain-project/mainchain (default branch is master):
------------------------------------------------------------------

```git clone https://github.com/drivechain-project/mainchain```

Add upstream Bitcoin as a branch in local git repository:
---------------------------------------------------------

```git fetch https://github.com/bitcoin/bitcoin```

```git checkout -b upstream FETCH_HEAD```

Create new branch of local upstream branch based on the last commit that drivechain merged in from upstream:
------------------------------------------------------------------------------------------------------------

```git branch branchname <sha1-of-commit>```

Example Bitcoin Core commit hash: ```fe53d5f3636aed064823bc220d828c7ff08d1d52```

```git branch createDIFF fe53d5f3636aed064823bc220d828c7ff08d1d52```

Generate diff (excluding UI) between the mainchainBMM and createDIFF branch:
----------------------------------------------------------------------------

```git diff createDIFF mainchainBMM -- . ':!*.md' ':!*.txt' ':!*.am' ':!*.json' ':!*.in' ':!*.if' ':!*.ac' ':!*.png' ':!*.tiff' ':!*.ico' ':!*.py' ':!*.ts' ':!*.ui' ':!*.rc' ':!*.sh' ':!*.svg' ':!*.yml' ':!*.m4' ':!*.html' ':!*.hex' ':!*.gitignore' ':!*.includes' ':!*.include' ':!*.bash-completion' ':!*.desktop' ':!*changelog' ':!*copyright' ':!*.pgp' ':!*config' ':!*COPYING' ':!*control' ':!*rules' ':!*.conf' ':!*.openrcconf' ':!*.service' ':!*.cert' ':!*.sub' ':!*.mk' ':!*.patch' ':!*.openrc' ':!*Doxyfile' ':!*.1' ':!*.pem' ':!*.bmp' ':!*.clang-format' ':!contrib/*' ':!depends/*' ':!src/bench/*' ':!src/rpc/*' ':!src/wallet/rpc*' ':!src/qt/*' > mainchainBMM.diff```  


Generate diff (UI only) between the mainchainBMM and createDIFF branch:
-----------------------------------------------------------------------
You'll need to create 2 diffs for this to work (TODO is there a better way?)
and append both to the same file.

From ```src/rpc/```:

```git diff createDIFF mainchainBMM -- . ':!*.md' ':!*.txt' ':!*.am' ':!*.json' ':!*.in' ':!*.if' ':!*.ac' ':!*.png' ':!*.tiff' ':!*.ico' ':!*.py' ':!*.ts' ':!*.rc' ':!*.sh' ':!*.svg' ':!*.yml' ':!*.m4' ':!*.html' ':!*.hex' ':!*.gitignore' ':!*.includes' ':!*.include' ':!*.bash-completion' ':!*.desktop' ':!*changelog' ':!*copyright' ':!*.pgp' ':!*config' ':!*COPYING' ':!*control' ':!*rules' ':!*.conf' ':!*.openrcconf' ':!*.service' ':!*.cert' ':!*.sub' ':!*.mk' ':!*.patch' ':!*.openrc' ':!*Doxyfile' ':!*.1' ':!*.pem' ':!*.bmp' ':!*.clang-format' ':!contrib/*' ':!depends/*' ':!src/bench/*' >> ../../mainchainUI.diff```

From ```src/qt/```:

```git diff createDIFF mainchainBMM -- . ':!*.md' ':!*.txt' ':!*.am' ':!*.json' ':!*.in' ':!*.if' ':!*.ac' ':!*.png' ':!*.tiff' ':!*.ico' ':!*.py' ':!*.ts' ':!*.rc' ':!*.sh' ':!*.svg' ':!*.yml' ':!*.m4' ':!*.html' ':!*.hex' ':!*.gitignore' ':!*.includes' ':!*.include' ':!*.bash-completion' ':!*.desktop' ':!*changelog' ':!*copyright' ':!*.pgp' ':!*config' ':!*COPYING' ':!*control' ':!*rules' ':!*.conf' ':!*.openrcconf' ':!*.service' ':!*.cert' ':!*.sub' ':!*.mk' ':!*.patch' ':!*.openrc' ':!*Doxyfile' ':!*.1' ':!*.pem' ':!*.bmp' ':!*.clang-format' ':!contrib/*' ':!depends/*' ':!src/bench/*' >> ../../mainchainUI.diff```


Generate html from diff files:
------------------------------

Install pygmentize (```pip install Pygments```) then:

```pygmentize -f html -O full,style=trac -l diff -o mainchainBMMDIFF.html mainchainBMM.diff```
```pygmentize -f html -O full,style=trac -l diff -o mainchainUIDIFF.html mainchainUI.diff```

TODO
----

```TODO``` Consider using diff-filter to only show additions (see: https://git-scm.com/docs/git-diff 'diff-filter')

```TODO``` Add note with date and branch commit hashes to html file
