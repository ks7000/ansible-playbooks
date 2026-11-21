# Configuración inicial del servidor en Ubuntu 24.04

Este guion llevará a cabo una configuración inicial del servidor para sistemas Ubuntu 24.04, tal y como se explica en la guía en inglés: [Instalando y configurando Ansible en Ubuntu 26.04](https://www.ks7000.net.ve/2026/11/13/instalando-y-configurando-ansible-en-ubuntu-26-04/).

> ⚠️ **Advertencia**
>
> Este libreto creará un usuario (aquí llamado `sammy`, la mascota de DigitalOcean) con derechos de administrador **y sin exigir explícitamente una contraseña para ejecutar** `sudo` (aunque le asignemos una contraseña con `passwd sammy` igual ejecutará de manera directa). _Se desaconseja esta configuración porque, aunque aligera bastante la configuración de libretos, si dado el caso esa cuenta de usuario fuera vulnerada pues igual necesitarán de conocer la contraseña de usuario para que las y/o los atacantes sigan avanzando, ES DECIR, se pierde una barrera de seguridad.

> ℹ️ **Información**
>
> De hecho, en realidad cualquier usuario que pertenezca al grupo `wheel` tendrá ese comportamiento de ejecutar `sudo` directamente y sin barreras.

Se crearán varios contenedores con las opciones especificadas en el archivo de variables `vars/default.yml`.

## Configuración

- `create_user`: El nombre del usuario remoto (quien ejecutará **sudo**) que se va a crear.
- `copy_local_key`: Ruta a una clave pública SSH local que se copiará como clave autorizada para el nuevo usuario. Por defecto, se copia la clave del usuario actual del sistema que está ejecutando Ansible.
- `sys_packages`: Matriz con la lista de paquetes que se deben instalar.

## Ejecución del libreto

Primeros pasos:

### 1. Descargar el libreto

```shell
git clone https://github.com/do-community/ansible-playbooks.git
cd ansible-playbooks/setup_ubuntu2404
```

### 2. Personalizar opciones

```shell
nano vars/default.yml
```

```yml
#vars/default.yml
---
create_user: sammy
copy_local_key: "{{ lookup('file', lookup('env','HOME') + '/.ssh/id_rsa.pub') }}"
sys_packages: [ 'curl', 'vim', 'git', 'ufw']
```

```shell
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

### 3. Ejecutar libreto

```command
ansible-playbook playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulta esta guía en inglés: [Initial Server Setup Guide for Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04).