
Un producto de software es algo que se crea, se usa y hay que mantener y evolucionar.


    DESARROLLO <> PRUEBAS > OK > REFACTORIZACION <> PRUEBAS > OK

Y parte de dejar un sistema listo para su mantenimiento y evolución es tener un historial de versiones LIMPIO y útil.


---

# DEVOPS

Filosofía, una cultura, un movimiento... en pro de ... LA AUTOMATIZACION !
Compis!!! Vamos a automatizar todo lo que podamos!! BIEN !!!!
Todo? que es todo? Todo lo que está entre el DEV -> OPS

Tareas en el ciclo de vida de un software:

                                    AUTOMATIZABLE?          HERRAMIENTAS

- Planificación     - Plan              POCO
- Desarrollo        - Code              POCO
- Empaquetado       - Build             SI
                                                            JAVA: MAVEN, GRADLE, SBT, ANT
                                                            C#: MSBUILD, DOTNET, NUGET
                                                            JS: NPM, YARN, WEBPACK
------------------------------------------------------------------------> Desarrollo ágil
- Pruebas           - Test
  - Diseño                              POCO
  - Ejecución                           MUCHO           
                                                            FRAMEWORKS: JUNIT, TESTNG, NUNIT, XUNIT, MOCHA, JEST
                                                            UI: SELENIUM, CYPRESS, APPUM, TESTCAFE, KARMA, UFT
                                                            Servicios WEB: POSTMAN, SOAPUI, RESTASSURED, KARATE, ReadyAPI
                                                            Rendimiento/Carga: JMETER, GATLING, WRK, APACHE BENCH
                Estas pruebas... me vale ejecutarlas en la máquina del desarrollador?   NO... No me fio.. está maleao ese entorno
                Estas pruebas... me vale ejecutarlas en la máquina del tester?          NO... No me fio.. está maleao ese entorno
                Estas pruebas... me vale ejecutarlas en la máquina de integración que hemos montado el día del proyecto para estos menesteres?  NO... No me fio.. está maleao ese entorno   (antes si... pardillos eramos)... Después de 50 instalaciones, cómo va a estar ese entorno? MALEAO
                Y hoy en día, la tendencia es a crear entornos de usar y tirar... creados bajo demanda... adhoc para lanzar unas pruebas y luego se destruyen: CONTENEDORES
--------------------------------------------------------------------------> Integración continua: Continuous Integration
Cuando continuamente tengo la última versión del producto (de lo que se está haciendo) en un entono de Integración, sometido a pruebas automatizadas.
- Liberación        - Release           MUCHO
    El acto de poner la última versión de mi producto (artefacto) en manos de mi cliente:
        - .jar -> Nexus
        - app android -> Google Play
        - app ios -> App Store 
--------------------------------------------------------------------------> Entrega continua: Continuous Delivery
- Despliegue        - Deploy            MUCHO \
--------------------------------------------------------------------------> Despliegue continuo: Continuous Deployment
- Operación         - Operate           MUCHO  > Kubernetes, Openshift, ...
- Monitorización    - Monitor           MUCHO /
--------------------------------------------------------------------------> DEVOPS

Cada una de esas herramientas, automatiza una pieza del puzzle:
- Maven empaqueta en automático
- Junit me permite ejecutar pruebas en automático
- Selenium me permite ejecutar pruebas de UI en automático
- Docker me permite crear entornos de usar y tirar en automático
- Kubernetes me permite desplegar en automático

Pero son piezas sueltas... hay que coserlas... orquestarlas... Y entonces necesito de un servidor de automatización: JENKINS, TEAMCITY, BAMBOO, CIRCLECI, GITLABCI, TRAVISCI, Github Actions, Azure DevOps(TFS), ...

