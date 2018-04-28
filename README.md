# How to generate diff of Bitcoin Core and the Drivechain project

Clone drivechain-project/bitcoin (default branch is mainchainBMM):
------------------------------------------------------------------

```git clone https://github.com/drivechain-project/bitcoin```

Add upstream Bitcoin as a branch in local git repository:
---------------------------------------------------------

```git fetch https://github.com/bitcoin/bitcoin```

```git checkout -b upstream FETCH_HEAD```

Create new branch of local upstream branch based on the last commit that drivechain merged in from upstream:
------------------------------------------------------------------------------------------------------------

```git branch branchname <sha1-of-commit>```

Example Bitcoin Core commit hash: ```fe53d5f3636aed064823bc220d828c7ff08d1d52```

```git branch createDIFF fe53d5f3636aed064823bc220d828c7ff08d1d52```

Generate diff between the mainchainBMM branch, and the upstreamcommit branch:
-----------------------------------------------------------------------------

```git diff createDIFF mainchainBMM -- . ':!*.md' ':!*.txt' ':!*.am' ':!*.json' ':!*.in' ':!*.if' ':!*.ac' ':!*.png' ':!*.tiff' ':!*.ico' ':!*.py' ':!*.ts' ':!*.ui' ':!*.rc' ':!*.sh' ':!*.svg' ':!*.yml' ':!*.m4' ':!*.html' ':!*.hex' ':!*.gitignore' ':!*.includes' ':!*.include' ':!*.bash-completion' ':!*.desktop' ':!*changelog' ':!*copyright' ':!*.pgp' ':!*config' ':!*COPYING' ':!*control' ':!*rules' ':!*.conf' ':!*.openrcconf' ':!*.service' ':!*.cert' ':!*.sub' ':!*.mk' ':!*.patch' ':!*.openrc' ':!*Doxyfile' ':!*.1' ':!*.pem' ':!*.bmp' ':!*.clang-format' ':!contrib/*' ':!depends/*' ':!src/bench/*' > mainchainBMM.diff```  

Generate html from diff
-----------------------

Install pygmentize (```pip install Pygments```) then:

```pygmentize -f html -O full,style=trac -l diff -o mainchainBMMDIFF.html mainchainBMM.diff```

TODO
----

```TODO``` Consider using diff-filter to only show additions (see: https://git-scm.com/docs/git-diff 'diff-filter')

```TODO``` Add note with date and branch commit hashes to html file
