# NFS
### Servidor
1. Actualizar
```
sudo apt update
```
2. Instalar NFS
```
sudo apt install nfs-kernel-server
```
3. Crear directorio
```
sudo mkdir -p /mnt/nfs_share
```
4. Habilitar acceso a todos al directorio creado
```
sudo chown -R nobody:nogroup /mnt/nfs_share
```
5. Otorgar permisos necesarios
```
sudo chmod 777 /mnt/nfs_share
```
6. Acceder al archivo
```
sudo nano /etc/exports
```
7. Insertar línea resaltada en blanco en cualquier parte del documento
```
/mnt/nfs_share 192.168.0.0/24(rw,sync,no_subtree_check)
```
8. Ejecutar
```
sudo exportfs -a
```
9. Resetear servicio
```
sudo systemctl restart nfs-kernel-server
```
10. Permitir acceso al firewall
```
sudo ufw allow from 192.168.0.0/24 to any port nfs
```
11. Habilitar firewall
```
sudo ufw enable
```
12. Cerrar terminal de PUTTY y en el servidor desde VMWare colocar el siguiente comando para habilitar SSH
```
sudo ufw allow 22
```
### Cliente (Ubuntu)
1. Actualizar
```
sudo apt update
```
2. Instalar NFS para clientes
```
sudo apt install nfs-common
```
3. Crear directorio
```
sudo mkdir -p /mnt/nfs_clientshare
```
4. Acceso a la carpeta
```
sudo mount <dirección_del_servidor>:/mnt/nfs_share /mnt/nfs_clientshare
```
5. (Si sale algún error) colocar los siguientes comandos
```
sudo systemctl is-enabled nfs-common
sudo systemctl enable nfs-common
file /lib/systemd/systems/nfs-common-service
sudo rm /lib/systemd/system/nfs-common.service
sudo systemctl daemon-reload
sudo systemctl status nfs-common
sudo systemctl start nfs-common
sudo systemctl status nfs-common
sudo systemctl enable nfs-common
```
