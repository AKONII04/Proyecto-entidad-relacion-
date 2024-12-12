# Proyecto-entidad-relacion-
# Diseño de la Base de Datos - Mundial League of Legends 2024
## Enunciado
El comité organizador del Mundial de League of Legends 2024 ha decidido informatizar la gestión del torneo con una base de datos que almacene toda la información relevante sobre el campeonato y sus participantes, con el objetivo de facilitar el análisis de datos y generar reportes históricos del evento.

En el Mundial de League of Legends de 2024, el equipo T1 se coronó campeón gracias a una combinación de talento individual y estrategia de equipo. Liderados por el legendario jugador Lee "Faker" Sang-hyeok como capitán y mid laner, el equipo también contaba con Zeus en el rol de top laner, Oner como jungler, Gumayusi como AD Carry y Keria como support. Bajo la dirección del entrenador principal, Tom, T1 logró superar a sus oponentes en el exigente formato suizo del torneo.

Se desea registrar los datos de los jugadores que participan en el torneo. De cada jugador se quiere almacenar su nombre completo, apodo, rol dentro del equipo (top laner, jungler, mid laner, AD Carry o support), nacionalidad, y fecha de nacimiento. Además, se debe incluir información sobre su rendimiento individual, como número de asesinatos, asistencias y muertes acumulados durante el torneo, junto con el número de partidas jugadas. Cada jugador tendrá un código único que lo identifique en la base de datos. Cabe destacar que un jugador solo puede pertenecer a un único equipo durante todo el torneo.

De cada equipo participante se debe registrar su nombre, la región a la que representan (por ejemplo, Corea, China, Europa, Norteamérica), el nombre del entrenador principal, la cantidad de títulos internacionales previos ganados y la alineación de jugadores que forman parte del equipo. Cada equipo tendrá un identificador único y solo podrá tener un entrenador principal asignado. 

En cuanto a los partidos jugados durante el torneo, se debe guardar información detallada como la fecha y hora del partido, los equipos enfrentados, el formato de la serie (por ejemplo, mejor de 1 o mejor de 5), el número de victorias obtenidas por cada equipo en la serie y el resultado final del enfrentamiento. 

Es necesario gestionar información sobre el torneo en sí, como su nombre, el año en que se lleva a cabo, la sede principal (ciudad o país), el formato competitivo utilizado (como fase de grupos, formato suizo o eliminatoria directa), y el premio total en dólares repartido entre los equipos. Además, se debe almacenar información sobre el equipo campeón del torneo y las estadísticas finales de sus jugadores.

Por otro lado, se desea registrar los logros individuales de los jugadores en cada partido, incluyendo distinciones como MVP (Jugador Más Valioso) del encuentro, la mayor cantidad de asesinatos en una partida o el mayor daño infligido. Estos logros estarán vinculados a jugadores específicos y a los partidos en los que los obtuvieron. Un jugador puede recibir múltiples reconocimientos a lo largo del torneo.

Finalmente, se quiere incluir información sobre los organizadores y patrocinadores del evento. De cada organizador se desea guardar su nombre, cargo, y entidad a la que pertenece. De los patrocinadores se debe registrar su nombre, el monto de su aportación económica y el tipo de patrocinio (tecnología, transporte, etc.). 


