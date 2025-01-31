﻿# TomcatMaven
﻿# TomcatMaven
## 1. Tomcat
 Instalar OpenJDK
```bash
sudo apt install -y openjdk-11-jdk
```


Instalar Tomcat 9
```bash
sudo apt install -y tomcat9
sudo groupadd tomcat9
sudo useradd -s /bin/false -g tomcat9 -d /etc/tomcat9 tomcat9
sudo systemctl start tomcat9
sudo systemctl status tomcat9
```
<img src="capturas/1_instalacion.png"/>
<img src="capturas/2_instalacion.png"/>
<img src="capturas/3_instalacion.png"/>
<img src="capturas/4_TomcatNavegador.png"/>



# 1.1. Configuración de la administración
Edita el archivo /etc/tomcat9/tomcat-users.xml:
```bash
sudo nano /etc/tomcat9/tomcat-users.xml
<role rolename="admin"/>
<role rolename="admin-gui"/>
<role rolename="manager"/>
<role rolename="manager-gui"/>
<user username="alumno" password="1234" roles="admin,admin-gui,manager,manager-gui"/>

```
 Instalar el administrador web
 ```bash
sudo apt install -y tomcat9-admin
 ```
edita el archivo /usr/share/tomcat9-admin/host-manager/META-INF/context.xml
 ```bash
<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="\d+\.\d+\.\d+\.\d+" />
 ```
 ```bash
sudo systemctl restart tomcat9
 ```
<img src="capturas/5_Usuarios.png"/>
<img src="capturas/6_tomcat9-admin.png"/>
<img src="capturas/7_tomcat9-admin.png"/>
<img src="capturas/8_manager.png"/>
<img src="capturas/9_manager.png"/>
<img src="capturas/10_war.png"/>
<img src="capturas/11_war.png"/>
<img src="capturas/12_war.png"/>

## 2 Instalación y configuración de Maven
 ```bash
sudo apt-get update && sudo apt-get -y install maven
mvn --version

 ```
En /etc/tomcat9/tomcat-users.xml, se añade:
 ```bash
<role rolename="manager-script"/>
<user username="deploy" password="1234" roles="manager-script"/>
 ```
Edita /etc/maven/settings.xml y se añade:
 ```bash
<servers>
    <server>
        <id>Tomcat</id>
        <username>deploy</username>
        <password>1234</password>
    </server>
</servers>
 ```
# 2.1. Generar una aplicación de prueba
 ```bash
mvn archetype:generate -DgroupId=org.example -DartifactId=tomcat-war -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
 ```
 ```bash
<build>
    <finalName>tomcat-war-deployment</finalName>
    <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
                <url>http://localhost:8080/manager/text</url>
                <server>Tomcat</server>
                <path>/despliegue</path>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```
# 2.2. Despliegue con Maven
 ```bash
mvn tomcat7:deploy
 ```
<img src="capturas/13_maven.png"/>
<img src="capturas/14_maven.png"/>
<img src="capturas/15__usuarios_maven.png"/>
<img src="capturas/16__usuarios_maven.png"/>
<img src="capturas/18_maven.png"/>
<img src="capturas/19_maven.png"/>
<img src="capturas/20_maven.png"/>
<img src="capturas/21_maven.png"/>
<img src="capturas/22_maven.png"/>
<img src="capturas/22_1_maven.png"/>
<img src="capturas/23_maven.png"/>
<img src="capturas/24_maven.png"/>

# 3 TAREA

Clonar el repositorio
 ```bash
cd ~
git clone https://github.com/cameronmcnz/rock-paper-scissors.git
 ```

Cambia al directorio del proyecto descargado:

 ```bash
cd rock-paper-scissors
 ```
Cambiar de rama
```bash
git checkout patch-1
```
Configurar Maven para el despliegue

Modificar el archivo pom_2.xml, y añadirlo en nuestro vagrantfile.
```bash
<plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
    <configuration>
        <url>http://localhost:8080/manager/text</url>
        <server>Tomcat</server>
        <path>/desplieguetarea</path>
    </configuration>
</plugin>

```
Guardamos y continuar con el despliegue

```bash
mvn tomcat7:deploy
```
Nos aparecera esto en http/localhost:8080/desplieguetarea

<img src="capturas/26.png"/>
