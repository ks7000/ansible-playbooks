# Wordpress en Ubuntu 24.04 LAMP

## Creación de entorno para WordPress

Esta guía te permitirá instalar un sitio web de WordPress en un entorno LAMP (**L**inux, **A**pache, **M**ySQL y **P**HP) en un equipo con Ubuntu 18.04, tal y como se explica en la guía en inglés disponible: [How to Use Ansible to Set Up Wordpress on Ubuntu 18.04 LAMP](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04).

Se creará un anfitrión virtual con las opciones especificadas en el archivo de variables `vars/default.yml`.

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
git clone https://github.com/ks7000/ansible-playbooks.git
cd ansible-playbooks/wordpress-lamp_ubuntu2404
```

#### 2. Personalziar opciones

```shell
nano vars/default.yml
```

```yml
---
#PHP Settings
php_modules:
  [
    "php-curl",
    "php-gd",
    "php-mbstring",
    "php-xml",
    "php-xmlrpc",
    "php-soap",
    "php-intl",
    "php-zip",
  ]

#MySQL Settings
mysql_db: "wordpress"
mysql_user: "sammy_user"
mysql_password: "sammy_password"
mysql_root_password: "SuSuperContrasenaSecreta211!"
mysql_socket: "/var/run/mysqld/mysqld.sock"

#HTTP Settings
http_host: "servidor_207"
http_conf: "servidor_207.conf"
http_port: "80"
apache_service: "{{ 'apache2' if ansible_os_family == 'Debian' else 'httpd' }}"
apache_user: "{{ 'www-data' if ansible_os_family == 'Debian' else 'apache' }}"
apache_group: "{{ 'www-data' if ansible_os_family == 'Debian' else 'apache' }}"
apache_conf_dir: >-
  {{ '/etc/apache2/sites-available' if ansible_os_family == 'Debian' else '/etc/httpd/conf.d'
  }}
```

#### 3. Ejecutar el libreto

```command
ansible-playbook playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulte esta guía (en inglés): [How to Use Ansible to Install and Set Up WordPress with LAMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04).
