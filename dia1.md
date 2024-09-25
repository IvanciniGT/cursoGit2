
# Qué es Git?

SCM: Sistema de control de código fuente

Linus lo creo para poder acometer el desarrollo de Linux (2005)
Notas de lanzamiento del proyecto, Linus metió un comentario:
- Cuando no sepamos qué decisión tomar con respecto a una funcionalidad... HAREMOS LO CONTRARIO QUE CVS.

## SCM?

- Llevar un control de los cambios
- Juntar código de varias personas
- Restaurar el proyecto / partes a estados previos
- Gestionar RAMAS <--- CLAVE

Al final en un SCM, acabamos generando un REPOSITORIO... que es una especie de BBDD donde acumulamos las versiones de nuestro proyetco + metadatos.

## COMMIT

En CVS y SVN un commit era un paquete de cambios:
- En el fichero a, hemos cambiado las lineas 17 y 19
- En el fichero b, hemos añadido una función en la línea 23
- Hemos quitado el fichero c

En git un commit es una foto completa de TODO el proyecto en un momento dado. COMPLETA! TODO !
OTRA VEZ ! guardadito dentro!
Como si le doy a la carpeta del proyecto con botón derecho y hago -> Comprimir a un ZIP

Ésto es lo que hace que git VAYA TAN RAPIDO (y puede parecer contradictorio)
Cuando es necesario calcular las diferencias / los cambios entre archivos, esa operación se realiza bajo demanda.

Un Commit siempre está asociado al menos a otro commit anterior. Tenemos una progresión de commits:
    C1 -> C2 -> C3 -> C4 -> C5
    Un commit = Backup

    En qué se diferencia GIT de un sistema de Backups? RAMAS !

## RAMA?

Una rama es una linea paralelas en el tiempo (a otras) de evolución de mi proyecto.

## Los tres árboles de GIT

Git controla 3 tipos de cosas diferentes:
- La carpeta de mi proyecto (Working Directory)             C:\miproyecto
        v ^ 
- Área de staging (preparación)                             PENSAD EN EL AREA DE STAGING COMO UNA CARPETA
                                                            PARALELA a la de mi proyecto. No la vaís a ver... pero está ahí.
        v ^
- Repositorio:                                              BBDD de commits... organizados en RAMAS

# Repositorios en GIT

Otra gran diferencia de GIT con respecto a CVS o Subversion es en la forma en la que gestionan los repositorios.
SVN y CVS guardan el repositorio en un servidor central.
En cambio GIT es un sistema de control distribuido > Cada usuario tiene un repositorio en su sistema
TOTALMENTE DIFERENTE AL DEL RESTO DE PARTICIPANTES

No tendría una vista global del proyecto SIN UNIR LOS REPOSITORIOS DE TODO EL MUNDO.

ESOS REPOS NO SON IGUALES.. NUNCA LO SERÁN Y NO DEBEN SERLO ADEMAS !

## FLUJO BASICO DE TRABAJO EN GIT EN LOCAL CON UNA RAMA
    
    git init y estoy en una rama

    Tengo unos archivos en mi carpeta
        git add -> Los paso al área de staging
    Tengo los archivos en el área de Staging (COPIADOS), REPLICADOS     COPY!!
        git commit -> Los paso al repositorio
            Mete en un ZIP (más o menos) los archivos del área de staging.
            Y guarda ese zip(COMMIT) en el repositorio.
            Y que hace con el área de staging después? NADA ! Se queda igual, con todo lo que tiene.

        Y la duda viene de cuando ejecutáis un git status: Mi proyecto esá limpio y que no hay nada para commitear.

        El problema gordo es entender qué hace git status!

        GIT no se aprende apretando botones en una herramienta.
        Es más, las herramientas gráficas no me permiten hacer ni un 30% de lo que se puede hacer con git.

