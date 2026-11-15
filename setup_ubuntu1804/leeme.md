# Configuración inicial del servidor en Ubuntu 18.04

Este guion llevará a cabo una configuración inicial del servidor para sistemas Ubuntu 18.04, tal y como se explica en la guía en inglés: [Initial Server Setup Guide for Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04).
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
cd ansible-playbooks/setup_ubuntu1804
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

### 3. Ejecutar libreto

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulta esta guía en inglés: [Initial Server Setup Guide for Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04).