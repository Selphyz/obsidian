___
Borrar TODOS los contenedores
```bash
docker kill $(docker ps -q)
```
---
Terminal Interactiva
```bash
docker exec -it <ID_o_nombre_del_contenedor> /bin/bash
```
