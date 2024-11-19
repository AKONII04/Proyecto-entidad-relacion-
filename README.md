# Proyecto-entidad-relacion-
# Diseño de la Base de Datos - Mundial League of Legends 2024
## Enunciado
El comité organizador del Mundial de League of Legends 2024 ha decidido informatizar la gestión del torneo con una base de datos que almacene toda la información relevante sobre el campeonato y sus participantes, con el objetivo de facilitar el análisis de datos y generar reportes históricos del evento.

En el Mundial de League of Legends de 2024, el equipo T1 se coronó campeón gracias a una combinación de talento individual y estrategia de equipo. Liderados por el legendario jugador Lee "Faker" Sang-hyeok como capitán y mid laner, el equipo también contaba con Zeus en el rol de top laner, Oner como jungler, Gumayusi como AD Carry y Keria como support. Bajo la dirección del entrenador principal, Tom, T1 logró superar a sus oponentes en el exigente formato suizo del torneo.

Se desea registrar los datos de los jugadores que participan en el torneo. De cada jugador se quiere almacenar su nombre completo, apodo, rol dentro del equipo (top laner, jungler, mid laner, AD Carry o support), nacionalidad, y fecha de nacimiento. Además, se debe incluir información sobre su rendimiento individual, como número de asesinatos, asistencias y muertes acumulados durante el torneo, junto con el número de partidas jugadas. Cada jugador tendrá un código único que lo identifique en la base de datos. Cabe destacar que un jugador solo puede pertenecer a un único equipo durante todo el torneo.

De cada equipo participante se debe registrar su nombre, la región a la que representan (por ejemplo, Corea, China, Europa, Norteamérica), el nombre del entrenador principal, la cantidad de títulos internacionales previos ganados y la alineación de jugadores que forman parte del equipo. Cada equipo tendrá un identificador único y solo podrá tener un entrenador principal asignado. También se desea registrar al capitán del equipo, que será uno de los jugadores en la alineación.

En cuanto a los partidos jugados durante el torneo, se debe guardar información detallada como la fecha y hora del partido, los equipos enfrentados, el formato de la serie (por ejemplo, mejor de 1 o mejor de 5), el número de victorias obtenidas por cada equipo en la serie y el resultado final del enfrentamiento. También se debe registrar estadísticas específicas como la duración de cada partida, el número de asesinatos totales por equipo y los objetivos logrados (dragones, heraldos, barones Nashor). Cada partido será identificado de manera única.

Es necesario gestionar información sobre el torneo en sí, como su nombre, el año en que se lleva a cabo, la sede principal (ciudad o país), el formato competitivo utilizado (como fase de grupos, formato suizo o eliminatoria directa), y el premio total en dólares repartido entre los equipos. Además, se debe almacenar información sobre el equipo campeón del torneo y las estadísticas finales de sus jugadores.

Por otro lado, se desea registrar los logros individuales de los jugadores en cada partido, incluyendo distinciones como MVP (Jugador Más Valioso) del encuentro, la mayor cantidad de asesinatos en una partida o el mayor daño infligido. Estos logros estarán vinculados a jugadores específicos y a los partidos en los que los obtuvieron. Un jugador puede recibir múltiples reconocimientos a lo largo del torneo.

Finalmente, se quiere incluir información sobre los organizadores y patrocinadores del evento. De cada organizador se desea guardar su nombre, cargo, y entidad a la que pertenece. De los patrocinadores se debe registrar su nombre, el monto de su aportación económica y el tipo de patrocinio (tecnología, transporte, etc.). Esto permitirá tener un registro completo de todos los actores involucrados en el Mundial de League of Legends 2024.

## Entidades y sus Atributos

### 1. **Jugador**

| Atributo              | Descripción                                    |
|-----------------------|------------------------------------------------|
| `ID_jugador`          | Identificador único del jugador (PK)           |
| `Nombre`              | Nombre completo del jugador                    |
| `Apodo`               | Apodo o nombre de invocador del jugador        |
| `Rol`                 | Rol del jugador (top laner, jungler, mid laner, AD Carry, support) |
| `Nacionalidad`        | Nacionalidad del jugador                       |
| `Fecha_de_nacimiento` | Fecha de nacimiento del jugador                |
| `ID_equipo`           | ID del equipo al que pertenece (FK hacia Equipo) |

### 2. **Equipo**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_equipo`           | Identificador único del equipo (PK)              |
| `Nombre`              | Nombre del equipo                                |
| `Región`              | Región representada por el equipo (Corea, China, etc.) |
| `Entrenador`          | Nombre del entrenador principal                  |
| `Capitán`             | ID del jugador que es el capitán del equipo (FK hacia Jugador) |
| `Títulos_previos`     | Cantidad de títulos internacionales previos    |

