# Utilizando Clamav Antivirus en GNU Linux OpenSuse

Siempre ha sido un eje de debate si existen o no los códigos maliciosos (virus, gusanos, etc.) para GNU/Linux , sea cierto o falso, lo verdadero es que siempre es conveniente tener un buen antivirus instalado en el sistema y más si se se ocupa como servidor de correo o servidor de archivos para otros sistemas operativos, sin un antivirus estaremos esparciendo código malicioso por la organización sin darnos cuenta.

Un antivirus es un programa que detecta cierta actividad sospechosa en la computadora, como el acceso a un disco de almacenamiento, la firma de un código malicioso en memoria o un intento para borrar o modificar un archivo, etc.

Hoy día existen varias opciones de antivirus para Linux, siendo ClamAv antivirus (www.clamav.net) una de las más reconocidas y utilizadas, por ofrecer las siguientes características:

Open source GNU Public License version 2
Escaneo rápido (fast scanning)
POSIX compatible
Detecta aprox 1 millon de virus, gusanos y troyanos incluyendo los virus de macro de microsoft Office, malware, etc.
Escaneo dentro de archivos comprimidos. (zip,rar, 7zip, arj,tar,gzip,bzip2, sfx, cab, etc)
Los dos comandos básicos para empezar a utilizar este antivirus son freshclam y clamscan. El primero actualiza la base de datos de definiciones de códigos maliciosos y el segundo escanea los archivos en su búsqueda.

Lo primero que debe hacerse antes de escanear cualquier archivo o directorio, es actualizar la lista de definiciones de virus.

NOTA: Si un antivirus no tiene actualizada su lista de definiciones, es totalmente inservible.

Para actualizar las definiciones ejecutamos el siguiente comando como root

    # freshclam
  
como un usuario sin privilegios esto se ejecuta de la siguiente forma:

    $ sudo root freshclam
  


Bien ya una vez que actualizamos las definiciones podemos proceder a escanear con el comando clamscan de la siguiente manera:

   clamscan [options] [filename or directory]
  
Por ejemplo para escanear un archivo ejecutable de Windows llamado IPEYE.EXE utilizamos el siguiente comando:

   $ clamscan IPEYE.EXE
  
Cuando ClamAv encuentra un código malicioso en el archivo escaneado, muestra el nombre del código entre el nombre de este archivo y la palabra FOUND, tal como se muestra en la imagen.



Para escanear todos los archivos en el directorio actual, utilizamos el siguiente comando:

   $ clamscan
  


A manera de una guía rápida, aquí presento una lista de las opciones más útiles para utilizar ClamAV:

1) Para escanear todos los archivos desde la raíz, pero unicamente mostrar los archivos infectados y al detectar una amenaza hacer sonar una alerta.

    $ clamscan -r --bell -i /
   
2) para escanear todos los archivos dentro del directorio /home.

    $ clamscan -r /home
   
3) para escanear todos los archivos dentro del directorio /home/martin y mover los archivos infectados al directorio /home/martin/quarantine.

    $ clamscan -r --move=/home/martin/quarantine /home/martin 
   
4) para escanear todos los archivos del directorio /home/martin y eliminar los archivos infectados.

    $ clamscan -r /home/martin --remove
   
5) Para escanear todos los archivos dentro del directorio /home/martin y copiar los archivos al directorio /home/martin/quarantine.

    $ clamscan -r --copy=/home/martin/quarantine /home/martin
   
6) Para escanear los archivos línea a línea contenidos en un archivo de texto llamado: [files2scan.txt]

    $ clamscan -file-list=files2scan.txt
   
Es importante mencionar que ClamAV únicamente escaneara los archivos en donde el usuario tenga permisos, si se requiere un escaneo completo de todo el sistema se deberá ejecutar con una cuenta con permisos de superusuario.

Si tienes un virus no detectado por ClamAV incluso con la última actualización de sus definiciones, favor de envialo a la siguiente dirección: http://www.clamav.net/sendvirus
