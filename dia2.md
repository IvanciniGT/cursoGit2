
- Aprendimos conceptos básicos:
  - REPO / RAMA / COMMIT
  - 3 arboles de git: WORKING DIR / STAGING / REPO
  - Intro a los repos remotos
- Flujo básico de trabajo con git en local
    init
    add
    commit
    show
    log
    diff
    restore (que aún no han sido commiteados)
    checkout
- Controlar el historial
  - Asegurarme que no genero commits que no aportan. 1 COMMIT = 1 FUNCIONALIDAD. REGLA DE ORO !
    amend 

        C1 ( está funcionando el R17... aleluya!!!)
        C1.5 Que ahora también el 18
        C2... Mierda que no... que me ha fallao algo en el R17... Pero ahora si que si
        C3... Cago en diez.... pues pensaba que si... pero resulta no... ero ahora si que que si de verdad de la buena...
        ...

  - Y a veces los generaré (LOS VOY A GENERAR SEGURO). No pasa nada... pero luego los limpio
    reset 
        soft
        mixed
        hard
    rebase interactivo 
        squash
        fixup
        pick
        ... y otros 10
- Aprender a trabajar con ramas
    Y cuidado... esto no es aprender:
        git switch
        git branch
        git merge
        git rebase
    NOnonono. Eso es el 20%. Es entender el concepto de workflow.
    El aprender a definir un workflow de trabajo con ramas
    El aprender a forzar un workflow de trabajo con ramas  HOOKS
- Aprender a trabajar con remotos
- Aprender a trabajar con submódulos
- Aprender a trabajar con stash
- Aprender a trabajar con tags
- Aprender a trabajar con hooks

---

# WORKFLOWS (GITFLOW, GITHUB FLOW, GITLAB FLOW)

master - main                                                                   //  PRODUCCION
    
    REGLA DE ORO: NUNCA se hace un commit en master
    Qué contiene esta rama? Código listo para producción

    Pero entonces... si no puedo hacer ahi commit.. como llegan aquí los commits? DESDE OTRAS RAMAS !

develop - desarrollo - dev                                                      // ENTORNO DESARROLLO

    Lo que he desarrollado y ya está probado de forma UNITARIA / INTEGRACION

release                                                                        //  PREPRODUCCION / PRUEBAS

    Donde hago las pruebas de SISTEMA
    
                                    -- hotfix1   C5 -> CHF1 (Se libera a producción)
                                                /
                                  ---main      C5
                                              /          Si permito commit habitualmente es para integrar. Decidir qué va a prod
                            ---release C4 -> C5      C7  (Y esto tengo que plantearme si lo permito?) 
                                       /            /    Si soy conservador NI DE COÑA. Si soy práctico, 
                                      /            /     BUENO... Pero apechuga.
    --- develop -> C1 -> C2 -> C3 -> C4 -> C6 -> C7 -> C7-HF1


    En git un commit no es un cambio,.. y para hacer algo como llevarme el CAMBIO realizado en el HF1 al C7, lo primero que necesito es IDENTIFICAR el cambio: calcular el PATCH: git diff CHF1 C5 -> Diferencias = PATCH = CAMBIO  \
    Y esas diferencias, las quiero aplicar sobre el C7  -> git apply PATCH                      / git cherry-pick CHF1

COMO SE COPIAN COMMITS A OTRAS RAMAS?       MERGE DE TIPO FAST FORWARD: Copiar un commit a otra rama.
En main, solo se deben permitir merges de tipo ff ( Por cierto... en un merge de tipo ff... si solo copio un commit a otra rama
    hay posibilidad de conflicto? NO... Machaco el commit de la rama destino con el de la rama origen... no lo fusiono)
En release se deben permitir merges de tipo ff? IGUAL... a priori SOLO de tipo ff... y en esta rama no hay posibilidad de conflicto
A priori git, si intento hacer un merge de tipo ff y ha habido cambios en la rama, no me deja... GIT NUNCA deja hacer nada que sea destructivo. A NO SER QUE SE LO SUPLIQUE... entonces si.. PERO SE LO TENGO QUE SUPLICAR. Y rama release y main, van asi.

Y en develop? SOLO fast-forward... y ni suplicándolo debería permitir aquí otra cosa
Por qué? Mientras haya un conflicto, nadie puede trabajar con la rama. Quien cojones se ha creido alguien para venir a joder la rama donde trabaja todo el mundo.

En proyectos sencillos, si podemos usar la rama develop. Y no pasa nada. Y puede ser que alguien genere conflicto.. bueno... EN SU LOCAL!

En proyectos más grandes, no vale esta forma de trabajo. Y lo primero abrimos ramas por feature: Un requisito o paquete de Requisitos

    ------ develop --...- C5 -> C6 -------------C8-----------C11
                                 \           ff / \         / ff
                                  \            /   \       /
                               R1-C6 -> C7 -> C8    \     /
                                    \                \ r /
                                 R2-C6 -> C9 -> C10 -> C11   Es mi responsabilidad hacer que mi código se integre con el resto
                                      \
                                    R3-C6 -> C11 -> ...
