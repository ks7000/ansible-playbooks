# LEMP en Ubuntu 18.04


Este libreto instalará un entorno LEMP en un equipo con Ubuntu 18.04, tal y como se explica en la guía sobre
[How to Use Ansible to Install and Set Up LEMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-lemp-on-ubuntu-18-04).
Se creará un anfitrión virtual con las opciones especificadas en el archivo de variables `vars/default.yml`.


## Configuración

- `mysql_root_password`: La contraseña de la cuenta de usuario **root** de MySQL.
- `http_host`: Su nombre de dominio.
- `http_conf`: El nombre del archivo de configuración que se creará en Nginx.
- `http_port`: puerto HTTP; el valor predeterminado es 80.

## Ejecución de este libreto

Pasos rápidos:

### 1. Obtener el playbook

```shell
git clone https://github.com/ks7000/ansible-playbooks.git
cd ansible-playbooks/lemp_ubuntu1804
```

### 2. Personalizar las opciones

```shell
nano vars/default.yml
```

```yml
#vars/default.yml
---
mysql_root_password: "mysql_root_password"
http_host: "su_dominio"
http_conf: "su_dominio.conf"
http_port: "80"
```

### 3. Ejecutar el libreto

```command
ansible-playbook -l [destino] -i [archivo de inventario] -u [usuario remoto] playbook.yml
```

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consulta esta guía en idioma inglés: [How to Use Ansible to Install and Set Up LEMP on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-install-and-set-up-lemp-on-ubuntu-18-04).