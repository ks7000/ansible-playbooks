# Comunidad DO / Comunidad KS7000 - Libretos de Ansible

Una recopilación de guiones en libretos (libro de memoria o, en idioma inglés, _playbooks_) minimalistas de Ansible para automatizar la configuración de servidores, basada en las guías de la comunidad de DigitalOcean y continuada por la [comunidad de KS7000](https//www.ks7000.net.ve/).

Recursos (en idioma inglés):

- [Initial Server Setup for Ubuntu 18.04](https://github.com/do-community/ansible-playbooks/tree/master/setup_ubuntu1804) *
- [Apache on Ubuntu 18.04](https://github.com/do-community/ansible-playbooks/tree/master/apache_ubuntu1804)
- [LEMP on Ubuntu 18.04](https://github.com/do-community/ansible-playbooks/tree/master/lemp_ubuntu1804)
- [LAMP on Ubuntu 18.04](https://github.com/do-community/ansible-playbooks/tree/master/lamp_ubuntu1804)
- [WordPress with LAMP on Ubuntu 18.04](https://github.com/do-community/ansible-playbooks/tree/master/wordpress-lamp_ubuntu1804)
- [Docker on Ubuntu 18.04](https://github.com/do-community/ansible-playbooks/tree/master/docker_ubuntu1804)

_\*La configuración inicial del servidor debería ser su punto de partida para los servidores nuevos._

## Estructura de libretos

Los libretos que contiene este repositorio se han creado con fines educativos y deben servir de base para crear sus propios libretos y roles.

Aunque hemos optado por no utilizar roles, estos guiones siguen una estructura específica para facilitar su reutilización, al tiempo que se mantienen, en su mayor parte, autónomos y sencillos.

Por ejemplo, así es como está estructurado el libreto `lemp`:

```
lemp_ubuntu1804
├── files
│   ├── info.php.j2
│   └── nginx.conf.j2
├── vars
│   └── default.yml
├── playbook.yml
├── leeme.md
└── readme.md

```

- `files/`: Directorio que contiene las plantillas y otros archivos necesarios para el libreto.
- `vars/`: Directorio para guardar los archivos de variables. Se incluye de forma predeterminada un archivo de variables llamado `default.yml`.
- `playbook.yml`: El archivo con el libreto de guiones.
- `leeme.md`: Instrucciones y enlaces relacionados con esta guía práctica.
- `readme.md`: (En idioma inglés) Instrucciones y enlaces relacionados con esta guía práctica.

## Primeros pasos

Para configurar tu entorno de Ansible, siga la guía publicada en idioma inglés: [How to Install and Configure Ansible on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04).

### Conexión de prueba

Desde su ordenador local o desde el nodo de control de Ansible, ejecute:

```command
ansible all -m ping -u remote_user
```

Si consigue recibir una respuesta "pong" de Sus nodos, su configuración funciona según lo previsto y podrá ejecutar tanto comandos _ad hoc_ como libretos en sus nodos mediante Ansible.

## Guías

Las siguientes guías (en idioma inglés) explican cómo utilizar los libretos que encontrará en este repositorio.

### Initial Server Setup

- [Initial Server Setup for Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-18-04)

Una vez se haya completado la configuración inicial del servidor, podrá elegir cualquiera de las guías de configuración (en idioma inglés) de servidor disponibles:

### Servidores web

- [Apache on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-apache-on-ubuntu-18-04)
- [LEMP (Linux, Nginx, MySQL, PHP) on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-lemp-on-ubuntu-18-04)
- [LAMP (Linux, Apache, MySQL, PHP) on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-lamp-on-ubuntu-18-04)

### Aplicaciones y mandejadores de contenido

- [WordPress with LAMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-wordpress-with-lamp-on-ubuntu-18-04)

### Contenedores & Kubernetes

- [Docker on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-docker-on-ubuntu-18-04)

