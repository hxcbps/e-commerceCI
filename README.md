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