R1, R2, R3



                                                                main  ---  suma, resta, valor absoluto
                                                                            /
                                    release  --- valor absoluto -> quito multiplicar
                                                    /
--- develop -> suma -> resta -> multiplicar -> valor absoluto

Antes de subir de una rama release a la rama develop, necesitaría asegurarme que:
- Tengo en mi rama los últimos cambios de la rama develop.
- Que MI código funciona:
  - Por si solo               Pruebas unitarias. Si no se superan: NO HAY PARTY !!!! No sube a develop
  - Integrado con lo demás    Pruebas de integración. Si no se superan: NO HAY PARTY !!!! No sube a develop

Si dejo a la buena voluntad de mis desarrolladores el validar esto, que ocurrirá? Voy a acabar con un desmadre!
Y por eso tendemos a proteger ramas.. ese es un mínimo.
Yo a hacer que a la rama dev solo pueda subir JENKINS, como parte de un pipeline donde antes se ha forzado la ejecución de pruebas unitarias y de integración... y si no pasan no sube a dev.
Y digo... pues sabes que... hago 4 pruebas de mierda y engaño al Jenkins... y subo a dev... Y es verdad que puedes hacer esto...
Pero al Sonar No le engañas... Que te va a mirar la cobertura de código... es decir, el porcentaje de código que está siendo ejecutado al ejecutarse las pruebas... Y si no llega a un mínimo 80-90%... NO SUBE A DEV.


## MERGES

- Fast Forward (ff) No hay fusión... hay reemplazo 
- Recursive (3-way) Hay fusión. puede haber conflicto

## FUSIONES DE CAMBIOS
                                                        ¿Qué me interesa reflejar en el historial?
- Recursive (3-way) Hay fusión. puede haber conflicto       Contar la verdad haciendo el historial más complicado
- Rebase                                                    Mentir para hacerlo más sencillo (el historial)

REBASE MIENTE. No refleja la realidad de lo que ha acontecido. Pero a veces la realidad no me interesa.
                De hecho NO SUELE INTERESARME.


# MERGE El merge refleja la fusión.Y no siempre me interesa. En alguno momento si.

    develop -> suma -> resta ------------> multiplicacion ------> integracion mul-div
                          \             / ff        \           /
        R1 -------------- resta -> multiplicacion    \         /
                              \                       \ merge /
        R2 ------------------- resta --> division -> integracion mul-div

    Miro el historial en develop:
        - suma
        - resta
        - multiplicacion
        - division
        - integracion mul-div   ¿Qué cojones significa esto?     

    Este es el historial del proyecto. Es real? Es lo que ocurrió? SI. Ahora bien...

# REBASE = CAMBIO DE BASE

Más peligroso, porque implica REESCRIBIR COMMITS DEL HISTORIAL ! Voy a mentir!

    develop -> suma -> resta ------------> multiplicacion
                          \             / ff             
        R1 -------------- resta -> multiplicacion        
                                          \                
                  R2 -------------- multiplicacion -> division' -> valor absoluto'

    Y si miro el historial en develop:
        - suma
        - resta
        - multiplicacion
        - division'

                            suma  -->  resta -->  Multiplicacion -->  division'
                             dev        dev          dev                dev
                             R1         R1           R1                 R2
                             R2         R2           R2

    En rebase tendré exactamente los mismo conflictos que en merge. IGUAL. De hecho un poco peor si me despisto.
    Lo puedo usar CON TRANQUILIDAD en ramas que no publico! 
    Pero en ramas que publico, siempre el rebase antes del push. Siempre. Siempre. Siempre.

    CUIDADO: Un conflicto no es algo malo. No es un error ni nada.
        2 compañeros hemos tocado la misma función del código. Habrá que decidir.. o juntar .. o lo que sea
        Qué probabilidad hay de que 2 compañeros toquen la misma linea en un proyecto?
            DEPENDE:
            - De la mierda de código que estemos haciendo. 
              - Si tengo un código guay, con complnentes DESACOPLADOS, MUY BAJA.. así haya 65 tios en el proyecto o tías.
              - Si mi código es una mierda... MUCHA ! Y si hay 65 tios en el proyecto... MUCHISIMA MÁS!

    Esto refleja la realidad de lo que pasó? NO... Me importa? NO... Por qué? Porque no me interesa. 
            Me interesa que el historial refleje los CAMBIOS que se han ido haciendo.

    Si me espero mucho a hacer rebase... como me lleguen conflictos Y YO tenga muchos commits, los tengo que arreglar en todos.
    Pues vaya coñazo! SOLUCION?
        Antes de hacer un commit en una rama donde quiero trabajar con rebases, hago un rebase de la rama padre.
        Por las mañanas, lo primero, me hago rebase.

        Qué pasa si ha he publicado mi rama. Si ya había publicado a un remoto: division
        Cuando intente mandar la rama con el commit reescrito me dice que no encajan QUE HAN DIVERGIDO.
        Puedo forzarlo... Y que se quede la ultima en el remoto.
        Pero si alguien ha trabajado en la rama... le jodo el trabajo. Y eso no mola.Entonces la lio más
        Ya que todos los compañeros que se hubieran descargado la rama, al descarga la nueva: ERROR HAN DIVERGIDO !
        Y Pueden arrglarlo.. pueden hacer un pull forzado! FOLLON
        Es decir, antes de publicar, me tengo que asegurar muy y mucho de haber hecho el rebase.

