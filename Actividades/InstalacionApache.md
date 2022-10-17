# Como instalar el servidor web Apache en Ubuntu
## Qué es Apache y cómo funciona
Apache es un servidor web HTTP de código abierto. Está desarrollado y mantenido por una comunidad de usuarios en torno a la Apache Software Foundation.
Actualmente y desde el 1996 es el servidor web más usado en todo el mundo debido a su seguridad y estabilidad.
La funcionalidad principal de este servicio web es servir a los usuarios todos los ficheros necesarios para visualizar la web.
## Instalar Apache
El primer paso que debemos realizar será abrir el terminal de ubuntu para a continuación empezar con los comandos para la instalación.  
**Importante** -> Actualizar
```
sudo apt update
```
Una vez ha terminado de actualizarse podemos empezar la instalación
```
sudo apt install apache
```
## Ajustar el firewall
Antes de empzar con Apache será necesario modificar los ajustes de firewall para permitir el acceso externo a los puertos web predeterminados
```
sudo ufw app list
```
Habilitaremos el tráfico en el puerto 80 (Apache) y activaremos el cortafuegos y verificaremos que el cambio se haya realizado
```
sudo ufw allow 'Apache'
sudo ufw enable
sudo ufw status
```
##Comprobar su servidor web
En este paso el servidor web ya estara activo.  
Vamos a realizar una verificación con el sistema `systemd` para saber si se encuentra en ejecución el servicio.  
```
sudo systemctl status apache2
```
Si el sistema te indicara que esta incativo, realizar el siguiente comando;
```
sudo systemctl start apache2
```
Una vez comprobamos que el servicio esta en ejecución, para conocer la dirección IP de nuestro servidor introduciremos el siguiente comando y desde nuestro navegador verificaremos que podemos acceder a la página predeterminada de Apache
```
hostname -I
http://_yourServerIP_
```
##Administrar el proceso de Apache
**Detener el servidor**
```
sudo systemctl stop apache2
```
**Iniciar servidor**
```
sudo systemctl start apache2
```
**Reiniciar el servidor**
```
sudo systemctl restart apache2
```
**Recargar sin cerrar las conexiones**
```
sudo systemctl reload apache2
```
**Deshabilitar Apache para que no se inicie automaticamente**
```
sudo systemctl disable apache2
```
**Habilitar el servicio para que se cargue en el inicio**
```
sudo systemctl enable apache2
```
# Como configurar el servidor web Apache en Ubuntu
## Creando nuestra propia web
Para empezar vamos a crear una carpeta para nuestra web dentro de _/var/www/_  
En este caso le hemos llamado _prueba_ pero puedes llamar a la carpeta como quieras.
```
sudo mkdir /var/www/prueba/
```
Ahora que tenemos el directorio creado para nuestra web, vamos a crear un HTML dentro de esta
```
cd /var/www/prueba
sudo nano index.html
```
Dentro de el archivo HTML que hemos creado, como de momento es una prueba, pondremos un pequeño código HTML.
## Configuración del archivo de configuración de VirtualHost
Vamos a empezar yendo al directorio donde estan almaccenados los archivos de configuración.
```
cd /etc/apache2/sites-available/
```
`Dato:`Apache viene configurado predeterminadamente con un archivo VirtualHost (lo utilizaremos como base)
`Recuerda:`En este caso hemos llamado al archivo de configuración _prueba_ para que coincida con el nombre de nuestro proyecto.
```
sudo cp 000-default.conf prueba.conf
```
A continuación editaremos el archivo _prueba.conf_
```
sudo nano prueba.conf
```
Dentro de este fichero añadiremos las siguientes lineas de código
```
ServerAdmin yourname@example.com
DocumentRoot /var/www/prueba/
ServerName prueba.example.com
```
* **ServerAdmin**: Los usuarios de Apache te pueden buscar en el caso de que hubiera algun problema.
* **DocumentRoot**: Directiva para apuntar la ruta donde estan alojados los archivos de nuestra web.
* **ServerName**: Garantiza que las personas lleguen al sitio correcto en lugar del predeterminado.
Después de configurar nuestro sitio web, debemos activar el archivo de configuración de hosts virtuales para habilitarlo.
```
sudo a2ensite prueba.conf
```
`Dato:` En el caso de que no hayas activado la nueva configuración te pedira que la actualices -> _sudo systemctl reload apache2_
  
Para acabar, comprueba buscando en el navegador tu _**ServerName**_.
