# LAMP en Ubuntu 26.04

Esta guía instalará un entorno LAMP (**L**inux, **A**pache, **M**ySQL y **P**HP) en una máquina con Ubuntu 26.04 .

La configuración de inicio del servidor está explicado en el artículo [Instalando y configurando Ansible en Ubuntu 26.04](https://www.ks7000.net.ve/2026/11/13/instalando-y-configurando-ansible-en-ubuntu-26-04/) (también es es válido para 24.04 y 22.04).

Se creará un anfitrión virtual con las opciones especificadas en el archivo de variables `vars/default.yml` .

En la carpeta `../host_vars` se guarda un fichero `servidor_211.yml` con la ruta de la clave SSH.

## Configuración

- `mysql_root_password`: Contraseña para la cuenta de usuario **root** de MySQL.
- `app_user`: Un usuario remoto sin privilegios de **root** en el anfitrión de Ansible que será el propietario de los archivos de la aplicación.
- `http_host`: Su nombre de dominio web.
- `http_conf`: El nombre del archivo de configuración que se creará en Apache.
- `http_port`: Número de puerto para HTTP, el valor por defecto es 80.
- `disable_default`: Si se desea desactivar o no el sitio web predeterminado de Apache. Si se establece en `true` (verdadero), su nuevo anfitrión virtual se utilizará como sitio web predeterminado. El valor por defecto es `true`.

## Ejecución del libreto

Guía de inicio rápido para quienes ya están familiarizados con Ansible:

### 1. Descargar el libreto

```shell
git clone https://github.com/ks7000/ansible-playbooks.git
cd ansible-playbooks/lamp_ubuntu2604
```

### 2. Configurar preferencias

```shell
nano vars/default.yml
```

```yml
---
mysql_root_password: "SuSuperContrasenaSecreta211!"
app_user: "jimmy"
http_host: "servidor_211.ks7000.net.ve"
http_conf: "servidor_211.conf"
http_port: "80"
disable_default: true
```

> [!WARNING]
> Las contraseñas deben ir sin caracteres especiales, tal como la letra eñe (sí, irónico).

```shell
echo "192.168.9.211 servidor_211.ks7000.net.ve" | sudo tee -a /etc/hosts

mkdir \
-p ~/proyecto-ansible-ubuntu/inventories\
/servidores_ubuntu/host_vars/servidor_211

nano ~/proyecto-ansible-ubuntu/inventories\
/servidores_ubuntu/host_vars/servidor_211/eleva.txt
```

Colocar la contraseña y guardar fichero. Aplicar derecho de lectura solamente al usuario propietario:

```shell
chmod 600 \
~/proyecto-ansible-ubuntu/inventories\
/servidores_ubuntu/host_vars/servidor_211/eleva.txt

### 3. Ejecutar el libreto

```command
ansible-playbook -l servidor_211 -i ~/ansible-playbooks/hosts.ini -u $(whoami) playbook.yml
```
### 4. Verificar la página HTML

Ejecutar el navegador web preferido e introducir en la barra de direcciones:

```
http://servidor_211.ks7000.net.ve/info.php
```
