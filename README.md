# e-commerce escalable y totalmente para Dockerizar
Integrantes del proyecto
* Dayan Fernando Fernandez Pacho 
* Fernando Tibaduiza Gutierrez
* Carlos Eduardo Jaramillo Franco

Esta aplicación se generó utilizando JHipster 6.9.0, puede encontrar documentación y ayuda en  [https://www.jhipster.tech/documentation-archive/v6.9.0](https://www.jhipster.tech/documentation-archive/v6.9.0).

## Desarrollo

Antes de poder construir este proyecto, debe instalar y configurar las siguientes dependencias en su máquina::

1. [Node.js][]:Usamos Node para ejecutar un servidor web de desarrollo y construir el proyecto.
    Dependiendo de su sistema, puede instalar Node desde la fuente o como un paquete preempaquetado.

Después de instalar Node, debería poder ejecutar el siguiente comando para instalar herramientas de desarrollo.
Solo necesitará ejecutar este comando cuando las dependencias cambien en [package.json](package.json).

    npm install

Utilizamos scripts npm y [Webpack][] como nuestro sistema de compilación

Ejecute los siguientes comandos en dos terminales separadas para crear una experiencia de desarrollo maravillosa donde su navegador
se actualiza automáticamente cuando los archivos cambian en su disco duro.

    ./gradlew -x webpack
    npm start

Npm también se usa para administrar las dependencias CSS y JavaScript que se usan en esta aplicación. Puede actualizar las dependencias especificando una versión más nueva en [package.json](package.json). También puedes correr `npm update` y `npm install` para gestionar dependencias.
Añada el `help` marca en cualquier comando para ver cómo puedes usarlo. Por ejemplo, `npm help update`.

El `npm run` El comando enumerará todos los scripts disponibles para ejecutar para este proyecto.

### Soporte PWA

JHipster viene con soporte PWA (Progressive Web App), y está desactivado por defecto. Uno de los componentes principales de una PWA es un trabajador de servicio.

El código de inicialización del trabajador de servicio está comentado de manera predeterminada. Para habilitarlo, descomente el siguiente código en`src/main/webapp/index.html`:

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('./service-worker.js').then(function () {
      console.log('Service Worker Registered');
    });
  }
</script>
```

### Administrar dependencias

Por ejemplo, para agregar [Leaflet][] biblioteca como una dependencia de tiempo de ejecución de su aplicación, ejecutaría el siguiente comando:

    npm install --save --save-exact leaflet

Para beneficiarse de las definiciones de tipo de TypeScript de [DefinitelyTyped][] repositorio en desarrollo, ejecutarías el siguiente comando:

    npm install --save-dev --save-exact @types/leaflet


### Using Angular CLI

También puedes usar [Angular CLI][] para generar un código de cliente personalizado.

Por ejemplo, el siguiente comando:

    ng generate component my-component

generará pocos archivos:

    create src/main/webapp/app/my-component/my-component.component.html
    create src/main/webapp/app/my-component/my-component.component.ts
    update src/main/webapp/app/app.module.ts


## Uso de Docker para primera entrega

Usar Docker para mejorar la experiencia de desarrollo del JHipster. Hay varias configuraciones de docker-compose disponibles en el proyecto [src/main/docker](src/main/docker) esta carpeta tiene los punto a punto de Docker construidos para nuestro ambiente

Por ejemplo, para iniciar una base de datos mysql en un contenedor docker, ejecutamos:

    docker-compose -f src/main/docker/mysql.yml up -d

Para detenerlo y eliminar el contenedor, ejecutamos:

    docker-compose -f src/main/docker/mysql.yml down

También dockerizamos completamente nuestra aplicación y todos los servicios de los que depende.
Para lograr esto, primero creamos una imagen acoplable de la aplicación ejecutando:

    ./gradlew bootJar -Pprod jibDockerBuild

Entonces ejecutamos 

    docker-compose -f src/main/docker/app.yml up -d
	
## Uso de Jhipster para la segunda entrega

JHipster nos ofrece un conjunto de herramientas para desarrollar y diseñar los elementos correspondientes al frontend y también al backend de un proyecto de desarrollo. Por ejemplo, el framework Spring Boot es la base más adecuada para obtener un robusto stack de Java del lado del servidor que nos permita conectarnos a varias bases de datos, motores de virtualización y herramientas de seguimiento. Para conectarse al frontend, utiliza una interfaz REST. A continuación, puedes encontrar algunas de las opciones disponibles del lado del servidor en JHipster:

Para poder acceder a estas multivariadas herramientas, debemosacceder al cmd con beneficios de administrador, posteriomente nos dirigimos a la carpeta raiz de nuestro proyecto y desde alli ya escribiendo Jhipster ya podremos acceder a los items de configuracion los cuales queramos adicionar a nuestro e-commerce

-Bases de datos: MariaDB, PostgreSQL, Oracle, MySQL, MongoDB
-Virtualización: Docker, Kubernetes, AWS
-Entornos de ejecución de pruebas: Karma, Cucumber
-Indexación: ElasticSearch
-Cachés: Ehcache, Infinispan
-Sistemas de monitorización: Prometheus

Adjuntamos el enlace de una guia practica para conocer la creacion de un proyecto de desarrollo con estas caracteristicas

https://www.ionos.es/digitalguide/paginas-web/desarrollo-web/jhipster/


## Uso de Jenkins para la segunda entrega
Jenkins basicamente es un servidor de integración continua de código abierto, Jenkins funciona a base de tareas donde se pueden administrar lo que se hará en un build, como programar cada cuanto tiempo revise nuestro repositorio de versionamiento o que haga un despliegue a otro servidor, entre otras cosas.
Otras alternativas usualmente usadas son: Travis CI, Codeship, CircleCI, etc.
Para usar Jenkins necesitas, java8, 256mb de ram, y 1gb de espacio de disco duro.

1. Descargarlo desde su sitio web oficial: https://jenkins.io/
2. Una vez descargado procedemos a descomprimirlo y ejecutar el sistema de instalación.
3. Una vez instalado lo abrimos:
- - Jenkins por defecto corre en el puerto 8080, para acceder a el solo debemos escribir la direccion en el navegador: `http://localhost:8080/`
- - Podremos ver la pagina de login, donde introduciremos nuestros datos o crearemos un usuario.

