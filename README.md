# ansible-deploy

Proyecto de vagrant / ansible para el despligue de las máquinas necesarias para mi entorno de desarrollo

## Requirements
* Virtual Box
* Vagrant
* Ansible
 
Es necesario crear el directorio

    /mnt/datos/deploy
    
en la máquina local, que es punto de montaje compartido entre el host, y las máquinas virtuales

## Redmine

Instala una máquina con redmine, para gestión de tareas, wiki y etc.
Periodicamente, hace copia de seguridad de la base de datos, y del código en:

    /mnt/datos/deploy/backup/redmine

Para levantar la máquina: 

    vagrant up redmine

## Monitoring

Instala una máquina con el stack ELK (ElasticSearch, Logstash y Kibana), para monitorizar el resto de proyectos.
Para enviar logs, a esta máquina, es necesario aplicar y configurar el rol

    filebeat
    
filebear, envia los archivos de logs, desde una máquina, a monitoring    
    

Para levantar la máquina: 

    vagrant up monitoring
    
    
## Website

Instala una máquina con el stack Lemp (Linux, nginx, y mysql), para proyectos web.
Incluye:

    - openresty   
    - java 
    - elasticsearch 
    - varnish 
    - mysql 
    - redis 
    - php 
    - php-xdebug 
    - composer 
    - blackfire 
    - nodejs 

Todo configurado para funcionar "out the box"

Para levantar la máquina: 

    vagrant up website
    
    
    
