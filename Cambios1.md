# optixTutorial

### Cambios hasta el tutorial 4

En el archivo tutorial4.cu se muestra el código con los cambios que realicé hasta el tutorial 4. Estos se describen a continuación.

#### Ray generation  

En términos de la generación de los rayos, se usa la función de generación de rayos *pinhole_camera()*, la cual se deja igual que el código original, aunque se podría cambiar la orientación de la escena al cambiar el orden de los argumentos de la función normalize al dejarla como `normalize(d.y*U + d.x*V + W)`, lo cual generaría el efecto de girar la escena 90° grados.


#### Closest hit

En términos de los programas tipo closest hits, se generan unas sombras y colores al intersectarse los rayos generados con la geometría. Esto se programa en la función *RT_PROGRAM void floor_closest_hit_radiance4()*. En esta función es importante configurar la dirección de las normales para que vayan en dirección del origen del rayo con *-ray.direction* en la función *faceforward*. También, en este programa se puede configurar el color de ambiente que tendrán los objetos al presentarse la intersección con los rayos. En el código se modifica la línea #163 para establecer un color claro `float3 color = Ka * (1.f, 1.f, 1.f)`. Adicionalmente, se cambia también el color reflectividad en la línea de código #205. 

### Miss

En términos del programa tipo Miss, se modifica el color de fondo en la línea de código #83. Este color se genera cuando los rayos no han intersectado ninguna geometría en la escena.

![imagen](https://raw.githubusercontent.com/wilmerodriguez/optixTutorial/original.PNG)
