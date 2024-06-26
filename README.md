# Contenerización de una aplicación
En esta practica, se procederá a contenerizar una aplicación. Durante el proceso, se trabajará con un gestor de listas de tareas básico que opera en Node.js.

## Requisitos

* Se debe tener instalada la última versión de Docker Desktop.
* Se ha de contar con un cliente Git instalado.
* Se necesita un IDE o editor de texto para editar archivos. Docker recomienda el uso de Visual Studio Code.
  
En resumen, se empaquetará la aplicación utilizando Docker y se trabajará con ella utilizando las herramientas mencionadas anteriormente.

## Obtener la aplicación

1) Clonar el repositorio getting-started-app usando el comando:
   
| git clone https://github.com/docker/getting-started-app.git |
|-------------------------------------------------------------|

<p align="center">
  <img src="Imagenes/1.jpg" alt="Imagen 1">
</p>

2) Ver el contenido del repositorio clonado. Debería ver los siguientes archivos y subdirectorios

<p align="center">
  <img src="Imagenes/2.jpg" alt="Imagen 2">
</p>

   
## Construir la imagen de la aplicación

Un Dockerfile es como una receta de cocina para crear una imagen de contenedor. Es un archivo de texto que contiene una serie de instrucciones que Docker utiliza para construir automáticamente una imagen Docker. Especifica qué software y configuraciones se deben incluir en la imagen, así como cómo se deben configurar y ejecutar. Una vez que tienes un Dockerfile, Docker puede usarlo para construir una imagen de contenedor de manera consistente y reproducible.

1) Entrar en el repositorio clonado y crear un archivo vacío llamado Dockerfile
   
| cd /path/to/getting-started-app |
|-------------------------------------------------------------|
   
| touch Dockerfile |
|-------------------------------------------------------------|
   
<p align="center">
  <img src="Imagenes/3.jpg" alt="Imagen 3">
</p>

2) En un editor de codigo agregamos el siguiente codigo al archivo Dockerfile

<p align="center">
  <img src="Imagenes/4.jpg" alt="Imagen 4">
</p>

3) Se construye la imagen usando el comando:

| docker build -t getting-started . |
|-----------------------------------|

<p align="center">
  <img src="Imagenes/5.jpg" alt="Imagen 5">
</p>

<p align="center">
  <img src="Imagenes/6.jpg" alt="Imagen 6">
</p>

Cuando se ejecuta el comando `docker build`, Docker utiliza el Dockerfile proporcionado para construir una nueva imagen. Si la imagen base especificada en el Dockerfile no está disponible localmente, Docker la descarga automáticamente. Luego, Docker sigue las instrucciones del Dockerfile, copiando los archivos de la aplicación, instalando dependencias (en este caso, usando `yarn`), y configurando el comando predeterminado que se ejecutará al iniciar un contenedor a partir de esta imagen (especificado por la directiva `CMD`).

La bandera `-t` permite etiquetar la imagen con un nombre que elijas, haciéndola fácilmente identificable. En este caso, la imagen se etiqueta como "getting-started". Al final del comando, el "." indica que Docker debe buscar el Dockerfile en el directorio actual.

El comando `docker build` utiliza el Dockerfile para construir una imagen de contenedor, siguiendo las instrucciones especificadas en el Dockerfile y etiquetando la imagen resultante para facilitar su identificación.

## Iniciar un contenedor de aplicaciones

1) Ejecutar el comando:

| docker run -dp 127.0.0.1:3000:3000 getting-started |
|----------------------------------------------------|

<p align="center">
  <img src="Imagenes/7.jpg" alt="Imagen 7">
</p>

<p align="center">
  <img src="Imagenes/8.jpg" alt="Imagen 8">
</p>

La bandera `-d` (abreviatura de --detach) ejecuta el contenedor en segundo plano, lo que significa que Docker inicia el contenedor y lo devuelve al indicador de terminal. Se puede verificar que un contenedor esté en ejecución visualizándolo en Docker Dashboard en Containers o ejecutando `docker ps` en la terminal.

La bandera `-p` (abreviatura de --publish) crea una asignación de puertos entre el host y el contenedor. Toma un valor de cadena en el formato HOST:CONTAINER, donde HOST es la dirección en el host y CONTAINER es el puerto en el contenedor. El comando publica el puerto 3000 del contenedor en 127.0.0.1:3000 (localhost:3000) en el host. Sin la asignación de puertos, no se puede acceder a la aplicación desde el host.

2) Abrir en el navegador web el enlace:

| http://localhost:3000/ |
|------------------------|

3) Agregue uno o dos elementos y compruebe que funciona como espera. Puede marcar elementos como completos y eliminarlos. Su interfaz está almacenando elementos correctamente en el backend.

En este punto, tiene un administrador de lista de tareas pendientes en ejecución con algunos elementos.

