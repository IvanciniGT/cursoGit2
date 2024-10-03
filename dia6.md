# Servicios de git públicos importantes:
                                                       SaaS     On-premise
- GitHub        Microsoft                               √
- GitLab        GitLab                                  √           √
- Bitbucket     Atlassian(Jira, Confluence, Trello)     √           √

Estos programas no solo ofrecen repos remotos. Ofrecen muchas otras cosas:
- Autenticación y control de acceso a los repositorios... A muchos niveles:
    - Quien puede ver el repo
    - Quien puede tocar el repo
    - Quién puede tocar una rama del repo (RAMAS PROTEGIDAS)
- Mecanismo alternativo para trabajar y compartir código:
  - Github y Bitbucket:     Pull Requests   \
  - GitLab:                 Merge Requests  / Misma mierda!
- Control de issues ( como un foro donde se discuten problemas y se asignan a personas para que los resuelvan)... y los mensajes pueden ir asociados a commits/ficheros
- Gitlab y Github nos ofrecen también herramientas de gestión de proyectos
  - En bitbucket se puede integrar con Jira para hacer lo mismo
- Github y Gitlab me ofrecen su propio servidor de automatización de tareas (Github Actions y Gitlab CI/CD)
  - Bitbucket se integra con Bamboo
  
  Nota: github actions, gitlab CI/CD y bamboo son herramientas tipo Jenkins.
  Nos permiten automatizar tareas asociadas a operaciones de git (commits, merges, etc)
- Exploradores de código
- Gráficos de actividad (Donde se ve la actividad de los usuarios en el repo)

---

# Pull Requests / Merge Requests

- Son una forma de colaborar en un proyecto distinta a simplemente generar commits en ramas y fusionarlas.

Esta pensado para equipos muy grandes o equipos donde no tengo suficiente confianza en los miembros del equipo.

Si estoy en un proyecto yo y mi primo me olvido de esto. No tiene sentido!
- Proyectos Open Source (donde mucha gente interviene y necesito controlar lo que se sube)
- En empresas, debido a la rotación de personal, es una forma de controlar lo que se sube.


Cuando trabajamos con PR/MR:
- Un desarrollador lo primero que hace es...
  - A veces me dejan crear una rama directamente.. pero no me dejan fusionarla con nada
  - En muchas ocasiones ni eso.. y entonces lo que hacemos es FORKEAR el repo:
      - Como un clonado del repo, dentro del propio servidor de almacenamiento de repositorios:
        Dentro del propio gitlab/github/bitbucket
- Posteriormente clono el repo en mi máquina (el forkeado)... Si me han dejado abrir rama, pues guay.. el único que hay es que que clono.
- Yo hago mis cambios. Desde esa rama puedo abrir más ramas si quiero.
- Lo que pno puedo ni en un caso ni en otro es subir cosas a las ramas originales que están protegidas. Y entonces hago una SOLICITUD DE FUSION DE CAMBIOS: PR/MR
  ESTO NO ES GIT. Es una funcionalidad de los servidores de git.
  Esa petición debe ser revisada por alguien con permisos para hacerlo y en su caso aceptarla o rechazarla. Y estos servicios nos ofrecen asociado a esta funcionalidad el llevar una especie de hilo de discusión asociado a la PR/MR. 



# Iniciar un proyecto nuevo.

Tenemos 2 opciones:
- OPCION 1: 
  - Creo un repo en local: git init
    - NO PUEDO CREAR COMMITS POR SEPARADO EN LOCAL ^ Y EN REMOTO v
  - Creo un repo en el servidor: github, gitlab, bitbucket
  - Asocio el repo local con el remoto: git remote add origin URL
  - Y ya subo cosas: git push origin master
- OPCION 2:
  - Creo un repo en el servidor: github, gitlab, bitbucket
  - Clono el repo en local: git clone URL
  - Y ya subo cosas: git push origin master


---

> MAL

# Local
git init
git add archivo.txt
git commit -m "Primer commit"

# Remoto
Creo un repo remoto y genero un commit en él.

# Local
git remote add NOMBRE URL_REMOTO
git push NOMBRE master = ERROR (las ramas han divergido)

*En cuanto marcamos al crear un repo en remoto que queremos un :
- README.md
- .gitignore
- LICENSE
Se genera un commit en el remoto que no tenemos en local. 

---

BLAME - Auditoria... Ver quién y cuando y en qué commit toco algo.
- Que me ayude, preguntarle a la persona que toco algo en un commit concreto.
- Ver otras cosas que se incluyeron con esa linea (COMMIT)
- Revertir cambios

BISECT- Quiero averiguar cuando se metió un cambio que nos está jodiendo.

Aplica un divide y vencerás. Me va partiendo el historial de commits a la la mitad


1
2    MALO
3   MALO
4
5   BUENO
6
7
8   BUENO
9
10





Submodules


100
 50
 25
 13
  7
  4
  2
  1