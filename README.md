# u2vpodcast-lxc
Prepara la aplicación u2vpodcast (https://github.com/atareao/u2vpodcast) para funcionar sobre contenedores LXC o máquinas virtuales utilizando recetas **Ansible**. La rama escogida de u2vpodcast es la rama **axum**.

He creado una receta de ansible que traduce el docker compose que propone el desarrollador de u2vpodcast y por lo tanto se puede aplicar a maquinas virtuales o contenedores LXC.


## Requisitos

### config.yml
Debes tener creado un archivo de configuración. Puedes ver uno de ejemplo en config-ejemplo.yml

### cookies.txt

Debes crear un archivo de cookies.txt. En este enlace puedes ver como ser prepara: [https://github.com/atareao/u2vpodcast?tab=readme-ov-file#how-do-you-cookies-to-work](https://github.com/atareao/u2vpodcast?tab=readme-ov-file#how-do-you-cookies-to-work)

### Maquinas o contenedores LXC

Es necesario tener dos máquinas: 
 - builder-axum
    - Sistema: Debian 11
    - RAM: 1 GB
    - Disco 8 GB
    - Funcionalidad: máquina que descarga el código fuente y compila la aplicación.
 - u2vpodcast-axum: 
    - Sistema: Alpine Linux v3.18
    - RAM: 128 MB
    - Disco: 8GB (más si vas a descargar muchos audios).
    - Funcionalidad: corre la app u2vpodcast en el puerto **6996**.

Ambas tienen que poder ser atacadas a través de **Ansible**. Debes copiar la clave pública SSH del central node de Ansible desde el que vas a lanzar la receta. Además tienen que tener instalado python.


Modifica inventario.yml para especificar el direccionamiento IP a tu gusto.


### Roles necesarios
Es necesario tener descargado el rol de Rust 1.70 para Debian 11 disponible en [https://github.com/danimedin/rust_role#](https://github.com/danimedin/rust_role#) 

La ruta donde hay que descargar los archivos del rol está especificada en el fichero playbook.yml (variable ruta_rust)


## Como lanzo la receta

ansible-playbook -i inventario.yml playbook.yml