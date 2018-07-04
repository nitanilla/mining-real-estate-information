# proyectoMateCompu
Auto-Organización Crítica


Pila de arena de una dimensión


Sea un arreglo unidimensional de L columnas de granos de arena con alturas hi. En cada columna definimos su pendiente local como


si=hi−hi+1


Definimos también la pendiente crítica sc: La pila es inestable si si>sc, para cualquier columna i.


La regla de actualización (dinámica), es: Si la pila es inestable, si>sc, entonces hi→hi−1 y hi+1→hi+1+1. Esto se debe de hacer de manera sincrónica en todas las columnas. Si la pila es estable, agrega un grano de arena a una columna al azar.
Muestra la evolución. Prográmalo como un autómata celular.


Hint Para los extremos considera dos escenarios: Pared fija o bordes abiertos (como si se cayeran de la mesa). ¿En que cambia la simulación?


Pila de arena de dos dimensiones


Una pila de arena más real es de tres dimensiones. En el artículo Bak, Tang and Wiesenfel Self-organized criticality: An explanation of the 1f noise, Phys. Rev. Lett. 59, 381(1987) los autores modelaron una pila de arena mediante un autómata celular de dos dimensiones.


En este modelo, se construye un arreglo de dos dimensiones en el que cada celda es una columna de arena.
Implemente el modelo, haga simulaciones en una pila de 200×200. Muestre varios patrones para cada nivel de estados inestables.


Explique el concepto de self-organized criticality. Muestre los datos que soportan su explicación.


Incendio forestal


En Bak, Chen and Tang A forest-fire model and some thoughts on turbulence,  Phys. Lett. A 147, 297-300 (1990), los autores crearon un autómata celular probabilístico para modelar como se esparce el fuego en un bosque. El bosque es modelado en un cuadrado de lado L en el que cada celda es un árbol que puede estar en tres estados: vivo(verde), quemándose (amarillo) y muerto (negro).


La evolución se determina como sigue:


En el tiempo t se determina el estado de cada celda, en t+1 se aplican las tres reglas:


  1. Si el árbol está vivo se verifican sus vecinos. Si _algún_ vecino está en llamas el árbol se quema.
  2. Si el árbol está en llamas, pasa a muerto.
  3. Si el árbol está muerto, se regenera con una probabilidad $p$.
  4. 
  
Reproduzca los resultados del artículo, en particular la longitud de la correlación ξ(p)
