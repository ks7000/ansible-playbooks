# LAMP en Ubuntu 18.04

Esta guía instalará un entorno LAMP (**L**inux, **A**pache, **M**ySQL y **P**HP) en una máquina con Ubuntu 18.04 , tal como se explica en la guía en inglés: [How to Use Ansible to Install and Configure LAMP on Ubuntu 18.04](#). Se creará un anfitrión virtual con las opciones especificadas en el archivo de variables `vars/default.yml`

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
git clone https://github.com/do-community/ansible-playbooks.git
cd ansible-playbooks/lamp_ubuntu1804
```

### 2. Configurar preferencias

```shell
nano vars/default.yml
```

```yml
---
mysql_root_password: "mysql_root_password"
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

Para obtener más información sobre cómo ejecutar esta configuración de Ansible, consultar esta guía: [(en construcción)]().