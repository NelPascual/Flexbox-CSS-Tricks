# Traducción de la Guía Completa de Flexbox de CSS-Tricks

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
    * [flex-flow](#flex-flow)
    * [justify-content](#justify-content)
    * [align-items](#align-items)
    * [align-content](#align-content)
    * [gap, row-gap, column-gap](#gap-row-gap-column-gap)
* [Propiedades para los hijos (flex items)](#propiedades-para-los-hijos)

    * [order](#order)

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

![Gráfico flujo de Flexbox](/img/flexbox-basic-terminology.svg "flex-flow directions")

Los elementos se dispondrán siguiendo el eje principal o ``main axis`` (de ``main-start`` a ``main-end``) o el eje transversal o ``cross axis`` (de ``cross-start`` a ``cross-end``).

* __``main axis``__ - El ``main axis`` de un contenedor flex es el eje principal a lo largo del cual se disponen los elementos flex. Cuidado, no es necesariamente horizontal; depende de la propiedad ``flex-direction`` (ver más abajo).

* __``main-start``__ | ``main-end`` - Los elementos flexibles se colocan dentro del contenedor empezando por ``main-start`` y llegando hasta ``main-end``.
* __``main size``__ - El ``width`` o el ``height`` de un elemento flexible, cualquiera que esté en la dimensión principal, es el tamaño principal del elemento. La propiedad de ``main size`` del ``flex item`` es la propiedad '``width``' o '``height``', la que se encuentre en la dimensión principal.

* __``cross axis``__ - El eje perpendicular al ``main axis`` se denomina ``cross axis``. Su dirección depende de la dirección del ``main axis``.

* __``cross-start`` | ``cross-end``__ - Las ``flex lines`` se llenan de ítems y se introducen en el contenedor comenzando por el lado del ``cross-start`` del contenedor flexible y avanzando hacia el lado de ``cross-end``.

* __``cross size``__ - El ``width`` o el ``height`` de un ``flex item``, cualquiera que esté en la dimensión transversal, es el tamaño transversal del elemento. La propiedad ``cross size`` es cualquiera de '``width``' o '``height``' que se encuentre en la dimensión transversal.

## Propiedades de Flexbox

![Propiedades del padre](/img/flex-container.svg "Flex container")

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

![flex-direction](/img/flex-direction.svg "flex-direction")

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

![flex-wrap](/img/flex-wrap.svg "flex-wrap")

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

### ``flex-flow``

Es una abreviatura de las propiedades ``flex-direction`` y ``flex-wrap``, que definen conjuntamente los ejes principal (``main axis``) y transversal (``cross axis``) del ``flex container's``. El valor por defecto es ``row nowrap``.

```css
.container {
    flex-flow: column wrap;
}
```

### ``justify-content``

![justify-content](img/justify-content.svg "justify-content")

Define la alineación a lo largo del ``main axis``. Ayuda a distribuir el espacio libre sobrante cuando todos los ``flex items`` de una línea son inflexibles, o son flexibles pero han alcanzado su tamaño máximo. También ejerce cierto control sobre la alineación de los items cuando desbordan la línea.

```css
.container {
    justify-content: flex-start | flex-end | start | end | left | right | center | space-between | space-around - space-evenly;
}
```

* __``flex-start``__ (default): los items se posicionan hacia el inicio del ``flex-direction``.
* __``flex-end``__: los items se colocan hacia el final del ``flex-direction``.
* __``start``__:  los items se colocan hacia el principio de la dirección del modo de escritura.
* __``end``__: los items se colocan hacia el final de la dirección del modo de escritura.
* __``left``__:  los items se colocan hacia el borde izquierdo del contenedor, a menos que no tenga sentido con el ``flex-direction``, entonces se comporta como ``start``.
* __``right``__: los items se colocan hacia el borde derecho del contenedor, a menos que no tenga sentido con el ``flex-direction``, entonces se comporta como ``end``.
* __``center``__: los items se centran a lo largo de la línea.
* __``space-between``__: los items se distribuyen uniformemente en la línea; el primer item está en la línea de inicio, el último en la línea final.
* __``space-around``__: los items están distribuidos uniformemente en la línea con el mismo espacio a su alrededor. Tenga en cuenta que visualmente los espacios no son iguales, ya que todos los items tienen el mismo espacio a ambos lados. El primer item tendrá una unidad de espacio contra el borde del contenedor, pero dos unidades de espacio entre el siguiente item porque ese siguiente item tiene su propio espaciado que se aplica.
* __``space-evenly``__: los items se distribuyen de modo que el espacio entre dos items cualesquiera (y el espacio hasta los bordes) sea igual.

También hay dos palabras clave adicionales que puedes emparejar con estos valores: ``safe`` e ``unsafe``. El uso de ``safe`` garantiza que, independientemente de cómo se realice este tipo de posicionamiento, no se puede empujar un elemento de forma que se muestre fuera de la pantalla (por ejemplo, en la parte superior) de tal manera que el contenido no se pueda desplazar también (lo que se denomina "pérdida de datos").

### ``align-items``

![align-items](img/align-items.svg)

Define el comportamiento por defecto para la disposición de los flex-items a lo largo del ``cross-axis`` en la línea actual. Piense en ello como la versión ``justify-content`` para el ``cross-axis`` (perpendicular al ``main-axis``).

```css
.container {
    align-items: stretch | flex-start | start | self-start | flex-end | end | self-end | center | baseline;
}
```

* __``stretch``__ (default): estira los items para llenar el contenedor (respetando ``min-width``/``max-width``)
* __``flex-start``__ / __``start``__ / __``self-start``__: los items se colocan al principio del ``cross-axis``. La diferencia entre ambos es sutil, y consiste en respetar las reglas de ``flex-direction`` o las reglas del modo de escritura.
* __``flex-end``__ / __``end``__ / __``self-end``__:  los items se colocan al final del ``cross-axis``. De nuevo, la diferencia es sutil y consiste en respetar las reglas de ``flex-direction`` frente a las reglas del modo de escritura.
* __``center``__: los items están centrados en el ``cross-axis``.
* __``baseline``__: los items están alineados de tal forma que sus líneas de base se alinean.

Las palabras clave modificadoras ``safe`` e ``unsafe`` pueden utilizarse junto con el resto de estas palabras clave (aunque tenga en cuenta la compatibilidad con navegadores), y se ocupan de ayudarle a evitar alinear elementos de forma que el contenido se vuelva inaccesible.

### ``align-content``

![align-content](img/align-content.svg "align-content")

Alinea las líneas de un ``flex-container`` cuando hay espacio extra en el ``cross-axis``, de forma similar a como ``justify-content`` alinea elementos individuales en el ``main-axis``.

__NOTA__: Esta propiedad sólo tiene efecto en los contenedores flexibles multilínea, en los que ``flex-wrap`` tiene el valor ``wrap`` o ``wrap-reverse``. Un ``flex-container`` de una sola línea (es decir, donde ``flex-wrap`` está establecido en su valor por defecto, ``no-wrap``) no reflejará ``align-content``.

```css
.container {
    align-content: normal | flex-start | start | flex-end | end | center | space-between | space-around | space-evenly | stretch;
}
```

* __``normal``__ (default): los items se colocan en su posición por defecto como si no se hubiera establecido ningún valor.
* __``flex-start``__ / __``start``__: los items se colocan al principio del contenedor. El (más soportado) ``flex-start`` respeta el ``flex-direction``, mientras que ``start`` respeta la dirección del modo de escritura.
* __``flex-end``__ / __``end``__: los items se colocan hasta el final del contenedor. El (más soportado) ``flex-end`` respeta el ``flex-direction`` mientras que ``end`` honra la dirección del modo de escritura.
* __``center``__: los items son centrados en el contenedor.
* __``space-between``__: los items son distribuidos uniformemente; la primera línea está al principio del contenedor mientras que la última está al final.
* __``space-around``__: los items son distribuidos uniformemente con el mismo espacio alrededor de cada línea.
* __``space-evenly``__:  los items se distribuyen uniformemente con el mismo espacio a su alrededor.
* __``stretch``__: las líneas se estiran para ocupar el espacio restante.

Las palabras clave modificadoras ``safe`` e ``unsafe`` pueden utilizarse junto con el resto de estas palabras clave (aunque tenga en cuenta la compatibilidad con navegadores), y se ocupan de ayudarle a evitar alinear elementos de forma que el contenido se vuelva inaccesible.

### ``gap, row-gap, column-gap``

![gap, row-gap, column-gap](img/gap_row-gap_column-gap.svg "gap, row-gap, column-gap")

La propiedad ``gap`` controla explícitamente el espacio entre los ``flex-items``. Aplica ese espaciado sólo entre elementos no en los bordes exteriores.

```css
.container {
    display: flex;
    ...
    gap: 10px;
    gap: 10px 20px; /* row-gap | column gap */
    row-gap: 10px;
    column-gap: 20px;
}
```

El comportamiento podría ser pensado como un canal mínimo, ya que si el canal es más grande de alguna manera (debido a algo como ``justify-content: space-between;``) entonces la brecha sólo tendrá efecto si ese espacio acabara siendo más pequeño.

No es exclusivo para Flexbox, ``gap`` funciona también en Grid y layout multicolumna.

## Propiedades para los hijos

### ``order``

![order](img/order.svg "order")

Por defecto, los flex items se disponen en el orden de origen. Sin embargo, la propiedad ``order`` controla el orden en que aparecen en el flex container.

```css
.item {
    order: 5; /* default is 0 */
}
```

Los items con el mismo ``order`` vuelven al orden de origen.