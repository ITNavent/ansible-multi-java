Multi-Java
=========

Ansible role to install multiple version o Java in the same system.

Requirements
------------


- Ubuntu
- Ansible 2.6
- wget


Role Variables
--------------
Ejemplo minimo:

```
mj_java_packages_java_version: "8u131" # si pisas el list 'mj_java_packages' esta variable deja de tener validez

```
Ejemplo mas chico:

```
mj_pre_shell_commands="supervisorctl stop user-postings-store" 

mj_java_packages:
  - 
    mj_java_version: "11.0.2"
  - 
    mj_nexus_java_version: "8u131"
    
mj_post_shell_commands="supervisorctl start user-postings-store"

```
Ejemplo mas completo:

```
#general
mj_java_download_base_url: "http://nexus.navent.biz:8081/nexus/service/local/repositories/releases/content/com/navent/java"
mj_relative_java_base_dir: "java"
mj_download_dir: "/tmp/java"
mj_alternatives_decreasing_start_priority: 256 # cada alternative tiene una prioridad y este role comienza a a asignarlas desde este numero de el 1er package de la lista hasta el ultimo, y va decreciendo
mj_java_package_file_ext_default: "gz"
mj_package_binary_relative_subpath_default: "bin/java"
mj_clean_java_dir_default: true
mj_clean_java_alternative_default: true
mj_reset_all_java_alternatives: true
mj_force_java_installation: false # sirve para forzar a que se instalen los packages de Java aunque ya este instalada la misma version que se quiere instalar


#default-java-package
mj_java_packages_java_version: "8u131" # si pisas el list 'mj_java_packages' esta variable deja de tener validez
mj_java_packages_java_package_file_ext: "gz"
mj_java_packages_clean_java_dir: true
mj_java_packages_clean_java_alternative: true

#java-packages (podes sobreescribir este list y agregar todos los packages que quieras)
mj_java_packages:
  - 
    mj_java_version: "{{mj_java_packages_java_version}}" # Forma alternativa de descarga 1, siempre y cuando el nombre del artefacto siga el patron 'java-{version_java}.{extension_archivo}' en su nombre de archivo en Nexus.
    mj_java_package_file_ext: "{{mj_java_packages_java_package_file_ext}}" # opcional (tiene valor default)
    mj_clean_java_dir: "{{mj_java_packages_clean_java_dir}}" # opcional (tiene valor default)
    mj_clean_java_alternative: "{{mj_java_packages_clean_java_alternative}}" # opcional (tiene valor default)
    mj_package_binary_relative_subpath: "jre/bin/java" # opcional (tiene valor default)
  # mj_java_dir_symlink_name: java-symlink # opcional (se genera de forma automatica)
  #-
  #  mj_java_download_url: "https://openjdk.org/..." # Forma alternativa de descarga 2, podes poner directamente la URL a un package comprimido que contenga los archivos de Java (no tendrias que especificar 'mj_java_version').
  #  mj_clean_java_dir: true

```

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: multi-java, mj_java_packages_java_version: 8u131 }

```

Author Information
------------------

Augusto Mendoza (amendoza@navent.com)

