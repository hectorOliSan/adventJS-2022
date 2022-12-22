# Reto #21: Creando la tabla de regalos

## Instrucciones :

Hay muchas cartas de niños pidiendo regalos y es muy difícil que podamos hacer inventario de todos ellos. Por eso, hemos decidido crear un programa que nos dibuje una tabla con los regalos que nos piden y sus cantidades.

Para ello nos dan un array de objetos con los nombres de los regalos y sus cantidades. Escribe una función que reciba este array y devuelva una cadena con la tabla dibujada.

```js
printTable([
  { name: 'Game', quantity: 2 },
  { name: 'Bike', quantity: 1 },
  { name: 'Book', quantity: 3 }
])
```

```
+++++++++++++++++++
| Gift | Quantity |
| ---- | -------- |
| Game | 2        |
| Bike | 1        |
| Book | 3        |
*******************
```

Otro ejemplo donde se puede ver que la tabla siempre usa sólo el espacio justo dependiendo de la longitud de los nombres de los regalos y de las cantidades.

```js
printTable([
  { name: 'PlayStation 5', quantity: 9234782374892 },
  { name: 'Book Learn Web Dev', quantity: 23531 }
])
```

```
++++++++++++++++++++++++++++++++++++++
| Gift               | Quantity      |
| ------------------ | ------------- |
| PlayStation 5      | 9234782374892 |
| Book Learn Web Dev | 23531         |
**************************************
```

Como ves, el tamaño de las celdas depende de la longitud de los nombres de los regalos y de las cantidades, aunque como mínimo tendrán que ser del espacio de los títulos `Gift` y `Quantity` respectivamente.

La tabla usa los símbolos: `+` para el borde superior, `*` para el borde inferior, `-` para las líneas horizontales y `|` para las líneas verticales.

Ten en cuenta:

- Usa sólo el espacio que necesitas para dibujar la tabla.

- Adapta la tabla a la longitud de los nombres de los regalos y de las cantidades o los títulos de las columnas.

- No hace falta que ordenes los resultados.

- La tabla no termina con salto de línea.

## **Solución :**

### 300 puntos

```js
function printTable(gifts) {
  gifts = [{name: 'Gift', quantity: 'Quantity'}, ...gifts];
  const sideALength = Math.max(...gifts.map(item => item.name.length));
  const sideBLength = Math.max(...gifts.map(item => `${item.quantity}`.length));
  const sectionsA = '-'.repeat(sideALength);
  const sectionsB = '-'.repeat(sideBLength);
  const totalLength = 7 + sideALength + sideBLength;
  gifts.splice(1,0,{name: sectionsA, quantity: sectionsB})

  const res = gifts.map((item) =>{
    const sideASubstract = sideALength - item.name.length;
    const sideASpaces = ' '.repeat(sideASubstract);
    const sideA = `| ${item.name}${sideASpaces} |`;

    const sideBSubstract = sideBLength - (`${item.quantity}`.length);
    const sideBSpaces = ' '.repeat(sideBSubstract);
    const sideB = ` ${item.quantity}${sideBSpaces} |`;

    return `${sideA}${sideB}\n`
  }).join('')

  const borderTop = '+'.repeat(totalLength);
  const borderBottom = '*'.repeat(totalLength);
  return `${borderTop}\n${res}${borderBottom}`
}
```