![Descripción de la imagen](https://pbs.twimg.com/media/Fg1apC5UYAAnVks?format=jpg&name=small)

## Entidades y sus Atributos / Paso a tabla 
# Atributos por Tabla

## Jugador
- **ID_jugador (PK)**  
- Nombre  
- Apodo  
- Rol  
- Nacionalidad  
- Fecha de nacimiento  


## Equipo
- **ID_equipo (PK)**  
- Nombre  
- Región  
- Entrenador  
- Títulos previos  

## Torneo
- **ID_torneo (PK)**  
- Nombre  
- Año  
- Sede  
- Formato  
- Premio total  

## Partido
- **ID_partido (PK)**  
- Fecha  
- ID_torneo (FK hacia Torneo)  
- Formato de serie  

## Patrocinador
- **ID_patrocinador (PK)**  
- Nombre  
- Tipo de patrocinio  
- Monto aportado  

## Organizador
- **ID_organizador (PK)**  
- Nombre  
- Cargo  
- Entidad  

---------


## Paso a tabla 


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
| `Entrenador`          | Nombre del entrenador principal                  | |
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


# Normalización del Modelo de Base de Datos - Mundial de League of Legends 2024

## Primera Forma Normal (1NF)

### Requisitos
- Cada columna debe contener valores **atómicos** (sin listas ni conjuntos).
- Cada fila debe ser única (asegurado con claves primarias).
- No deben existir columnas repetitivas.

### Ejemplo de Aplicación
- En la tabla **Jugador**, cada jugador tiene una fila única identificada por `ID_jugador`. Sus atributos, como `Rol` o `Nacionalidad`, contienen valores atómicos (no listas de roles ni múltiples nacionalidades).

---

 ## Segunda Forma Normal (2NF)

### Requisitos
- Cumple con 1NF.
- Todos los atributos no clave dependen **totalmente** de la clave primaria.

### Ejemplo de Aplicación
- En **EstadísticasPartido**, los atributos como `Asesinatos` o `Asistencias` dependen completamente de la combinación de las claves `ID_partido` y `ID_jugador`, que forman la clave primaria en un modelo de tabla compuesta.

Si hubiera información como el nombre del jugador, que depende solo de `ID_jugador` y no de ambos atributos, se movería a la tabla **Jugador**.
---

## Tercera Forma Normal (3NF)

### Requisitos
- Cumple con 2NF.
- No existen dependencias transitivas entre atributos no clave.

### Ejemplo de Aplicación
- En **Equipo**, los atributos como `Nombre` o `Región` dependen solo de la clave primaria `ID_equipo`. Si existiera una relación como "La región determina el nombre del equipo", se dividiría en una nueva tabla (no necesaria aquí porque no hay dependencia transitiva).

  

---



# Relaciones entre Entidades - Mundial League of Legends 2024

## Relaciones Principales

### 1. **Relación Jugador - Equipo (1:N)**  
- **Descripción**:  
  Un jugador pertenece a un único equipo durante el torneo, pero un equipo puede tener varios jugadores en su alineación.  
- **Cardinalidad**:  
  - **1:N**: Un equipo puede tener muchos jugadores.  
  - **1:1**: Un jugador pertenece a un único equipo.  
- **Implementación**:  
  - En la tabla **Jugador**, el atributo `ID_equipo` actúa como una clave foránea hacia la tabla **Equipo**.  

---

### 2. **Relación Partido - Torneo (1:N)**  
- **Descripción**:  
  Un partido pertenece a un solo torneo, pero un torneo puede incluir múltiples partidos.  
- **Cardinalidad**:  
  - **1:N**: Un torneo puede tener varios partidos.  
  - **1:1**: Cada partido pertenece a un único torneo.  
- **Implementación**:  
  - En la tabla **Partido**, el atributo `ID_torneo` actúa como una clave foránea hacia la tabla **Torneo**.

---

### 3. **Relación Jugador - PartidoEstadísticas (N:M)**  
- **Descripción**:  
  Un jugador puede participar en varios partidos y, en cada partido, se registran estadísticas individuales.  
- **Cardinalidad**:  
  - **N:M**: Un jugador puede estar en múltiples partidos y un partido tiene estadísticas para varios jugadores.  
- **Implementación**:  
  - La tabla **EstadísticasPartido** actúa como una tabla intermedia entre **Jugador** y **Partido**, permitiendo registrar estadísticas detalladas para cada jugador en cada partido.

---

### 4. **Relación Torneo - Patrocinador (N:M)**  
- **Descripción**:  
  Un torneo puede tener múltiples patrocinadores, y un patrocinador puede estar asociado con múltiples torneos.  
- **Cardinalidad**:  
  - **N:M**: Un torneo puede tener varios patrocinadores, y un patrocinador puede apoyar múltiples torneos.  
- **Implementación**:  
  - La tabla **TorneoPatrocinador** actúa como una tabla intermedia que conecta a las tablas **Torneo** y **Patrocinador**.  

---

### 5. **Relación Torneo - Organizador (1:N)**  
- **Descripción**:  
  Un torneo puede tener varios organizadores involucrados en su gestión.  
- **Cardinalidad**:  
  - **1:N**: Un torneo puede estar gestionado por múltiples organizadores.  
  - **1:1**: Cada organizador está asignado a un único torneo.  
- **Implementación**:  
  - En la tabla **Organizador**, el atributo `ID_torneo` actúa como una clave foránea hacia la tabla **Torneo**.  

---

### 6. **Relación LogroIndividual - Jugador - Partido (N:M)**  
- **Descripción**:  
  Un jugador puede recibir múltiples logros en diferentes partidos del torneo.  
- **Cardinalidad**:  
  - **N:M**: Un jugador puede tener logros en varios partidos, y un partido puede incluir logros para varios jugadores.  
- **Implementación**:  
  - La tabla **LogroIndividual** relaciona **Jugador** y **Partido**, con un campo adicional para la descripción del logro.

---

### 7. **Relación Equipo - Partido (N:M)**  
- **Descripción**:  
  Cada partido tiene dos equipos enfrentándose, y un equipo puede participar en múltiples partidos.  
- **Cardinalidad**:  
  - **N:M**: Un equipo puede jugar varios partidos, y cada partido enfrenta a dos equipos.  
- **Implementación**:  
  - En la tabla **Partido**, los atributos `Equipo_ganador` y `Equipo_perdedor` son claves foráneas hacia la tabla **Equipo**.

---

### 8. **Relación Torneo - Equipo (1:N)**  
- **Descripción**:  
  Un torneo puede tener múltiples equipos compitiendo, pero un equipo pertenece a un único torneo.  
- **Cardinalidad**:  
  - **1:N**: Un torneo incluye varios equipos.  
  - **1:1**: Cada equipo compite en un único torneo.  
- **Implementación**:  
  - En la tabla **Equipo**, el atributo `ID_torneo` podría añadirse (si es necesario) como una clave foránea hacia **Torneo** para conectar los equipos con el torneo correspondiente.

---
![EntidadRelacionLOL2024 drawio](https://github.com/user-attachments/assets/1d45d5ef-2802-4ae2-a80e-628f8797f3c5)










