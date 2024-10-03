
# Git stash

Pensar en ello como el portapapeles de git.
Me permite copiar CAMBIOS al portapapeles y pegarlos en otro lugar... o en el mismo de donde los cogí.

BASICAMENTE ES UN PORTAPAPELES QUE ADMITE las operaciones:
- Cortar
- Pegar

Es un portapapeles guay... YA que me permite tener muchos paquetes de cambios en el portapapeles y poder ir pegando el que me interese en cada momento.

- merge: Nos genera commit de fusion.. si yo he tocado cosas en paralelo
- rebase: Reescribe los commits para incorporar el cambio por delante.. Esto está guay.. nos encanta.. siempre y cuando no haya subido ya al repo central... entonces PAILAS !!!!
- cherry-pick: Me permite coger un commit y pegarlo en otro lugar... como si fuera un portapapeles de commits.
  Voy a tener nuevo commit, pero no de fusión de cambios... no hay spiderman
- stash: Me lo traigo, pero sin commit, solo al working dir... y ya generaré commit cuando quiera, como quiera y con lo que quiera


---

# Remotos

Github <-
Gitlab
Bitbucket