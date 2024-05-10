### Ejercicio volumen montado

En este ejemplo vamos a ejecutar un contenedor Docker que montará la carpeta web y que por tanto, mostrará el contenido de la web.

Como la carpeta la tenemos en nuestro equipo, podemos editar y modificar la web mientras la probamos sobre el servidor web del contenedor. Es una solución muy adecuada cuando se desea desarrollar una aplicación web sin tener que instalar soluciones locales como Xampp y además podemos asegurarnos de trabajar con un entorno de ejecución idéntico al de producción.

## Procedimiento:
1.Nos ubicamos primero en la carpeta: cd "C:\Users\diegd.DIEGDAR-PC\OneDrive\FORMACION\Programacion\🐳Docker\Capsula Docker-Cibergnarium\CursDocker\01.VolumMuntat"

2.Primero, obtén la ruta del directorio actual utilizando el comando Get-Location.
Luego, combina la ruta obtenida con la ruta dentro del contenedor utilizando la concatenación de cadenas.
Finalmente, utiliza la ruta completa como argumento del volumen en el comando docker run.:
    $currentDir = Get-Location
    $volumeMountPath = "$currentDir\html:/usr/share/nginx/html"

    docker run -it --rm -v $volumeMountPath -p 80:80 nginx