Si echa un vistazo rápido a sus contenedores, debería ver al menos un contenedor ejecutándose que utiliza la getting-startedimagen y el puerto 3000. Para ver sus contenedores, puede utilizar la CLI o la interfaz gráfica de Docker Desktop.

<p align="center">
  <img src="Imagenes/9.jpg" alt="Imagen 9">
</p>

Ejecutar el siguiente comando en una terminal para enumerar sus contenedores.

| docker ps |
|------------------------|

# Actualizar la aplicación
En esta sección, se procederá a actualizar tanto la aplicación como la imagen asociada. Además, se aprenderá a detener y eliminar un contenedor en ejecución.

## Actualizar el código fuente
1) En el src/static/js/app.jsarchivo, se actualiza la línea 56.
   
<p align="center">
  <img src="Imagenes/11.jpg" alt="Imagen 11">
</p>

2) Crear la versión actualizada de la imagen. 

3) Inicie un nuevo contenedor usando el código actualizado.

| docker run -dp 127.0.0.1:3000:3000 getting-started |
|------------------------|

## Eliminar el contenedor creado anteriormente

1)Obtener el ID del contenedor con el comando:

| docker ps |
|-----------|

2) Utilizar el docker stop comando para detener el contenedor. Reemplazar <the-container-id>con el CONTAINER ID.

| docker stop <the-container-id> |
|--------------------------------|

<p align="center">
  <img src="Imagenes/13.jpg" alt="Imagen 13">
</p>

<p align="center">
  <img src="Imagenes/13.jpg" alt="Imagen 14">
</p>

3)Eliminar el contenedor detenido

<p align="center">
  <img src="Imagenes/15.jpg" alt="Imagen 15">
</p>

## Iniciar el contenedor de aplicaciones actualizado

1) Usar docker run para iniciar el contenedor
   
<p align="center">
  <img src="Imagenes/16.jpg" alt="Imagen 16">
</p>

<p align="center">
  <img src="Imagenes/17.jpg" alt="Imagen 17">
</p>

2) Abrir en el navegador web el enlace:
   
| http://localhost:3000/ |
|------------------------|

Se observa el cambio en el texto de la aplicación

 ### Antes
<p align="center">
  <img src="Imagenes/13.jpg" alt="Imagen 13">
</p>

 ### Despues
 <p align="center">
  <img src="Imagenes/18.jpg" alt="Imagen 18">
</p>

## Compartir la aplicación 

Ahora que ha creado una imagen, puede compartirla. Para compartir imágenes de Docker, debe utilizar un registro de Docker. El registro predeterminado es Docker Hub y es de donde provienen todas las imágenes que ha utilizado.

### Crear un repositorio

Para enviar una imagen, primero debe crear un repositorio en Docker Hub.

1. Regístrese o inicie sesión en Docker Hub .
2. Seleccione el botón Crear repositorio .
3. Para el nombre del repositorio, utilice getting-started. Asegúrese de que la visibilidad sea pública .
4. Seleccione Crear .

## Push en la imagen

1. Este comando enviará a este repositorio.

| docker push docker/getting-started:tagname |
|------------------------|

2. Inicie sesión en Docker Hub usando el comando
   
| docker login -u YOUR-USER-NAME |
|------------------------|

3. Utilice el docker tagcomando para darle a la getting-startedimagen un nuevo nombre. Reemplácelo YOUR-USER-NAMEcon su ID de Docker.

|  docker tag getting-started YOUR-USER-NAME/getting-started |
|------------------------|

4. Ahora ejecute el docker pushcomando nuevamente. Si está copiando el valor de Docker Hub, puede descartar la tagnameparte, ya que no agregó una etiqueta al nombre de la imagen. Si no especifica una etiqueta, Docker usa una etiqueta llamada latest.

| docker push YOUR-USER-NAME/getting-started |
|------------------------|

## Ejecute la imagen en una nueva instancia.
Ahora que su imagen se creó y se insertó en un registro, intente ejecutar su aplicación en una instancia nueva que nunca haya visto esta imagen de contenedor. Para hacer esto, utilizará Play with Docker.

| docker build --platform linux/amd64 -t YOUR-USER-NAME/getting-started . |
|------------------------|

1. Abra su navegador para Play with Docker.

2. Seleccione Iniciar sesión y luego seleccione la ventana acoplable en la lista desplegable.

3. Inicie sesión con su cuenta de Docker Hub y luego seleccione Iniciar .

4. Seleccione la opción AGREGAR NUEVA INSTANCIA en la barra lateral izquierda. Si no lo ve, amplíe un poco su navegador. Después de unos segundos, se abre una ventana de terminal en su navegador.
   
5. En la terminal, inicie su aplicación recién enviada.

| docker run -dp 0.0.0.0:3000:3000 YOUR-USER-NAME/getting-started |
|------------------------|

6. Seleccione la insignia 3000 cuando aparezca.

Si la insignia 3000 no aparece, puede seleccionar Abrir puerto y especificar 3000.