# MERGE

Hay casos donde me interesa que la fusión quede reflejada... porque implica cambios en el codigo
Lo mio funciona.
Lo tuyo funciona.
Pero junto no. Tenemos que ajustarnos. Y eso implica hacer cambios YO... y hacer cambios TU.
Y en este caso, me interesa el commit de fusión.




---
# SOLID

S - Principio de responsabilidad única:
    Una clase / módulo solo debe tener una única razón para cambiar!
---

Usamos git para:
- Tener un historial:
  - Poder volver a versiones anteriores de mis ficheros
    - REFACTORIZACION !
    - DESARROLLO EXPLORATORIO
  - Recuperar funcionalidades que metí en un momento dado
    - Una funcionalidad que he acabado... y está lista, diga, NO LA ENTREGO
      - REVERT -> CHERRY PICK
    - Un arreglo que he hecho en una rama (hotfix) y me lo quiero traer a dev
      - CHERRY PICK
  - Por si hay un bug en producción, poder volver a la versión anterior en producción, uso el artifactory.
    Lo que si, es que tendré que ver DONDE SE INTRODUJO EL BUG.. y quién... para pedirle que lo arregle.
      - BLAME / BISECT 
  
Y para poder hacer TODAS ESAS COSAS, lo primero que necesito es tener un historial UTIL y LIMPIO!
Si no tengo un historial UTIL y LIMPIO, no vale para nada. Deja GIT


GIT: SCM (Source Code Management)

    Un proyecto, cuando tiene una version lista -> RELEASE -> REPO DE ARTEFACTOS: Nexus, Artifactory




Escribo código <> Pruebo > REFACTORIZO <> Pruebo > Subo
- MEJORAR LA MANTENIBILIDAD


-------dev--->C10 -------------------> CRa 
                \                   /
         ---Ra--C10 ............. CRa (squash)
                  \              /
    --RamaIvanRa--C10->C11->C12 /



TAGS

--> Git HOOK para meter un fin de linea en los ficheros

JAVA
  maven spotless PALANTIR

  PRE COMMIT: Si voy a dev:
    mvn test
      pom.xml           CONFIG DEL PROYECTO ---> Datos identificativos del proyecto (coordenadas) 
    npm run test                                    ID, VERSION
      package.json      CONFIG DEL PROYECTO ---> Datos identificativos del proyecto (coordenadas)

  lint



make


ant


# Quién establece la versión del proyecto? 

DESARROLLADOR

# Quién es la fuente de verdad de la versión del proyecto? 

GIT


Es automatizable el versionado de un proyecto? NI DE COÑA !


## Versiones de software

Esquema estándar de versionado de software: MAJOR.MINOR.PATCH 
                                            1.2.3

            ¿Cuándo cambian?
1 MAJOR     Breaking changes: Cambios que rompen la compatibilidad
2 MINOR     Nueva funcionalidad
            Funcionalidad marcada como deprecated
3 PATCH     Corrección de bugs


Quién sabe esto? UNA MAQUINA ?

En todo momento necesito tener controlada la versión de software en la que estoy trabajando.

Los IDs de commit me valen para algo? Para esto NADA de nada: TAGs

¿Cuándo se pone un tag? Cuando empiezo un desarrollo nuevo
¿En qué ramas se trabaja con tags? TODAS

                    0.0.1
                       v
        master         C3
                       /  
    release           C3                            C6               C9
                     / ^ 0.1.0-rc1                 / ^ 1.0.0-rc1    / ^ 1.0.0-rc2
  dev-> C1 -> C2 -> C3 -> C4 -> C5 -------------> C6 -> C7-> C8 -> C9
                                ^ \            /                    ^
                                0.2.0-dev     /                     1.0.0-dev
    feature1                        \ C5 -> C6
                                             ^ 1.0.0-dev-feature1


Lo habitual es usar el git para controlar lo tags.
Cuando abro rama, o subo commit de una rama a otra tengo que gestionar esto.
Nuevo commit en dev, muevo el tag de -dev
Abro rama: Nuevo tag, añadiendo sufijo de la rama
Subo a release: Nuevo tag, añadiendo rc el que toque
Subo a master: Nuevo tag, añadiendo la versión (quitando los sufijos)
Y antes de hacer un commit, modifico el archivo de configuración del proyecto : pom.xml, package.json, build.gradle, etc para que refleje la versión que estoy trabajando.


Toda la automatización la quiero en .git...

Cuidao ... que hay gente con buena fé que esta metiendo esto en Jenkins... y no es el sitio. GIT es el sitio... porque es el garante de la versión del proyecto: Y para esto están los hooks de git.

MAVEN, NPM, GRADLE, MAKE, ANT, Meto las dependencias.. y en las dependencias tengo que meter las versiones