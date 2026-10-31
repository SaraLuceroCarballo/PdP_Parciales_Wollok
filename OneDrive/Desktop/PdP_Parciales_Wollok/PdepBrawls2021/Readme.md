# Pdep Brawls
 
Parcial de Objetos - Paradigmas de Programación (Jueves Mañana) - 11/11/2021
Lenguaje: Wollok
 
## Contexto
 
La empresa Superchet nos contrató para desarrollar la lógica de su nuevo juego **Pdep Brawls** en Wollok. Cualquier coincidencia con juegos existentes es mera casualidad: ¡el juego es completamente diferente!
 
En el juego se pueden tener varios **personajes** con los cuales participar de distintas **misiones**. Cada personaje tiene una cierta cantidad de copas ganadas, y al realizar una misión puede pasar que ganen o pierdan copas.
 
## Dominio
 
### Personajes
 
Existen estos personajes, pero puede haber más a futuro.
 
| Personaje | Destreza | Estrategia |
|---|---|---|
| **Arquero** | agilidad * rango | cuando su rango supera los 100 metros |
| **Guerrera** | fuerza + 50% (1,5 * fuerza) | depende de cada guerrera (hay con y sin estrategia) |
| **Ballestero** | el doble de la de un arquero normal | como un arquero (es un arquero entrenado) |
 
### Misiones
 
En toda misión hay **copas en juego**. Se suman o se restan a los personajes que participan, según si la misión puede ser superada o no.
 
| Misión | Copas en juego | Puede ser superada cuando... |
|---|---|---|
| **Individual** | el doble de la dificultad de la misión | el personaje tiene estrategia, o su destreza supera la dificultad de la misión |
| **Por equipo** | 50 dividido la cantidad de personajes que participan | más de la mitad de los participantes tienen estrategia, o cada uno tiene una destreza mayor a 400 |
 
## Requerimientos
 
Se pide codificación y diagrama estático (de clases) completo, incluyendo los **puntos de entrada** de cada punto.
 
### 1. Saber si una misión puede ser superada
 
### 2. Realizar una misión
 
Repartir las copas (sumando o restando) según lo establecido.
 
**Restricciones:** no debe ser posible realizar:
 
- misiones individuales cuyo participante tenga menos de **10 copas**
- misiones por equipo con un total de copas entre los participantes menor a **60**
En ambos casos debe ocurrir el error **"Misión no puede comenzar"**.
 
**Ejemplo:** misión por equipo con 5 participantes.
 
- Si puede ser superada, cada uno recibe 10 copas.
- Si no puede ser superada, a cada uno se le restan 10 copas.
- Si la misión no puede realizarse, no ocurre ninguna de las dos cosas y salta el error "Misión no puede comenzar".
### 3. Misiones Boost y Bonus
 
Además de las misiones comunes, se agregan:
 
- **Boost:** cada una tiene un multiplicador que multiplica la cantidad de copas en juego.
- **Bonus:** otorgan 1 copa más por cada participante de la misión.
Puede haber misiones comunes, Boost y Bonus, **tanto por equipo como individuales**.
 
### 4. Tests
 
Escribir los tests necesarios para probar el código que verifica que una **misión individual fue superada**. Se espera un test bien nombrado por cada clase de equivalencia.
 
### 5. Polimorfismo
 
¿En qué lugar de la solución aparece el polimorfismo? Justificar marcando los objetos polimórficos y quién se aprovecha del polimorfismo.
 
### 6. Diagrama estático
 
Realizar el diagrama estático de toda la solución. No hace falta poner getters ni setters.
 
## Entregables
 
- [ ] Código Wollok (puntos 1 a 3)
- [ ] Punto de entrada indicado en cada punto
- [ ] Tests (punto 4)
- [ ] Justificación del polimorfismo (punto 5)
- [ ] Diagrama de clases completo (punto 6)
## Notas de diseño (para la resolución)
 
- Personajes y misiones son dos familias polimórficas: `destreza()` y `tieneEstrategia()` en los personajes; `puedeSerSuperada()` y `copasEnJuego()` en las misiones.
- Ballestero es un arquero: herencia con `super()`.
- Boost y Bonus se combinan con individual y por equipo, así que conviene composición (la misión delega en un modificador de copas) y no herencia.
- Validar antes de repartir copas, para no dejar estado a medias.
- Clases de equivalencia para la misión individual: con estrategia; sin estrategia y destreza mayor a la dificultad; sin estrategia y destreza igual (borde); sin estrategia y destreza menor.
 