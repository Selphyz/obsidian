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
Formato del output
```bash
docker ps -a --format "table {{.Names}}\t{{.Image}}\t{{.Ports}}"
```
___
Copiar ficheros de un container
```bash
docker cp container_id:container_filepath local_filepath
```
___
Habilitar hosting de modelos en docker desktop
```bash
docker desktop enable model-runner
docker model
```
___
