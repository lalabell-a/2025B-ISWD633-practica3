# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado o utilizó otros comandos que no se mencionan al realizar la práctica también se debe documentar.

## Antes de la práctica

Antes de esta práctica, ya tuve experiencias previas con los conceptos que aplicamos en las practicas pasadas: contenedores, imagenes, redes, variables de entorno, base de datos, etc. 

El conocimiento de la gestion de contenedores en Docker y la ejecución de comandos básicos, unión de redes, conectar distintos contenedores y demás. Las variables de entorno se usaron en casos sumamente básicos. Si bien configuramos contenedores que se pueden comunicar mediantes redes, no se profundizo tanto. 


## Luego de la práctica

Estaba un poco confundida respecto a las diferencias de cómo escribir los comandos y que me ofrecía cada uno: descubrí que -mount es la opción recomendada de Docker al ser más explicito y seguro, a su vez que permite más funciones. Mientras -v ofrece facilidad de escritura pero tiene limitaciones o puede traer lugar a ciertas ambiguedades al tener una sintaxis menos clara. 

Un bind mount, ¿Qué hace exactamente? esta línea (--mount type=bind,source=C:\nginx\html,target=/usr/share/nginx/html) Docker monta la carpeta del host en el punto de montaje del contenedor. En palabras simples, lo que hay en el host se muestra dentro del contenedor de esta ruta. Por ello aparece el error 403, en realidad, este sucede en tres escenarios (si no hay index.html, si no tiene permisos de lecturas o si es una pantalla en blanco).

Tal y como en la práctica pasada, cuando se eliminó el contenedor de wordpress y se volvió a crear. Se hizo lo mismo acá, solo que esta vez no estaba conectado a otro contenedor sino que este apuntaba a una dirección de host, Bind Mount mantiene los datos persistentes fuera del contenedor.

Se entendió el concepto de los volumenes nombrados (almacenado en una ubicación especifica en el sistema de archivos del host) y los anonimos (creados automaticamente cuando ejecutas un contenedor). Estos ayudan a que los datos persistan aunque elimines los contenedores, tal como pasa si lo guardases en una base de datos.

Un problema encontrado fue que en mi primer intento no cargaba los datos de PostgreSQL o Drupal porque la ruta del volumen estaba mal escrita (`/var/lipostgresql/data` en lugar de `/var/lib/postgresql/data`), una corrección sencilla. 

Hubo problemas con puertos y puertos mapeados duplicados (nginx vs WordPress), se solucionó eliminando el contenedor que ya no necesitabamos en ese momento para dejar el puerto libre. Eso sí, en caso de necesitar el puerto, la solución es poner el segundo contenedor con un puerto cercano para que no haya un choque. 