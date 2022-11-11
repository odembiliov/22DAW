# Práctica SSH
## PC Servidor
### Crear un usuario nuevo y activar servidor SSH
Crearemos un usuarios y le daremos permisos de super usuario, para ello utilizaremos los siguientes comandos:
```
sudo adduser nombreUsuario
sudo usermod -aG sudo nombreUsuario
```
A continuación iniciaremos SSH y buscaremos nuestra IP
```
sudo systemctl start ssh
ifconfig
```
## PC Cliente
### EAcceder al servidor mediante SSH
Con el usuario que hayamos creado anteriormente utilizaremos el siguiente comando añadiendo la IP del servidor
```
 ssh nombreUsuario@IP_server
```
Ejemplo del resultado:  
![](https://lh4.googleusercontent.com/TNsVTUC0cZELaz4gkRVRkzdJ1steWeVl0OZgFnN9ImzW6cQ8fzxVSbBUbao7YH0JxEY=w2400)

### Instalación Apache en el servidor
```
sudo apt install apache2
```
Para seguir con la parte de configuración visitar los siguientes links:  
[Link 1](https://github.com/Sebi16/Portfolio_DAW/edit/main/Ejercicios/Apache.md)  
[Link 2](https://github.com/odembiliov/UD1-GitHub-y-MarkDown/blob/main/Actividades/InstalacionApache.md)  
[Link 3]()  
Una vez realizada la configuración el resultado final debe poder dejarnos entrar en la página por defecto de Apache indicandonos que funciona correctamente.
![](https://lh6.googleusercontent.com/EkLnHS4MUgv2FCAyIICw4MH-9dhSr0GIaDu1nGuanYg3rEACEn9CHF2qdNxh34zxyXo=w2400)
### Pasa una web a algún lugar del servidor
Para pasar una pagina web lo primero deberemos configurar el archivo de configuración de VirtualHost.
### Configuración del archivo de configuración de VirtualHost
Empezaremos yendo al directorio donde estan almacenados los archivos de configuración.
```
cd /etc/apache2/sites-available/
```
`Dato:`Apache viene configurado predeterminadamente con un archivo VirtualHost (lo utilizaremos como base)
`Recuerda:`En este caso hemos llamado al archivo de configuración _prueba_ para que coincida con el nombre de nuestro proyecto.
```
sudo cp 000-default.conf practica.conf
```
A continuación editaremos el archivo _practica.conf_
```
sudo nano practica.conf
```
Dentro de este fichero añadiremos las siguientes lineas de código
```
ServerAdmin yourname@example.com
DocumentRoot /var/www/practica/
ServerName practica.example.com
```
En el caso de que nos saliera el siguiente problema, modificaremos los hosts.  
![](https://www.desarrollolibre.net/public/images/example/apache/sitio-caido.png?ezimgfmt=rs:300x225/rscb1/ng:webp/ngcb1)
### Modifica los host del local para que con la dirección elegida vaya a la ip del servidor
Para modificar los hosts deberíamos ir al siguiente directorio y modificar el archivo hosts.
```
cd /etc/hosts
sudo nano hosts
```
Dentro del archivo hosts deberemos agregar nuestro dominio.
```
127.0.0.1 practica.example.com
IP_server practica.example.com
```
Ahora si navegamos a nuestro dominio podremos visualizar nuestra página.
![](https://lh4.googleusercontent.com/ySvXjjaQJqoquzbNBg5hu7l_w5Yw8L7BIWXcx7RqLimRBo5DZXWZqcU3OKkSbY9iwb8=w2400)