## Empiezo un proyecto
    1. Creo una carpeta en mi máquina: c:\miproyecto
    2. Ejecuto un git init: -> Se crea un nuevo repositorio para ir guardando mis ramas + Commits
                               Se crea un área de staging 
                               TANTO REPO como AREA DE STAGING se guardan dentro de una carpeta oculta en
                               la carpeta de mi proyecto `.git`

    c:\miproyecto                   (en algún sitio dentro de .git)
    WORKING DIR                     AREA DE STAGING                 REPOSITORIO

    Archivo1(v4)    - git add ->    Archivo1(v3)   - git commit ->  C1[Archivo1(v1)]
    Archivo2(v1)                    Archivo2(v1)                    C2[Archivo1(v1)+Archivo2(v1)]
                                                                    C3[Archivo1(v2)+Archivo2(v1)]

4 versiones del Archivo1:
    v1: C1 y C2 del Repo
    v2: C3 del repo
    v3: Staging
    v4: Working dir

    Y ahora podría empezar a pedirle a git que:
    - Quiero que me restaures la versión del archivo1 que tengo en el C2
    - Quiero que compares la version que tengo del archivo1 en Staging y en el C1

# Ahora, ya no quiero trabajar SOLO... es muy aburrido :(
    

                                   RAMA1 C1, C2, C3, C4M         (1)
                                   REPO < git init --bare
                                    |
                            Servidor de alojamiento de repos remotos: Github, Gitlab, BitBucket
                                    |
    +-------------------------------+-------------------------------+------- red (de comunicaciones)
    |                                                               |
    IvanPC                                                          MenchuPC
    |                                                               |
    c:\miproyecto                                                   c:\menchuproyecto
      REPO IVAN                                                       REPO MENCHU
      RAMA1          C1, C2, C3, C4M                                  origin/RAMA1 C1, C2, C3, C4M    (1)
        v                                                               v
      miremoto/RAMA1 C1, C2, C3, C4M (1)                              RAMA1        C1, C2, C3, C4M
                                                                        v C3
                                                                      Staging
                                                                      Working directory c:\menchuproyecto
                                                                      RAMA MENCHU  C1, C2, C3, C4M

1º Configurar en mi máquina una asociación entre MI REPO LOCAL y el REPO REMOTO
(de hecho podría tener 25 repos remotos asociados a mi repo local)
A ese repo remoto concreto que tengo ahí le doy un nombre: MIREMOTO

Y ahora copio UNA RAMA DE MI REPO LOCAL a REPO REMOTO <<< ESO ES LO QUE SE HACE EN GIT
En realidad, GIT duplica mi RAMA en mi REPO LOCAL, creando una nueva rama, que llamara como mi rama, 
    pero añadiéndole el prefijo del remoto

Cómo se llama esa operación de duplicar una rama mia, para vinculación en un remoto: git push --set-upstream
                                                                                     git push -u


Al hacer un clonado de un repo: git clone, lo primero que hace git es vincular un nuevo REPO local 
con un REPO REMOTO... al que da un nombre: origin (por defecto... lo puedo cambiar si quiero)

# Para que Menchu pase su C4M a la Rama 1
Lo que necesita hacer es una operación de FUSION DE CAMBIOS:
- merge: 
  - fast-forward
  - merge recursivo
  - merge OCTOPUS
- rebase (GUAY !!!! LOS ADORAMOS !!!! MERGE = CACA)
                                      REBASE = GUAY !!! 

git pull = git fetch + [ git rebase | git merge ]

---

> EJEMPLO LOCAL

                            ------------En seguimiento----------------
WORKING DIR                  STAGING                     REPO
libreria.codigo(3)           libreria.codigo(3)          C1[libreria.codigo(1)]  HEAD 
                                                         C2[libreria.codigo(2)]  
                                                         C3[libreria.codigo(3)] 



ID de un commit? ES UN HASH del empaquetado
    Una huella. Si alguien tocase algún archivo por detrás, fallaría al comprobar la huella y me avisaría de corrupción de datos.

---

CUIDADO con un comando llamado git checkout:
- cambia de ramas           git switch 
- Viaja al pasado           git checkout
- Restaura archivos         git restore
- Crear ramas               git switch -c

ESTE COMANDO, hoy en día CASI TODOS SUS USOS ESTÁN DEPRECATED

---