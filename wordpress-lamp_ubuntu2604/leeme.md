# Wordpress en Ubuntu 18.04 LAMP

## Configuración inicial de servidor Ubuntu 18.04


Este guion llevará a cabo una configuración inicial del servidor para sistemas Ubuntu 18.04, tal y como se explica en la guía en inglés sobre
[Initial Server Setup Guide for Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04).
Se crearán varios contenedores con las opciones especificadas en el archivo de variables `vars/default.yml`.

### Settings

- `create_user`: El nombre del usuario (con derechos de ejecución **sudo**) a crear.
- `copy_local_key`: Ruta a una clave pública SSH local que se copiará como clave autorizada para el nuevo usuario. Por defecto, se copia la clave del usuario del sistema actual que está ejecutando Ansible.
- `sys_packages`: Matriz con la lista de paquetes que deben instalarse.


### Ejecutando este libreto

Pasos iniciales:

#### 1. Descargar el libreto

```shell
git clone https://github.com/do-community/ansible-playbooks.git
cd ansible-playbooks/setup_ubuntu1804
```

#### 2. Personalizar opciones

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

#### 3. Ejecutar el libreto

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulta esta guía: [Initial Server Setup Guide for Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04).

## Creación de entorno para WordPress

Esta guía te permitirá instalar un sitio web de WordPress en un entorno LAMP (**L**inux, **A**pache, **M**ySQL y **P**HP) en un equipo con Ubuntu 18.04, tal y como se explica en la guía en inglés disponible: [How to Use Ansible to Set Up Wordpress on Ubuntu 18.04 LAMP](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04). Se creará un anfitrión virtual con las opciones especificadas en el archivo de variables `vars/default.yml`.

### Configuración

- `php_modules`: Una matriz que contiene las extensiones de PHP que deben instalarse para que funcione correctamente su instalación de WordPress. Es innecesario modificar esta variable,  quizás se necesite añadir nuevas extensiones a la lista si su configuración específica lo requiere.
- `mysql_root_password`: La contraseña que deseas para la cuenta **root** de MySQL.
- `mysql_db`: El nombre de la base de datos de MySQL que debe crearse para WordPress.
- `mysql_user`: El nombre del usuario de MySQL que debe crearse para WordPress.
- `mysql_password`: La contraseña del nuevo usuario de MySQL.
- `http_host`: Su nombre de dominio.
- `http_conf`: El nombre del archivo de configuración que se creará en Apache.
- `http_port`: Número de puerto HTTP para este anfitrión virtual, siendo `80` el valor por defecto.

### Ejecutando el libreto

Guía de inicio rápido para quienes ya están familiarizados con Ansible:

#### 1. Descargar el libreto

```shell
git clone https://github.com/do-community/ansible-playbooks.git
cd ansible-playbooks/wordpress-lamp_ubuntu1804
```

#### 2. Personalziar opciones

```shell
nano vars/default.yml
```

```yml
---
#System Settings
php_modules: [ 'php-curl', 'php-gd', 'php-mbstring', 'php-xml', 'php-xmlrpc', 'php-soap', 'php-intl', 'php-zip' ]

#MySQL Settings
mysql_root_password: "mysql_root_password"
mysql_db: "wordpress"
mysql_user: "sammy"
mysql_password: "password"

#HTTP Settings
http_host: "your_domain"
http_conf: "your_domain.conf"
http_port: "80"
```

#### 3. Ejecutar el libreto

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulte esta guía: [How to Use Ansible to Install and Set Up WordPress with LAMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04).
