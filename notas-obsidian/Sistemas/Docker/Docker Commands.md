___
Borrar todos los contenedores
```bash
docker stop $(docker ps -q)
```
___
Shell interactiva en el container
```bash
docker exec -it <ID_o_nombre_del_contenedor> /bin/sh
```
___
