
git init            Inicializa un repositorio local de git
                    Inicializa un área de staging(preparación)

git status          Muestra el estado git con respecto al proyecto:
                        - En que rama estoy
                        - Los cambios/diferencias entre:
                          - Working directory y Staging area
                          - Staging area y último commit

git add PATHSPEC    COPIA al área de staging los archivos que se le indiquen
                    PATHSPEC:
                        git add libreria.codigo  -> Copia ese archivo a staging
                        git add *                -> Copia todos los archivos NO OCULTOS
                                                    de la carpeta actual Y SUBCARPETAS
                                                    a staging
                        git add .                -> Copia todos los archivos OCULTOS y
                                                    NO OCULTOS de la carpeta actual Y SUBCARPETAS a staging
                        git add :/               -> Copia todos los archivos OCULTOS y
                                                    NO OCULTOS de cualquier carpeta del proyecto a staging (con independencia de en que carpeta esté yo en la terminal)

git branch          Muestra las ramas del proyecto
                    En git, hasta que no hay un commit, no hay ramas.

git show            Muestra información de un commit. Si no digo cual, del ultimo

git diff            Muestra las diferencias entre distintas versiones de un 
                    fichero/carpeta/repo

                    git diff FICHERO                Working vs Staging
                    git diff --staged FICHERO       Staging vs ULTIMO COMMIT 
                    git diff COMMIT FICHERO         Working vs COMMIT
                    git diff COMMIT1 COMMIT2        Diferencias entre dos commits
Pero no pasa nada si no me acuerdo del ID del commit en el que estoy...
GIT ME REGALA UNA VARIABLE: HEAD

La variable HEAD es una variable que punta al commit en el que estoy ubicado.

    HEAD^       -> El commit anterior al que estoy                          HEAD~1
    HEAD^^      -> El commit anterior al anterior al que estoy              HEAD~2
    HEAD^^^     -> El commit anterior al anterior al anterior al que estoy  HEAD~3

    git log --oneline          Muestra los commits de la rama en la que estoy
                                con su ID y su mensaje


    git restore MODIFICADORES  -- FICHERO

    git restore --source HEAD  -- FICHERO
                                        Restaura el fichero desde el Ultimo Commit
                            --worktree
                            --staged
                            --worktree --staged
    git restore --worktree -- FICHERO
                                        Restaura el fichero desde el Staging             

    git checkout COMMITID               Viajo al pasado
                                        Mueve el HEAD a ese commit pasado
                                            OJO: Deja el repo en estado DETACHED
                                                                        DESASOCIADO
                                                 Solo es que están aquí no puedo hacer COMMITS en esta rama. Por qué?
                                                 Porque estoy en un commit que ya tiene otro detrás en esta rama

                                                 Podría hacer cambios y generar una nueva rama desde aquí con un commit y los cambios
    git checkout -                    Vuelvo al anterior que estaba


    1          HEAD
    2                       HEAD
    3 HEAD

    git checkout - ---> 1