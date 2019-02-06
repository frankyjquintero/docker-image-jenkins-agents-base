Jenkins Agent Docker image Base
===


Esta es una imagen base para Docker, que incluye OpenJDK 8 y el ejecutable del agente Jenkins (slave.jar).
Este ejecutable es una instancia de la [biblioteca de Jenkins Remoting] (https://github.com/jenkinsci/remoting).

## Uso
Esta imagen se utiliza como base para la imagen del [Agente JNLP de Docker] (https://github.com/jenkinsci/docker-jnlp-slave/).
En esa imagen, el contenedor se inicia externamente y se adjunta a Jenkins.

En su lugar, esta imagen se puede usar para iniciar un agente utilizando el ** Método de lanzamiento ** de ** Agente de lanzamiento a través de la ejecución del comando en el maestro **. Prueba por ejemplo

```sh
docker run -i --rm --name agent --init jenkins/slave java -jar /usr/share/jenkins/slave.jar
```

después de configurar **Directorio raíz remoto** para `/home/jenkins/agent`.

### Directorios de trabajo de los Agentes

A partir de [Remoting 3.8] (https://github.com/jenkinsci/remoting/blob/master/CHANGELOG.md#38) hay un soporte de directorios de trabajo,
que proporciona el registro de forma predeterminada y cambia el comportamiento del almacenamiento en caché de JAR.

Call example:

```sh
docker run -i --rm --name agent1 --init -v agent1-workdir:/home/jenkins/agent jenkins/slave java -jar /usr/share/jenkins/slave.jar -workDir /home/jenkins/agent
```

## Configuraciones

La imagen tiene varias configuraciones compatibles, a las que se puede acceder a través de las siguientes etiquetas:

* `alpine`: Small image based on Alpine Linux (based on `openjdk:8-jdk-alpine`)

Solo se utilizara la version [alpine] basada en la oficial
https://github.com/jenkinsci/docker-slave/