## Configurar Jenkins
1. Primero agregaremos las credenciales a Jenkins, esta nos servita para dar permisos a configuraciones posteriores. Ingresamos los datos que se nos piden y damos clic en OK.
2. Luego descargaremos los Plugins necesarios para que se comunique con GitHub. En el panel de control damos click en:
- -  Manage Jenkins -> Maneje Plugins.
3. Seleccionamos y descargamos los Plugins, en la pestaña Available encontramos los que están disponibles para la descarga. Seleccionamos cualquier opción para comenzar la descarga e instalación.
4. Crear una nueva tarea para construir la solución,
- - En el panel principal de Jenkins seleccionamos la opción New Item.
5. Escribimos el nombre de la tarea y seleccionamos de la opción Crear un proyecto de estilo libre. Y damos clic en OK.
6. Configurar la nueva tarea para que se comunique con GitHub.
- - Colocamos una descripción a la tarea y seleccionamos la opción de GitHub Project en donde colocaremos la URL del repositorio creado en GitHub.
7. Configuramos el origen del código fuente con los datos con la URL del repositorio de GitHub y la credencial que ya habíamos creado.
8. Seleccionamos las opciones disparadores de ejecución, marcamos la opción ejecutar periódicamente, en donde agregaremos los parámetros para indicar cada cuanto tiempo revise si existe un cambio y en un lapso de cuantas horas.
9. Seleccionamos guardar y esperamos que se construya la primera solución.
10. En el panel principal se muestran las tareas que hemos agregado y el estado en el que se encuentra.
11. Damos clic en Construir ahora para que se compile y genere el ejecutable de nuestra aplicación.


## Documentacion Travis

Travis-CI es un sistema de Integración Continua, gratuita para proyectos Open Source y de pago para proyectos privados. Se integra sin problemas con GitHub y automáticamente ejecuta el pipeline definido en cada push o pull requests. Testea y buildea aplicaciones escritas en Ruby, Node, Objective-C, Go, Java, C# y F#, entre otras (que corran en Linux).

Posee su propia “Deploy engine” la cual permite a los desarrolladores testear por completo sus aplicaciones para luego realizar exitosamente el deploy sin sorpresas. Travis-CI tiene un proveedor para Azure Web Apps, que permiten combinar GitHub y Travis-CI con Azure para realizar los deploys automáticos.

Si bien es similar a Jenkins, tiene sus diferencias. No utiliza tareas programadas, no tiene costos de mantenimiento (esta hosteado como servicio),el setup es “simple”, entre otras.

##Repositorio

Lo primero que necesitas es tener to código en un repositorio. Si tu proyecto es open source, puedes usar Github y dejarlo libre sin costo, y eso te permite usar la versión Open de Travis, para repositorios públicos.

##Conectar Travis CI a tu repositorio

Una vez tengas tu repo creado, dirígete a Travis-CI e inicia sesión con tu cuenta de Github, esto permite a Travis ver tu lista de repos. Busca el que quieres configurar y activalo con el switch a verde y despues clicka en settings.

En las settings te recomiendo que actives las opciones Build pushed branches y Build pushed pull requests para que Travis se ejecute en las PR que generes o te envíe y tambien cuando éstas sean aceptadas y mergeadas a master.

##Fichero de configuración

Aquí es donde entra la magia. Con un simple fichero que llamaremos .travis.yml y alojaremos en la raiz de nuestro proyecto, vamos a decirle a Travis lo que vamos a hacer.

Ahora ya sabes como configurar Travis en tu proyecto para tener CI/CD (Integración y Despliegue contínuos) de manera que los tests se ejecuten cuando se abra una pull request, y una vez la aceptemos y Travis de el OK, poderla mergear en master y desplegar los cambios en producción o el entorno que elijas.



