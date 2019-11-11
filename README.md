# La Parrilla de Rosendo
Rosendo tiene una parrilla y nos pidió un sistema para administrar el menú de su reciente parrilla.

## 1. Comidas
Nos piden modelar los distintos platos que ofrece la parrilla. De cada uno de ellos nos interesa conocer:
* su **peso**, medido en gramos;
* si es **apto vegetariano**;
* su **valoración**, un número que indica qué tan bueno es el plato;
* si **es abundante**, lo cual es cierto cuando su peso es mayor a 250 gramos.

Consideraremos inicialmente estos platos:

### Provoleta
Cada provoleta tiene un peso diferente. Se debe informar además si **tiene especias** y si **es completa** (o sea, con jamón y morrones). La provoleta común es _apta vegetariano_, mientras que la completa no. 

Su _valoración_ es de 120 puntos si es especial, y de 80 en caso contrario. Decimos que una provoleta es especial cuando se cumple alguna de estas condiciones:
* _es abundante_ y _tiene especias_;
* o _es completa_. 

### Hamburguesas de carne
Su _peso_ es siempre de 250 gramos y lógicamente no son _aptas para vegetariano_. 
A cada hamburguesa se le configura su pan, y la _valoración_ del plato se calcula como `60 + valoración del pan`. Los panes posibles son:
* **industrial** otorga 0 puntos;
* **casero** otorga 20 puntos;
* **de masa madre** otorga 45 puntos.

### Hamburguesas vegetarianas
Se comportan igual que las hamburguesas de carne, con tres diferencias:
* son _aptas para vegetariano_;
* para cada hamburguesa, se informa de qué legumbre está hecha (por ejemplo: `"lentejas"` o `"garbanzos"`);
* a la valoración se le suma otro plus, que se calcula como `2 * cantidad de letras del nombre de la legumbre`. Por ejemplo, si es de lentejas (que tiene 8 letras) el plus será de 16. 

Chusmear la [Wollok Doc](https://www.wollok.org/documentacion/wollokdoc/), los strings comparten varios métodos con las colecciones. :wink:

### Parrillada
Para cada parrillada se nos indica los cortes de carne pedidos. De cada corte se conoce su _calidad_ (un número) y su _peso_.

El _peso_ de la parrillada es la suma de los pesos de sus cortes. No es _apto vegetariano_. La _valoración_ se calcula como `15 * máxima calidad de sus cortes - cantidad de cortes`, y no puede dar un resultado negativo.

## 2. Comensales
Nos piden agregar al modelo a los comensales. De los comensales nos interesa saber si _le agrada una commida_, esto depende de su gusto culinario:
- A los **vegetarianos** les agradan las comidas que son aptas vegetariano y tienen una valoración mayor a 85.
- A los de **hambre popular** simplemente les agradan las comidas abundantes.
- A los **exquisitos** les agradan las comidas que pesan entre 150gr y 300gr, y además tengan una valoración mayor a 100.

Por ahora nos piden modelar estos tipos de comensales, sabiendo que es posible que se agreguen más en el futuro.

## 3. Menú
Se quiere agregar al modelo un menú, que tiene _todas las comidas_ que se ofrecen en la parrilla. Se quiere conocer
- La _comida más valiosa_ del menú. Esta es la que tiene mayor valoración.
- Saber si el menú _tiene alguna comida liviana_. O sea, alguna que pese menos de 100gr.
- Saber si el menú está _libre de maltrato animal_. Esto significa que todas sus comidas son aptas vegetariano.
- Conocer todas las comidas que _le gustan a un comensal_.

También se pide **poder elegir un plato** del menú para un comensal. Por ahora es cualquier plato que le guste. Si no le gusta ningún plato del menú entonces se debería lanzar un error específico.


## 5. Secreto parrillero
Por último, se nos pide agregar a Rosendo al sistema para saber cómo queda su parrilla luego de cocinar para un grupo de comensales. Esto significa, al recibir colección de comensales:
- Tomar sus pedidos, o sea, que elijan un plato del menú.
- Cocinarlos todos: el secreto de Rosendo es dejar las comidas en la parrilla un rato más para que _se tuesten_. 
Al tostar una comida, todas ellas reaccionan aumentando su valoración un 50%. Pero además, el asado pierde sus cortes con calidad de 1 o menos (porque se queman).

El sistema debe poder determinar cómo queda la parrilla (o sea, las comidas) luego de recibir a un conjunto de comensales.

## 6. BONUS: Criterios de hambre
A Rosendo le gustaría extender el sistema por el cual un comensal elige una comida del menú. Sigue mantieniendo que debe ser una comida que le guste, pero por lo general no eligen cualquiera al azar, sino que tenemos los siguientes patrones:
- Los **hambrientos** elijen, entre las comidas del menú que le gustan al comensal, la primera abundante.
- Los **glotones** elijen, entre las comidas del menú que le gustan al comensal, la más pesada
- Los **memoriosos** elijen, entre las comidas del menú que le gustan al comensal, la que pidieron la última vez. Pero si es la primera que va, o la comida no se encuentra en el menú (porque la sacaron o porque le dejó de gustar), elije cualquiera (y la recuerda, obviamente).
