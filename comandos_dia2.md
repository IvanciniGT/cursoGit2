 517  git status
  518  git status
  519  git diff libreria.codigo
  520  clear
  521  git diff libreria.codigo
  522  git diff --staged libreria.codigo
  523  git diff libreria.codigo HEAD
  524  git diff HEAD libreria.codigo
  525  git log --oneline
  526  git branch
  527  git commit -m 'Operacion suma'
  528  git status
  529  git add .
  530  git commit -m 'Operacion resta'
  531  git status
  532  git status
  533  git log --oneline
  534  git diff bb78d3a libreria.codigo
  535  git log --oneline
  536  git diff HEAD^^^ libreria.codigo
  537  git diff HEAD^^ libreria.codigo
  538  git diff HEAD~2 libreria.codigo
  539  git diff HEAD~2 HEAD
  540  clear
  541  git status
  542  git rm libreria.codigo 
  543  git status
  544  git restore --help
  545  clear
  546  git restore --from HEAD --worktree -- libreria.codigo
  547  git restore --source HEAD --worktree -- libreria.codigo
  548  git status
  549  git restore --source HEAD --worktree --staged -- libreria.codigo
  550  git status
  551  git log --oneline
  552  git checkout HEAD^^
  553  git log --oneline
  554  git log --oneline -a
  555  git log --oneline --all
  556  git checkout -
  557  cd ..
  558  git init
  559  git add :/
  560  git commit -m 'alta'
  561  git remote add origin https://github.com/IvanciniGT/cursoGit2.git
  562  git push -u origin master
  563  git add :/
  564  git commit -m 'alta'
  565  git push -u origin master
  566  clear
  567   cd local/
  568  clear
  569  git log --oneline
  570  git switch -c dev
  571  git switch -c multiplicar
  572  git switch -c dividir
  573  git branch
  574  git log --oneline
  575  git switch multiplicar
  576  git switch dividir
  577  git switch multiplicar
  578  git add .
  579  git switch dividir
  580  git switch multiplicar
  581  git commit -m 'multiplicacion hastiado'
  582  git switch dividir
  583  git switch master
  584  git switch dev
  585  git switch dividir
  586  git switch multiplicar
  587  git switch dividir
  588  git commit -m 'division'
  589  git commit -am 'division'
  590  git switch multiplicar
  591  git log --oneline --graph -a
  592  git log --oneline --graph --all
  593  git status
  594  git add .
  595  git commit -m 'multiplicacion'
  596  git log --oneline --graph --all
  597  git reset HEAD^
  598  clear
  599  git log --oneline --graph --all
  600  git commit --amend 'multiplicar' # Reescribe el ultimo commit
  601  git commit --amend -m 'multiplicar' # Reescribe el ultimo commit
  602  git log --oneline --graph --all
  603  git commit --amend -m 'Operacion multiplicación'
  604  git log --oneline --graph --all
  605  git switch dev
  606  git status
  607  git commit -a --amend -m 'Operacion multiplicación'
  608  git switch dev
  609  clear
  610  git log --oneline --graph --all
  611  git merge multiplicacion --ff-only
  612  git merge multiplicar --ff-only
  613  git log --oneline --graph --all
  614  git reset --hard HEAD^
  615  clea
  616  clear
  617  git log --oneline --graph --all
  618  git switch multiplicar 
  619  git merge dev
  620  git switch dev 
  621  git merge multiplicar --ff-only
  622  git log --oneline --graph --all
  623  git merge division
  624  git switch dividir 
  625  git merge dev --ff-only
  626  git merge -m 'npi algo de juntar la div y multi'
  627  git merge dev -m 'npi algo de juntar la div y multi'
  628  git commit -am 'npi de juntar lo de multiplicar y dividir'
  629  git log --oneline --graph --all
  630  git switch dev
  631  git merge dividir --ff-only 
  632  git log --oneline --graph --all
  633  git reset HEAD^^
  634  git log --oneline --graph --all
  635  git switch dividir
  636  git status
  637  git restore libreria.codigo
  638  git switch dividir 
  639  clear
  640  git reset --hard HEAD^
  641  clear
  642  git log --oneline --graph --all
  643  git switch multiplicar 
  644  git merge dev
  645  git switch dev
  646  git merge multiplicar --ff-only 
  647  git log --oneline --graph --all
  648  git switch dividir 
  649  git rebase dev
  650  git add .
  651  git rebase --continue
  652  git log --oneline --graph --all
  653  git switch dev
  654  git merge dividir --ff-only
  655  git log --oneline --graph --all
  656  git diff HEAD HEAD^
  657  git diff HEAD HEAD^^
  658  git diff HEAD HEAD^^^
  659  git log --oneline --graph --all
  660  git revert HEAD
  661  git log --oneline --graph --all
  662  git cherry-pick 03dd5f6
  663  git log --oneline --graph --all
  664  git reset --hard HEAD^^
  665  git log --oneline --graph --all