Y hoy en día, lo que buscamos es que cuando un desarrollador hace commit... y marca ese commit con un tag: v1.2.3... que automáticamente se dispare una serie de tareas SIN INTERVENCIÓN HUMANA:
Quiero a jenkins creando un entorno de pruebas con docker.
Quiero en ese entorno descargar con git el código fuente de ese tag.
Quiero a mevn compilarndo el código y ejecutando las pruebas unitarias con Junit.
Quiero a sonarqube realizando una revisión de código de calidad.
Si todo va bien, quiero hacer pruebas en un entorno de integración con una BBDD real, de pruebas.
Quiero levantar un servidor de aplicaciones con docker y desplegar la aplicación.
Quiero poder hacer pruebas de interfaz gráfica con 200 combinaciones de SO/Dispositivo/Navegador/Version de navegador sobre la app web.
Si todo va bien, quiero eso en Artifactory/Nexus
Desde ahí quiero un job que lance un despliegue en kubeernetes, donde se ejecute un smoke test.
Quiero manda un email a todo el mundo con el resultado de todo esto.

Y en 20 minutos, desde que un desarrollador ha hecho commit, y sin que nadie haga nada, tengo los cambios en producción. ESTE ES EL MUNDO DESDE HACE UNA DECADA!

Y una de 2, al hacer commit:
x O el desarrollador está muy volao! y se la suda todo
x O le va a dar un infarto al apretar enter
√ O tiene confianza en que solo se subirá a producción si todo va bien.. habiendo muchos controles de por medio!

Y las pruebas hoy son criticas...
Y forzar procedimiento rígidos de trabajo (automatizaciones) es fundamental para que todo vaya bien.

---

# Metodologías ágiles

Entrega incremental al cliente! No le doy el producto el día 300... Cada 20 días le hago una entrega en producción.
Desde el día 20 de proyecto.

Por qué hago esto? Por qué he tomado esta decisión?
- Satisfacer al cliente
- Feedback rápido

Lo que no me cuentan en los cursos de SCRUM... es que esto nos ha ayudado con muchos de los problemas que teníamos al usar metodologías en cascada... pero también ha traído nuevos problemas:
- Cuantas instalaciones en pro voy a hacer ahora? Tropetantas, cada 20 días??? REALLY??? TAS DE COÑA???
- Cuantas instalaciones en pre voy a hacer ahora? Tropetantas, cada 20 días??? REALLY??? TAS DE COÑA???
- Espera.. y si paso a pro cada 20 días... que tengo que hacer antes??? Pruebas a nivel de producción.

Y de donde sale la pasta? y los recursos? y el tiempo? para hacer todo esto? NO HAY, ni pasta, ni recursos, ni tiempo.
Entonces? SOLO HAY UNA SOLUCION: AUTOMATIZARLO TODO

Este es el mundo de hoy, junto con otras cosas.

# Arquitecturas de microservicios

Las app web tradicionales: .war .ear OBSOLETO: TOTALMENTE

