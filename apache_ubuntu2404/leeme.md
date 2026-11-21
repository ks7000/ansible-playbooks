# Apache en Ubuntu 24.04

Este libreto instalará el servidor web Apache 2 en un equipo con Ubuntu 24.04, tal y como se explica en la guía [Instalando y configurando Ansible en Ubuntu 26.04] (https://www.ks7000.net.ve/2026/11/13/instalando-y-configurando-ansible-en-ubuntu-26-04/). Se creará un host virtual utilizando las opciones especificadas en el archivo de variables `vars/default.yml`.

## Configuración

- `app_user`: Un usuario remoto que no sea usuario **root** en el anfitrión de Ansible y que será el propietario de los archivos de la aplicación.
- `http_host`: Su nombre de dominio (o dirección IP).
- `http_conf`: El nombre del archivo de configuración que se creará en Apache.
- `http_port`: Puerto HTTP; el valor por defecto es 80.
- `disable_default`: Si se debe desactivar o no el sitio web predeterminado de Apache. Cuando se establece en `true` su nuevo host virtual se utilizará como sitio web predeterminado. El valor por defecto es `true`.

## Ejecución de este libreto

Pasos rápidos:

### 1. Obtener el libreto

```shell
cd 
[ -d "ansible-playbooks" ] || git clone https://github.com/ks7000/ansible-playbooks.git
cd ansible-playbooks/apache_ubuntu2604
git pull
```

### 2. Personalizar opciones

```shell
nano vars/default.yml
```

```yml
#vars/default.yml
---
app_user: "jimmy"
http_host: "servidor_207.ks7000.net.ve"
http_conf: "servidor_207.conf"
http_port: "80"
disable_default: true
```
```shell
echo "192.168.9.207 servidor_207.ks7000.net.ve" | sudo tee -a /etc/hosts

mkdir \
-p ~/proyecto-ansible-ubuntu/inventories\
/servidores_ubuntu/host_vars/servidor_207

nano ~/proyecto-ansible-ubuntu/inventories\
/servidores_ubuntu/host_vars/servidor_207/eleva.txt
```

Colocar la contraseña y guardar fichero. Aplicar derecho de lectura solamente al usuario propietario:

```shell
chmod 600 \
~/proyecto-ansible-ubuntu/inventories\
/servidores_ubuntu/host_vars/servidor_207/eleva.txt
```

```shell
nano ansible.cfg
```

```
become_password_file = ~/proyecto-ansible-ubuntu/inventories/servidores_ubuntu/host_vars/servidor_207/eleva.txt
inventory = ../hosts.ini
```

### 3. Ejecutar el libreto

```command
ansible-playbook -l servidor_207 -i ~/ansible-playbooks/hosts.ini -u $(whoami) playbook.yml
```
### 4. Verificar la página HTML

Ejecutar el navegador web preferido e introducir en la barra de direcciones:

```
http://servidor_207.ks7000.net.ve/
```
