# Pdepfoni — Parcial Objetos 2019
 
Paradigmas de Programación · Jueves Mañana · Parcial Objetos 2019 · Wollok
 
## Contexto
 
Una empresa de telefonía celular pide un sistema que maneje las **líneas** y **packs** de sus clientes.
 
- Una **línea** tiene un número de teléfono y puede tener **varios packs activos**.
- Los packs permiten que la línea realice **consumos**.
## Tipos de consumo
 
| Consumo | Se mide en |
|---|---|
| Internet | cantidad de MB |
| Llamadas | cantidad de segundos |
 
## Packs existentes
 
| Pack | Descripción |
|---|---|
| Crédito | Cierta cantidad de crédito disponible |
| MB libres | Cantidad de MB libres para navegar |
| Llamadas gratis | Llamadas sin costo |
| Internet ilimitado los findes | Ver uso de `Date` al final |
 
## Reglas generales
 
- Agregar packs a futuro debe ser **sencillo** (por ejemplo: Internet gratis los martes, segundos de llamada libres). No hace falta implementarlos ahora.
- Algunos packs tienen **vigencia** (fecha de vencimiento). Un pack de llamadas gratis o de 1000 MB que esté vencido **no puede utilizarse más**.
## Requerimientos
 
### 1. Costo de un consumo
 
La empresa dispone de precios por MB y por segundo de llamada. Siempre se cobra un **precio fijo por los primeros 30 segundos** de llamada, y luego se cobra por cada segundo pasado de los 30.
 
Ejemplo con precio por segundo `$0.05`, precio fijo `$1` y precio por MB `$0.10`:
 
- Llamada de 40 segundos: `$1 + 10 * $0.05 = $1.50`
- Consumo de internet de 5 MB: `5 * $0.10 = $0.50`
> Recomendación: leer el punto 2 para ayudarse con el modelado.
 
### 2. Información de los consumos de una línea
 
- **a.** Costo **promedio** de todos los consumos realizados dentro de un rango de fechas (inicial y final).
- **b.** Costo **total** gastado por la línea en los consumos de los **últimos 30 días**.
### 3. Un pack puede satisfacer un consumo
 
Ejemplos (con los precios del punto 1):
 
- Un pack de 100 MB libres satisface un consumo de internet de 5 MB.
- Ese mismo pack **no** satisface una llamada de 60 segundos.
- Un pack de $100 de crédito satisface ambos consumos.
### 4. Agregar un pack a una línea
 
Poder agregar cualquiera de los packs mencionados a una línea.
 
### 5. Una línea puede hacer cierto consumo
 
Ejemplo: la línea `1566666666` tiene estos packs:
 
- 10 MB libres
- $50 de crédito
- 200 MB libres, vencidos el 13/10/2019
- 5 MB libres
- 15 MB libres, vigentes hasta el 12/12/2019
Esta línea **no** puede hacer un consumo de internet de 20 MB, porque el consumo debe poder satisfacerse **completamente por un único pack**.
 
### 6. Realizar un consumo
 
Debe:
 
- **Registrar** el consumo en la línea (punto 2).
- **Gastar** el pack que lo satisface. Por ahora, los packs de MB libres y crédito se van gastando; el resto no.
- Consumir el **último pack agregado** que pueda satisfacerlo. Ejemplo: si primero se agregó un pack de llamadas gratis y después uno de crédito, primero se descuenta el crédito.
- Lanzar un **error** si no se puede realizar el consumo porque ningún pack alcanza.
### 7. Más sobre packs
 
- **a. Limpieza de packs:** eliminar los packs vencidos o completamente acabados.
- **b. Packs "MB libres++":** como los de MB libres, pero cuando se gastan los MB libres **siguen sirviendo** para consumos de **0.1 MB o menos**.
### 8. Tipos de línea
 
| Tipo | Comportamiento cuando ningún pack permite el consumo |
|---|---|
| Común | No se puede hacer el consumo |
| Black | Se realiza igual y se **suma el costo a un registro de deuda** |
| Platinum | Se realiza igual y **no suma ninguna deuda** |
 
Las líneas deben poder **cambiar entre común, black y platinum** sin perder el registro de packs ni las estadísticas de consumo.
 
### 9. Tests
 
En base a los ejemplos, hacer 3 tests:
 
- **a.** Uno que verifique que se haya producido **efecto** correctamente.
- **b.** Uno que verifique que **no se pueda hacer** algo.
- **c.** Uno que verifique que **se devuelva bien** algo.
### 10. Preguntas de diseño
 
Describir y **justificar** qué es lo mínimo necesario para agregar:
 
- **a.** Un nuevo pack (como los mencionados al principio).
- **b.** Un nuevo consumo (como la posibilidad de enviar SMS).
Debe usarse un **diagrama** que acompañe la explicación.
 
## Anexo: uso de la clase `Date`
 
```wollok
>>> var hoy = new Date()
>>> var diaIndependencia = new Date(day=9, month=7, year=1816)
>>> hoy > diaIndependencia
true
>>> hoy.dayOfWeek() == sunday
true
```
 
Las fechas también entienden mensajes para restar/sumar días y saber si están entre otras dos:
 
```wollok
>>> var ayer = hoy.minusDays(1)
>>> var maniana = hoy.plusDays(1)
>>> hoy.between(ayer, maniana)
true
```
 

Claude terminó la respuesta
