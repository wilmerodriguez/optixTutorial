# optixTutorial

### Cambios hasta el tutorial 4

En el archivo tutorial4.cu se muestra el código con los cambios que realicé hasta el tutorial 4. Estos se describen a continuación.

#### Ray generation program  

En términos de la generación de los rayos, se usa la función de generación de rayos *pinhole_camera()*, la cual se deja igual que el código original, aunque se podría cambiar la orientación de la escena al cambiar el orden de los argumentos de la función normalize al dejarla como `normalize(d.y*U + d.x*V + W)`, lo cual generaría el efecto de girar la escena 90° grados.


#### Closest hit program

En términos de los programas tipo *closest hits*, se obtienen colores al intersectarse los rayos generados con la geometría más cercana. Esto se programa en la función *RT_PROGRAM void floor_closest_hit_radiance4()*. En esta función es importante configurar la dirección de las normales para que vayan en dirección del origen del rayo con *-ray.direction* en la función *faceforward*. También, en este programa se puede configurar el color de ambiente que tendrán los objetos al presentarse la intersección con los rayos. En el código se modifica la línea #163 para establecer un color claro (`float3 color = Ka * (1.f, 1.f, 1.f)`). Adicionalmente, se cambia también el color reflectividad en la línea de código #205. 

#### Miss program

En términos del programa tipo *Miss*, se modifica el color de fondo en la línea de código #83. Este color se genera cuando los rayos no han intersectado ninguna geometría en la escena.

#### Any hit program

En términos del programa *any hit*, se modifica el color de atenuación de la sombra en la línea de código #93. Este color se genera cuando los rayos se intersectan con los objetos de la escena y no interesa tener en cuenta las superficies más cercanas al rayo, como sí sucede con el programa tipo *closest hit*. Este valor de atenuación hará que la sombra generada se vea más clara u oscura según sea el caso. Adicionalmente, se puede quitar la sombra si se cambia el valor de profundidad *max_depth* a 0, que originalmente es de 100, en la línea de código #197. 

En las siguientes imágenes se pueden observar los cambios realizados.

#### Imagen original
![imagen original](https://github.com/wilmerodriguez/optixTutorial/blob/master/original.PNG)

#### Imagen modificada
![imagen modificada](https://github.com/wilmerodriguez/optixTutorial/blob/master/modificada.PNG)
