# Catar 2022
 
Parcial de Objetos - Paradigmas de Programación (Jueves Mañana) - UTN FRBA - 2022
Lenguaje: Wollok
 
## Contexto
 
> **Catar** (1. tr. Probar, gustar algo para examinar su sabor o sazón. 2. sp. Lugar donde se juega la copa del mundo. 3. pdep. Parcial de objetos.)
 
Queremos modelar un sistema en el que los **cocineros** se ocupan de preparar y catar **platos**.
 
## Dominio
 
### Platos
 
| Plato | Azúcar | ¿Es bonito? |
|---|---|---|
| **Entrada** | nunca tiene | siempre |
| **Principal** | puede tener una cantidad de azúcar o nada | puede serlo o no |
| **Postre** | siempre 120 g | cuando tiene más de 3 colores |
 
**Calorías de cualquier plato:** 3 * cantidad de azúcar + 100 de base.
 
### Cocineros
 
Por ahora son **pasteleros** o **chefs**. Todo cocinero, además de cocinar, sabe **catar** un plato (calificarlo).
 
| Cocinero | Atributo propio | Calificación al catar |
|---|---|---|
| **Pastelero** | nivel deseado de dulzor | 5 * azúcar del plato / dulzor deseado (máximo 10) |
| **Chef** | cantidad máxima de calorías (definida por cada chef) | 10 si el plato es bonito y tiene hasta esa cantidad de calorías; 0 en caso contrario |
 
## Requerimientos
 
Se pide la codificación completa en Wollok de los siguientes puntos, utilizando las herramientas del paradigma de objetos.
 
### 1. Calorías de un plato
 
Conocer las calorías de un plato (3 * azúcar + 100).
 
### 2. Catar un plato
 
Cuando un plato es catado, se obtiene la calificación que le da el catador.
 
### 3. Cambiar de especialidad
 
Que un cocinero pueda cambiar de especialidad (por ejemplo, pasar de ser chef a ser pastelero).
 
### 4. Souschef
 
Agregar la especialidad **souschef**. Es como el chef, pero cuando no se cumplen las expectativas la calificación que pone es la cantidad de calorías del plato / 100 (máximo 6).
 
### 5. Cocinar
 
Hacer que un cocinero cocine, lo cual crea un plato y lo retorna:
 
| Especialidad | Plato que crea |
|---|---|
| **Pastelero** | postre con tantos colores como su nivel de dulzor deseado dividido 50 |
| **Chef** | plato principal bonito, con una cantidad de azúcar igual a la cantidad de calorías preferida del cocinero |
| **Souschef** | entrada |
 
### 6. Torneos
 
Existen torneos, que tienen catadores.
 
- **a.** Hacer que un cocinero participe en un torneo: al participar cocina y presenta su plato al torneo.
- **b.** Encontrar el cocinero ganador del torneo: es aquel que haya presentado el plato que obtiene la mayor puntuación del torneo (la suma de las calificaciones individuales de cada catador).
  - **Cuidado:** si no se presenta ningún cocinero al torneo, no se puede establecer al ganador.
### 7. Tests
 
Escribir los tests necesarios para probar la calificación otorgada por un **pastelero**. Se esperan tantos tests como clases de equivalencia, bien nombrados.
 
## Entregables
 
- [ ] Código Wollok (puntos 1 a 6)
- [ ] Tests de la calificación del pastelero (punto 7)
## Notas de diseño (para la resolución)
 
- Platos: familia polimórfica con `azucar()` y `esBonito()`. Las calorías se calculan igual para todos, así que van en la superclase.
- Como un cocinero puede cambiar de especialidad, conviene composición: el cocinero tiene un atributo `var especialidad` y le delega `catar(plato)` y `cocinar()`.
- Souschef es como el chef: hereda del chef y redefine solo la calificación cuando no se cumplen las expectativas.
- Torneo: la puntuación de un plato es la suma de lo que le da cada catador (`sum`). Para el ganador, `max` sobre los participantes, validando antes el caso sin participantes.
- Clases de equivalencia para el pastelero: azúcar baja (calificación menor a 10), azúcar justo en el límite (10), azúcar que excede el límite (se corta en 10) y plato sin azúcar (0).
 