El sistema de Animalitos Fermín.

    Sistema WEB
        Frontal (HTML, CSS, JS)             BACKEND (programas JAVA, C#, PHP)
        Dónde se generaba el HTML...        En servidor: YA NO VALE!

    Los sistemas hoy en día son más complejos

    FRONTAL:                                                    BACKEND
        Web  1.1.0                                                       
            HTML se genera en navegador(JS)
                Estándar WebComponents: Estándar del W3C, igual que HTML o CSS
                Que permite montar un nuevo tipo de página web: SPA (Single Page Application)
                                                                  1.1.5
                Páginas que mutan sin recargar la página          2.0.0            2.0.0               2.0.0       2.0.0
        Apps moviles                         <-JSON-              rest             nuevoAnimal()       -> save()    -> BBDD
            Android   1.0.0                                       CONTROLADOR      SERVICIO            REPOSITORIO
            iOS       2.0.0                                                                            JEE(JPA)
        Apps de escritorio                                        soap
        App de un cajero (corre windows)
        IVR: Sistema de voz interactivo
        Siri, Alexa, Google Home 1.0.0

        Tengo un sistema v1.0.0
        Y me dice el fermin, que quiero que lo animales, que antes tenían:
            nombre
            tipo
            fecha de nacimiento
        Ahora pueden tener Una foto

Y AQUI ES DONDE ENTRAN LAS MET. AGILES.
Una foto no... muchas.. y audio, video...

JSON v1.1.0
{
    "nombre": "Firulais",
    "tipo": "Gato",
    "fechaNacimiento": "2010-01-01",
    "foto": "http://www.fermin.com/fermin3.jpg"
}

JSON v2.0.0
{
    "nombre": "Firulais",
    "tipo": "Gato",
    "fechaNacimiento": "2010-01-01",
    "multimedia": {
        fotos: [
            "http://www.fermin.com/fermin3.jpg",
            "http://www.fermin.com/fermin4.jpg",
            "http://www.fermin.com/fermin5.jpg"
        ],
        audios: [
            "http://www.fermin.com/fermin3.mp3",
            "http://www.fermin.com/fermin4.mp3",
            "http://www.fermin.com/fermin5.mp3"
        ],
        videos: [
            "http://www.fermin.com/fermin3.mp4",
            "http://www.fermin.com/fermin4.mp4",
            "http://www.fermin.com/fermin5.mp4"
        ]

    }
}

---

## Reescritura del historial

Hasta ahora hemos restaurado ficheros del área del staging al working directory.
También del Repositorio (algun commit) al working directory y/o al staging.
Pero hemos reescrito poco ya dentro del repositorio:
- git commit --amend
- git rebase 

Esas 2 utilidades están bien para ir dejando / creando un historial limpio y ordenado.

Pero que hacer cuando historial YA está sucio y desordenado? Se me ha descontrolado el historial y quiero dejarlo organizado y útil.
2 operaciones:
- git reset
- git rebase -i # Git rebase INTERACTIVO... y es otra guerra totalmente distinta a un rebase normal.

Podríamos encajar aquí el git revert... pero lo cierto es que el revert no modifica el historial... crea un nuevo commit anulación de cambios.

### Git reset

Qué hace? Borra commits del historial... aunque no elijo cuales... lo que digo es en cual quiero quedar (donde se posicionará el HEAD). Git borrará todos commits siguientes a ese:

                                HEAD
                                v
        C1 -> C2 -> C3 -> C4 -> C5
            Y quiero volver al C3... pero quiero que desaparezcan C4 y C5 del repositorio
        
        C1 -> C2 -> C3
                    ^
                    HEAD

            git reset C3

Pero hay 3 git reset... Más bien 3 modos de ejecutar el git rest:
- git reset --soft
- git reset --mixed             # el por defecto
- git reset --hard

                            WORKING DIR (mi carpeta)        AREA DE STAGING         REPOSITORIO
            --soft                  NO                          NO                      SI      
                     borra commits, pero no me elimina ni el código, ni las inclusiones que he hecho al área de staging
            --mixed                 NO                          SI                      SI
                     borra commits, me elimina las inclusiones que he hecho al área de staging, pero no me elimina el código
            --hard                  SI                          SI                      SI
                     borra commits, me elimina las inclusiones que he hecho al área de staging, y me elimina el código
                     MUCHO CUIDADO... este commit es destructivo. PERDEIS CODIGO



> Ejemplo SOFT
            C1 -> C2 -> C3 -> C4 -> C5
            git reset --soft C3
                            WORKING DIR (mi carpeta)        AREA DE STAGING         REPOSITORIO
                 antes               C5                              C5                  C1 -> C2 -> C3 -> C4 -> C5
                 después             C5                              C5                  C1 -> C2 -> C3

                Pierdo código? NO
                Pierdo lo había dicho de ese código que tengo en mi carpeta que quiero que suba al proximo commit? NO
                Pierdo es historia de los commits? SI
                Caso de uso típico: 
                    Me he vuelto loco creando commits... que no aportan nada... Pero el código al final me ha quedado guay.
                        Si C3, C4 y C5 no aportan tanto... quizás solo el C5
                            git reset --soft C3
                            git commit --amend -m 'Cambio guay'
                                C1 -> C2 -> C5'

> Ejemplo MIXED
            C1 -> C2 -> C3 -> C4 -> C5
            git reset --mixed C3
                            WORKING DIR (mi carpeta)        AREA DE STAGING         REPOSITORIO
                 antes               C5                              C5                  C1 -> C2 -> C3 -> C4 -> C5
                 después             C5                              C3                  C1 -> C2 -> C3

                Pierdo código? NO
                Pierdo lo había dicho de ese código que tengo en mi carpeta que quiero que suba al proximo commit? NO
                Pierdo es historia de los commits? SI
                Caso de uso típico: 
                    Me he vuelto loco creando commits... que no aportan nada... Pero el código al final me ha quedado guay.
                    Y de hecho me pase metiendo cosas en el repositorio que no quería meter... al menos en ese commit.
                            git reset --mixed C3
                            git commit --amend -m 'Cambio guay'
                                Me diría que no hay cambios pendientes de confirmar
                            git status, me informaría de que hay cambios sin confirmar, los que introduje en C4 y C5

                        Si no quiero perder el código, pero quiero generar otra estructura de commits, donde cada commit incluya solamente algunos de los cambios... los asociados a un RQ.
                            git reset --mixed C3
                            git add PARTE DE LOS ARCHIVOS
                            git commit --amend -m 'R1'
                            git add PARTE DE LOS ARCHIVOS
                            git commit -m 'R2'
                                C1 -> C2 -> R1 -> R2
                            Y puede incluso que haya cosas que no suba a repo.
                                Por ejemplo... estoy con java, maven y he subido la carpeta target/
> Ejemplo HARD
            C1 -> C2 -> C3 -> C4 -> C5
            git reset --hard C3
                            WORKING DIR (mi carpeta)        AREA DE STAGING         REPOSITORIO
                 antes               C5                              C5                  C1 -> C2 -> C3 -> C4 -> C5
                 después             C3                              C3                  C1 -> C2 -> C3

                Pierdo código? SI
                Pierdo lo había dicho de ese código que tengo en mi carpeta que quiero que suba al proximo commit? SI
                Pierdo es historia de los commits? SI
                Caso de uso típico: 
                    Quiero deshacer trabajo... para volver a un punto anterior:
                      - Desarrollo exploratorio... y me he metido en un callejón sin salida
                      - Si un refactor me ha salido mal y quiero empezar

Estos 3 son sencillos... pero tampoco dan para mucho... son casos muy concretos, aunque habituales.

Hay casos que no resuelven... y para esos caso tenemos una herramienta mucho más potente... Diría que la herramienta más potente de GIT: 

# GIT REBASE INTERACTIVO

Y con mucha diferencia, la herramienta más compleja/peligrosa de GIT.

Básicamente se trata de reescribir todo un trozo del historial... desde un determinado commit... quizás 20 commits atrás... o 2... o 200.
Más de 15-20 (locura) no tiene sentido... es inmanejable.

Y este rebase se ejecuta en fases:
1. Elegir el commit desde el que quiero reescribir:
    $ git rebase -i HEAD~3
2. En este punto, git mostrará una ventana (editor de textos) con los identificadores de los commits desde el que quiero reescribir hasta el HEAD.
   Al lado de cada commit, me mostrará la acción que se va a realizar sobre ese commit. Por defecto, será 'pick' (coger).

            pick 1298121 # ID HEAD
            pick 1298122 # ID HEAD~1
            pick 1298123 # ID HEAD~2
            pick 1298124 # ID HEAD~3
   Si guardo este archivo sin hacer cambios, el git rebase interactiva no hará nada... finaliza sin ejecutar cambios.
   El tema viene porque puedo cambiar en ese momento (estamos en un editor de textos) el 'pick' por otra acción.
   Tenemos un huevo de acciones disponibles:
    - pick
    - reword
    - edit
    - squash
    - fixup
    - exec
    - drop
    - label
    - reset
    - merge
Algunas no hacen nada.
Otras borran el commit.
Otras juntaran varios commits en uno solo.
Otras cambiarán el mensaje del commit.
Otras ejecutarán un comando.


El ejecutar un rebase interactivo implica una reescritura en profundidad del historial... y a puedo liar parda... puedo perder historial... o dejarlo hecho un desastre.
Siempre, antes de un rebase interactivo, hacer un backup del repositorio: Copio la carpeta .git a otro sitio... y si la riego, me vale con copiarla de vuelta.

Esas tareas que elijo en el rebase interactivo, se ejecutan en orden... de arriba a abajo.
Algunas generan conflictos... y hay que resolverlos... y luego seguir con el rebase.
