# Docker en Ubuntu 18.04

[Leer en Castellano (LEEME.md)](./LEEME.md)

Este manual le guiará en la instalación de Docker en un equipo con Ubuntu 18.04, tal y como se explica en la guía en inglés sobre
[How to Use Ansible to Install and Set Up Docker on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-docker-on-ubuntu-18-04).
Se crearán varios contenedores con las opciones especificadas en el archivo de variables `vars/default.yml`.

## Configuración

- `create_containers`: Número de contenedores a crear.
- `default_container_name`: Nombre por defecto para los contenedores nuevos.containers.
- `default_container_image`: Imagen por defecto para los contenedores nuevos.containers.
- `default_container_command`: Comando por defecto para los contenedores nuevos.containers.


## Ejecución de este libreto

Primeros pasos:

### 1. Descargar el libreto

```shell
git clone https://github.com/ks7000/ansible-playbooks.git
cd ansible-playbooks/docker_ubuntu1804
```

### 2. Personalizar opciones

```shell
nano vars/default.yml
```

```yml
#vars/default.yml
---
create_containers: 4
default_container_name: docker
default_container_image: ubuntu
default_container_command: sleep 1d
```

### 3. Ejecutar el libreto

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulta esta guía en inglés: [How to Use Ansible to Install and Set Up Docker on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-docker-on-ubuntu-18-04).