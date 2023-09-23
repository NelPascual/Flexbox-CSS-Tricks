# Traducción de la Guía completa de Flexbox de CSS-Tricks

**Por Chris Coyier**

Nuestra guía completa sobre el diseño con CSS Flexbox. Esta guía completa explica todo sobre Flexbox, centrándose en todas las diferentes propiedades posibles para el elemento padre (el ``flex container``) y los elementos hijos (los ``flex items``). También incluye historia, demos, patrones y una tabla de compatibilidad con los navegadores.

## Tabla de contenidos

[Parte 1: Introducción](#introducción)

[Parte 2: Conceptos básicos y terminología](#conceptos-básicos-y-terminología)

[Parte 3: Propiedades de Flexbox](#propiedades-de-flexbox)

* [Propiedades del padre (flex container)](#propiedades-del-padre)

    * [display](#display)
    * [flex-direction](#flex-direction)
    * [flex-wrap](#flex-wrap)

Parte 4: Prefijos Flexbox

Parte 5: Ejemplos

Parte 6: Trucos Flexbox

Parte 7: Compatibilidad con navegadores

Parte 8: Bugs

Parte 9: Propiedades relacionadas

Parte 10: Más información

Parte 11: Más fuentes

## Introducción

El módulo Flexbox Layout (Caja flexible) tiene como objetivo proporcionar una forma más eficiente de disponer, alinear y distribuir el espacio entre los elementos de un contenedor, incluso cuando su tamaño es desconocido y/o dinámico (de ahí la palabra "flex").

La idea principal detrás del diseño flexible es dar al contenedor la capacidad de alterar el ``width``/``height`` de sus elementos (y el orden) para llenar mejor el espacio disponible (sobre todo para adaptarse a todo tipo de dispositivos de visualización y tamaños de pantalla). Un contenedor flexible expande los elementos para llenar el espacio libre disponible o los encoge para evitar el desbordamiento.

Y lo que es más importante, el flexbox layout es independiente de la dirección, a diferencia de los diseños habituales (bloque, que se basa en la vertical, e inline, que se basa en la horizontal). Si bien funcionan para las páginas, carecen de flexibilidad (sin juego de palabras) para soportar aplicaciones grandes o complejas (especialmente cuando se trata de cambiar la orientación, cambiar el tamaño, estirar, encoger, etc.).

Nota: El Flexbox Layout es más apropiado para los componentes de una aplicación y los diseños a pequeña escala, mientras que el diseño Grid está pensado para diseños a mayor escala.

## Conceptos básicos y terminología

Dado que Flexbox es un módulo completo y no una sola propiedad, implica un montón de cosas, incluyendo todo su conjunto de propiedades. Algunas de ellas están destinadas a ser establecidas en el contenedor (elemento padre, conocido como ``flex container``), mientras que las otras están destinadas a ser establecidas en los hijos (llamados ``flex items``).

Si la maquetación "normal" se basa tanto en direcciones de flujo en bloque como en línea, el flex layout se basa en "flex-flow directions". Eche un vistazo a esta figura de la especificación, en la que se explica la idea principal de la distribución flexible.

![Gráfico flujo de Flexbox](../Flexbox%20CSS%20Tricks/img/flexbox-basic-terminology.svg "flex-flow directions")

Los elementos se dispondrán siguiendo el eje principal o ``main axis`` (de ``main-start`` a ``main-end``) o el eje transversal o ``cross axis`` (de ``cross-start`` a ``cross-end``).

* __``main axis``__ - El ``main axis`` de un contenedor flex es el eje principal a lo largo del cual se disponen los elementos flex. Cuidado, no es necesariamente horizontal; depende de la propiedad ``flex-direction`` (ver más abajo).

* __``main-start``__ | ``main-end`` - Los elementos flexibles se colocan dentro del contenedor empezando por ``main-start`` y llegando hasta ``main-end``.
* __``main size``__ - El ``width`` o el ``height`` de un elemento flexible, cualquiera que esté en la dimensión principal, es el tamaño principal del elemento. La propiedad de ``main size`` del ``flex item`` es la propiedad '``width``' o '``height``', la que se encuentre en la dimensión principal.

* __``cross axis``__ - El eje perpendicular al ``main axis`` se denomina ``cross axis``. Su dirección depende de la dirección del ``main axis``.

* __``cross-start`` | ``cross-end``__ - Las ``flex lines`` se llenan de ítems y se introducen en el contenedor comenzando por el lado del ``cross-start`` del contenedor flexible y avanzando hacia el lado de ``cross-end``.

* __``cross size``__ - El ``width`` o el ``height`` de un ``flex item``, cualquiera que esté en la dimensión transversal, es el tamaño transversal del elemento. La propiedad ``cross size`` es cualquiera de '``width``' o '``height``' que se encuentre en la dimensión transversal.

## Propiedades de Flexbox

![Propiedades del padre](../Flexbox%20CSS%20Tricks/img/flex-container.svg "Flex container")

## Propiedades del padre

### ``display``

Define un ``flex container``; _inline_ o _block_ dependiendo del valor dado. Habilita un contexto flex para todos sus hijos directos.

```css
.container {
    display: flex; /* o inline-flex */
}
```

Tenga en cuenta que las columnas CSS no tienen ningún efecto en un contenedor flexible.

### ``flex-direction``

![Flex direction](../Flexbox%20CSS%20Tricks/img/flex-direction.svg "flex-direction")

Esto establece el ``main-axis``, definiendo así la dirección en la que se colocan los ``flex items`` en el ``flex container``. Flexbox es (aparte del envoltorio opcional) un concepto de diseño unidireccional. Piensa que los ``flex items`` se colocan principalmente en filas horizontales o columnas verticales.

```css
.container {
    flex-direction: row | row-reverse | column | column-reverse;
}
```
* ``row`` (default): de izquierda a derecha en ltr; de derecha a izquierda en rtl
* ``row-reverse``: de derecha a izquierda en ltr; de izquierda a derecha en rtl
* ``column``: igual que la fila pero de arriba a abajo
* ``column-reverse``: igual que la inversión de filas, pero de abajo a arriba

### ``flex-wrap``

![Flex-wrap](../Flexbox%20CSS%20Tricks/img/flex-wrap.svg "flex-wrap")

Por defecto, todos los elementos flex intentarán caber en una línea. Puede cambiar esto y permitir que los items se ajusten según sea necesario con esta propiedad.

```css
.container {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

* ``nowrap`` (default): todos los flex items estarán en una línea
* ``wrap``: Los flex items se envolverán en varias líneas, de arriba abajo.
* ``wrap-reverse``: los flex items se envolverán en varias líneas de abajo a arriba.

Hay algunas [demostraciones visuales de flex-wrap aquí](https://codepen.io/NPascual/pen/rNoJQYy).