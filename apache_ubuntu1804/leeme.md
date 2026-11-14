# Apache en Ubuntu 18.04

Este libreto instalará el servidor web Apache 2 en un equipo con Ubuntu 18.04, tal y como se explica en la guía (en idioma inglés) [How to Use Ansible to Install and Configure Apache on Ubuntu 18.04] (https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-apache-on-ubuntu-18-04). Se creará un host virtual utilizando las opciones especificadas en el archivo de variables `vars/default.yml`.

## Configuración

- `app_user`: Un usuario remoto que no sea usuario **root** en el anfitrión de Ansible y que será el propietario de los archivos de la aplicación.
- `http_host`: Su nombre de dominio.
- `http_conf`: El nombre del archivo de configuración que se creará en Apache.
- `http_port`: Puerto HTTP; el valor por defecto es 80.
- `disable_default`: Si se debe desactivar o no el sitio web predeterminado de Apache. Cuando se establece en `true` su nuevo host virtual se utilizará como sitio web predeterminado. El valor por defecto es `true`.

## Ejecución de este libreto

Pasos rápidos:

### 1. Obtener el libreto

```shell
git clone https://github.com/ks7000/ansible-playbooks.git
cd ansible-playbooks/apache_ubuntu1804
```

### 2. Personalizar opciones

```shell
nano vars/default.yml
```

```yml
#vars/default.yml
---
app_user: "sammy"
http_host: "your_domain"
http_conf: "your_domain.conf"
http_port: "80"
disable_default: true
```

### 3. Ejecutar el libreto

```command
ansible-playbook -l [target] -i [inventory file] -u [remote user] playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulte esta guía en inglés: [How to Use Ansible to Install and Configure Apache on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-apache-on-ubuntu-18-04).