### 3. **Torneo**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_torneo`           | Identificador único del torneo (PK)              |
| `Nombre`              | Nombre del torneo (por ejemplo, "Mundial 2024")   |
| `Año`                 | Año del torneo                                  |
| `Sede`                | Ciudad o país donde se lleva a cabo el torneo   |
| `Formato`             | Formato competitivo del torneo (fase de grupos, formato suizo, etc.) |
| `Premio_total`        | Monto total en dólares del premio               |

### 4. **Partido**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_partido`          | Identificador único del partido (PK)             |
| `Fecha`               | Fecha y hora en que se jugó el partido           |
| `ID_torneo`           | ID del torneo al que pertenece este partido (FK hacia Torneo) |
| `Equipo_ganador`      | ID del equipo ganador (FK hacia Equipo)          |
| `Equipo_perdedor`     | ID del equipo perdedor (FK hacia Equipo)         |
| `Formato_de_serie`    | Formato de la serie (mejor de 1, mejor de 5, etc.) |

### 5. **EstadísticasPartido**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_estadistica`      | Identificador único de la estadística (PK)       |
| `ID_partido`          | ID del partido (FK hacia Partido)                |
| `ID_jugador`          | ID del jugador (FK hacia Jugador)                |
| `Asesinatos`          | Número de asesinatos del jugador en ese partido  |
| `Asistencias`         | Número de asistencias del jugador en ese partido |
| `Muertes`             | Número de muertes del jugador en ese partido     |
| `Daño_total`          | Daño total infligido por el jugador              |
| `MVP`                 | Si fue MVP del partido (booleano)                |

### 6. **LogroIndividual**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_logro`            | Identificador único del logro (PK)               |
| `ID_jugador`          | ID del jugador (FK hacia Jugador)                |
| `ID_partido`          | ID del partido (FK hacia Partido)                |
| `Descripción`         | Descripción del logro (por ejemplo, "Mayor cantidad de asesinatos") |

### 7. **Patrocinador**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_patrocinador`     | Identificador único del patrocinador (PK)        |
| `Nombre`              | Nombre del patrocinador                          |
| `Tipo_de_patrocinio`  | Tipo de patrocinio (tecnología, transporte, etc.) |
| `Monto_aportado`      | Monto de la aportación económica                 |

### 8. **TorneoPatrocinador**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_torneo`           | ID del torneo (FK hacia Torneo)                  |
| `ID_patrocinador`     | ID del patrocinador (FK hacia Patrocinador)      |

### 9. **Organizador**

| Atributo              | Descripción                                      |
|-----------------------|--------------------------------------------------|
| `ID_organizador`      | Identificador único del organizador (PK)         |
| `Nombre`              | Nombre del organizador                           |
| `Cargo`               | Cargo que ocupa dentro del evento                |
| `Entidad`             | Entidad o empresa a la que pertenece             |
| `ID_torneo`           | ID del torneo gestionado por el organizador (FK hacia Torneo) |

---

## Relaciones y Consideraciones

1. **Relación Jugador - Equipo (N:1)**: Un jugador pertenece a un solo equipo, pero un equipo puede tener múltiples jugadores. Esta relación se maneja mediante el atributo `ID_equipo` en la tabla **Jugador**.

2. **Relación Capitán - Jugador (1:1 reflexiva)**: El capitán de un equipo es un jugador de ese equipo. En la tabla **Equipo**, el campo `Capitán` es una clave foránea hacia la tabla **Jugador**, lo que asegura que el capitán sea un jugador válido.

3. **Relación Partido - Torneo (N:1)**: Un partido pertenece a un solo torneo, pero un torneo puede tener múltiples partidos. Esta relación se maneja mediante el atributo `ID_torneo` en la tabla **Partido**.

4. **Relación Jugador - Partido - Estadísticas (N:1)**: Un jugador puede participar en múltiples partidos y un partido tiene estadísticas para múltiples jugadores. Esta relación se maneja a través de la tabla **EstadísticasPartido**.

5. **Relación Torneo - Patrocinador (N:1)**: Un torneo puede tener múltiples patrocinadores, y un patrocinador puede estar asociado a múltiples torneos. Esta relación se gestiona con la tabla **TorneoPatrocinador**.

6. **Relación Torneo - Organizador (1:1)**: Un torneo es gestionado por un único organizador. Esta relación se maneja con el campo `ID_torneo` en la tabla **Organizador**.

7. **Relación LogroIndividual - Jugador - Partido (N:1)**: Un jugador puede obtener múltiples logros en distintos partidos. Esta relación se gestiona mediante la tabla **LogroIndividual**.

---

Este diseño proporciona una estructura sólida para almacenar y gestionar toda la información relevante para el Mundial de League of Legends 2024, permitiendo un fácil acceso y análisis de datos para generar reportes históricos, estadísticas y más.
