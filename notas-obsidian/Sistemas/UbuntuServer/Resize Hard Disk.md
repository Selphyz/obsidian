```bash
df -h
lsblk
sudo growpart /dev/sda 3
sudo pvresize /dev/sda3
sudo lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

Utiliza `growpart` para expandir la partición `sda3` en el disco `sda`
Ahora, informa a LVM que la partición `sda3`, que es un Volumen Físico (PV), ha cambiado de tamaño con pvresize
Expandir el Volumen Lógico (LV) con lvextend `ubuntu--vg-ubuntu--lv`
Expandir el Sistema de Archivos