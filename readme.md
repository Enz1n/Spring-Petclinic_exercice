# Spring Pet Clinic 

Este repositorio contiene una implementación lista para contenedores de la clasica aplicación Spring Petclinic. Específicamente, este código es útil con la tecnología OpenShift Source-to-Image (s2i) y es parte del material introductorio de [Developer Sandbox for Red Hat OpenShift](https://developers.rehat.com/developer-sandbox).



## Consola de desarrollo

Asegúrese de estar en la perspectiva de desarrollador:

![Dev Perspective](images/3-switch-perspective.png)

Y crear una nueva instancia de MySQL haciendo click en `+Add` y eligiendo la opcion: `Database`

![Add DB](images/4-db.png)

Escoger MySQL Ephemeral:

![MySQL Ephemeral](images/5-mysql-ephemeral.png)

Y hacer click en `Instantiate Template`.

A continuación, complete los espacios con los siguientes parámetros:

![MySQL Template](images/6-db-params.png)

Apretar el boton de  `Create` .

Estamos utilizando una implementación **Ephemeral** porque esta es una demostración de corta duración y no necesitamos retener los datos. 

En un sistema de producción, lo más probable es que utilice una instancia de MySQL permanente. Esto almacena los datos en un volumen persistente (básicamente un disco duro virtual), lo que significa que el pod de MySQL puede destruirse y reemplazarse con los datos que permanecen intactos.

### Desplegar la Pet Clinic App


Click the `+Add` button and choose `From Git` type:

Fill the git repo with the following value `https://github.com/redhat-developer-demos/spring-petclinic` and select the project as Java project:

![Pet Clinic Deploy](images/7-petclinic-deploy.png)

Apretar en `Build Configuration` 

![Build Configuration](images/8-build-config.png)

Añadir las siguientes variables de entorno :

```
SPRING_PROFILES_ACTIVE=mysql
MYSQL_URL=jdbc:mysql://mysql:3306/petclinic
```

![DC Env Vars](images/9-app-env-vars.png)

Finalmente apretar el boton `Create` y espere hasta que finalice la Build y el Pod esté en funcionamiento (azul oscuro alrededor de la burbuja de implementación).

Luego apretamos el boton de Open URL  para ver la Pet Clinic app:

![Pet Clinic Deployment](images/10-petclinic-url.png)


![Pet Clinic UI](images/11-output-ui.png)

Y si vamos a la Terminal de la implementación de MySQL, se peude conectar a la base de datos para ver el esquema y los datos.


```
mysql -u root -h mysql -p

petclinic

use petclinic;
show tables;
```

![MySQL Terminal](images/12-mysql-terminal-1.png)

```
select * from owners;
```

![MySQL Terminal](images/13-mysql-terminal-2.png)
`### End ###`
