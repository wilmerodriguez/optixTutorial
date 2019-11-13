# optixTutorial

## Primeros cambios

En el archivo [cambios1.cu](https://github.com/wilmerodriguez/optixTutorial/blob/master/cambios1.cu) se muestra el código con los cambios que realicé hasta el tutorial 4. Estos se describen a continuación.

#### Ray generation program  

En términos de la generación de los rayos, se usa la función de generación de rayos *pinhole_camera()*, la cual se deja igual que el código original, aunque se podría cambiar la orientación de la escena al cambiar el orden de los argumentos de la función *normalize* al dejarla como `normalize(d.y*U + d.x*V + W)`, lo cual generaría el efecto de girar la escena 90° grados.


#### Closest hit program

En términos de los programas tipo *closest hits*, se obtienen colores al intersectarse los rayos generados con la geometría más cercana. Esto se codifica en los programas *RT_PROGRAM void closest_hit_radiance3()* y *RT_PROGRAM void floor_closest_hit_radiance4()*. En esta función es importante configurar la dirección de las normales para que vayan en dirección del origen del rayo con *-ray.direction* en la función *faceforward*. También, en este programa se puede configurar el color de ambiente que tendrán los objetos al presentarse la intersección con los rayos. En el código se modifica la línea #163 para establecer un color claro (`float3 color = Ka * (1.f, 1.f, 1.f)`). Adicionalmente, se cambia también el color reflectividad en la línea de código #205. 

#### Miss program

En términos del programa tipo *Miss*, se modifica el color de fondo en la línea de código #83. Este color se genera cuando los rayos no han intersectado ninguna geometría en la escena.

#### Any hit program

En términos del programa *any hit*, se modifica el color de atenuación de la sombra en la línea de código #93. Este color se genera cuando los rayos se intersectan con los objetos de la escena y no interesa tener en cuenta las geometrías más cercanas al origen del rayo, como sí sucede con el programa tipo *closest hit*. Este valor de atenuación hará que la sombra generada se vea más clara u oscura según sea el caso. Adicionalmente, se puede quitar la sombra si se cambia el valor de profundidad *max_depth* a 0, que originalmente es de 100, en la línea de código #197. 

En las siguientes imágenes se pueden observar los cambios realizados.

#### Imagen original
![imagen original](https://github.com/wilmerodriguez/optixTutorial/blob/master/original.PNG)

#### Imagen modificada
![imagen modificada](https://github.com/wilmerodriguez/optixTutorial/blob/master/modificada.PNG)

## Segundos cambios

En el archivo [Cambios_optixTutorial.cpp](https://github.com/wilmerodriguez/optixTutorial/blob/master/Cambios_optixTutorial.cpp) se muestra el código con los cambios realizados hasta el tutorial 8. Estos se describen a continuación.


#### Bounding Box

En términos del programa tipo *Bounding Box*, se crea una nueva geometría basada en la caja original. Este programa calcula los límites de una primitiva para habilitar estructuras de aceleración, que construyen geometrías, en las intersecciones encontradas del ray tracing pipeline. La nueva geometría creada se llama *box2* y se crea con diferentes valores en los límites *boxmin* y *boxmax* en las líneas de código #274 - 279:
```
Geometry box2 = context->createGeometry();
box2->setPrimitiveCount(1u);
box2->setBoundingBoxProgram(box_bounds);
box2->setIntersectionProgram(box_intersect);
box2["boxmin"]->setFloat( 0.0f, 1.0f, -8.0f);
box2["boxmax"]->setFloat( 4.0f, 5.0f, -4.0f);
```

Adicionalmente se deben cambiar los valores en las líneas de código #432, #439 y #442 para relacionar esta nueva geometría a la escena. También, se cambia la altura de la caja original en la línea de código #271 como sigue: `box["boxmax"]->setFloat(  2.0f, 10.0f,  2.0f )`.

Finalmente, se cambia el color para las ranuras en la textura de la geometría del paralelogramo, que sería el piso de la escena. Se usa el color verde para las ranuras de las baldosas en la línea de código #396 así: `floor_matl["crack_color"]->setFloat(0.1f, 1.0f, 0.1f)`.

#### Imagen original

![](https://github.com/wilmerodriguez/optixTutorial/blob/master/original2.PNG)

#### Imagen modificada

![](https://github.com/wilmerodriguez/optixTutorial/blob/master/modificada2.PNG)
