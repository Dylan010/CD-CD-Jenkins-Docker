
# Proyecto CD-CD-Jenkins-Docker

Este repositorio contiene un ejemplo de implementación continua (CI/CD) utilizando Jenkins y Docker para una aplicación Flask simple. El proyecto incluye un `Dockerfile` para construir la imagen del contenedor, un `Jenkinsfile` para la configuración del pipeline en Jenkins, y una aplicación Flask que se muestra en la página principal.

## Estructura del Proyecto

.
├── app.py
├── DESAFIO_13.pdf
├── Dockerfile
├── Jenkinsfile
├── README.md
├── requirements.txt
└── templates
    └── index.html

## Requisitos

1. **Docker**: Asegúrate de tener Docker instalado en tu sistema. Puedes seguir las instrucciones en [Docker Installation](https://docs.docker.com/get-docker/).

2. **Jenkins**: Debes tener Jenkins instalado y configurado en tu entorno. Consulta [Jenkins Installation](https://www.jenkins.io/doc/book/installing/) para obtener detalles sobre cómo instalar y configurar Jenkins.

3. **Credenciales de DockerHub**: Necesitarás credenciales de DockerHub para poder subir imágenes a tu repositorio. Puedes obtenerlas registrándote en [DockerHub](https://hub.docker.com/).

4. **Git**: Asegúrate de tener Git instalado para clonar el repositorio. Más información en [Git Installation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## Pasos para Ejecutar el Proyecto

1. **Clonar el Repositorio**

   Clona el repositorio en tu máquina local utilizando Git:

   ```bash
   git clone https://github.com/Dylan010/CD-CD-Jenkins-Docker.git
   cd CD-CD-Jenkins-Docker
   ```

2. **Configurar Docker**

   - Asegúrate de tener Docker en funcionamiento.
   - Construye la imagen de Docker con el siguiente comando:

     ```bash
     docker build -t dy010101/desafio-13:latest .
     ```

3. **Configurar Jenkins**

   - Asegúrate de que Jenkins esté instalado y en funcionamiento.
   - Crea una nueva tarea en Jenkins y elige "Pipeline".
   - En la sección "Pipeline", selecciona "Pipeline script from SCM" y configura el repositorio Git con la URL del repositorio y las credenciales necesarias.
   - Define el script de Jenkins en el campo correspondiente. Puedes utilizar el `Jenkinsfile` proporcionado en el repositorio.

4. **Ejecutar el Pipeline en Jenkins**

   - Ejecuta el pipeline manualmente o deja que se ejecute automáticamente según el cron programado en el `Jenkinsfile` (todos los días a las 2 AM).
   - El pipeline realizará las siguientes acciones:
     - **Checkout**: Obtendrá el código fuente desde el repositorio Git.
     - **Build Docker Image**: Construirá la imagen Docker.
     - **Test**: Ejecutará un contenedor para verificar que la aplicación funciona.
     - **Push to DockerHub**: Subirá la imagen Docker a DockerHub.
     - **Deploy**: Desplegará la aplicación actualizada.

5. **Acceder a la Aplicación**

   Una vez que el contenedor esté en funcionamiento, puedes acceder a la aplicación en [http://localhost:5000](http://localhost:5000).

## Adaptar el Proyecto

Para que otros usuarios puedan replicar tu código, ellos deben:

1. **Actualizar las Credenciales de DockerHub**

   En el `Jenkinsfile`, asegúrate de que el ID de credenciales `dockerhub-credentials` sea actualizado con las credenciales de DockerHub del usuario.

2. **Modificar el Nombre de Imagen y el Tag**

   Cambia las variables `IMAGE_NAME` y `IMAGE_TAG` en el `Jenkinsfile` si desean utilizar un nombre y un tag diferentes para la imagen Docker.

3. **Actualizar el Archivo `Dockerfile`**

   Asegúrate de que el `Dockerfile` esté configurado correctamente para las necesidades específicas de su aplicación. Pueden modificar las instrucciones del `Dockerfile` según sea necesario.

4. **Actualizar el Archivo `requirements.txt`**

   Añade o elimina dependencias en el archivo `requirements.txt` para que se ajusten a las necesidades de su aplicación.


