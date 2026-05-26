# Proyecto final -  Tecnología de la programación
# Sistema de registro y evaluación de estudiantes

## Descripción del problema
Sistema donde se pueden registrar alumnos, con seis calificaciones cada uno, para luego poder promediar sus calificaciones y en base a ese promedio verificar si el estudiante esta aprobado o reprobado, mostrar a los alumnos con mejor y con peor promedio respectivamente y calcular el promedio general del grupo, asi como mostrar un reporte con el promedio grupal y el promedio de cada alumno.

Este sistema esta pensado para mejorar y agilizar los procesos de calificación de los estudiantes en instituciones académicas y esta diseñado para que pueda ser usado por los docentes y por la parte administrativa de dichas instituciones

## Pseudocódigo
```
INICIO

    // =====================================
    //         MÓDULO DE VALIDACIÓN
    // =====================================

    FUNCIÓN ValidarCalificación(calificación)
        SI
            calificación >= 0 Y calificación <= 10
            RETORNAR verdadero
        Sino
            RETORNAR falso
        FIN SI
    FIN FUNCIÓN

    FUNCIÓN ValidarNombreUnico(nombres, nombre)
        SI
            nombre NO ESTA EN nombres
            RETORNAR verdadero
        SINO
            RETORNAR falso
        FIN SI
    FIN FUNCIÓN

    // =====================================
    //         MÓDULO DE CÁLCULO
    // =====================================

    FUNCIÓN CalcularPromedo(calificaciones)
        Suma = 0
        PARA CADA calificación EN calificaciones HACER
            suma = suma + calificación
        FIN PARA
        RETORNAR suma/Cantidad(califiaciones)
    FIN FUNCIÓN

    FUNCIÓN DeterminarEstado(promedio)
        SI promedio >= 6
            RETORNAR "Aprobado"
        SINO
            RETORNAR "Reprobado"
        FIN SI
    FIN FUNCIÓN 

    FUNCIÓN EncontrarMejor(estudiantes)
        mejor = estudiantes[0]
        PARA CADA estudiante EN estudiantes HACER
            SI estudiante.promediio > mejor.promedio 
                mejor = estudiante
            FIN SI
        FIN PARA
        RETORNAR mejor
    FIN FUNCIÓN 

    FUNCIÓN EncontrarPeor(estudiantes)
        peor = estudiantes[0]
        PARA CADA estudiante EN estudiantes HACER
            SI estudiante.promedio < peor.promedio ENTONCES
                peor = estudiante
            FIN SI
        FIN PARA
        RETORNAR peor
    FIN FUNCIÓN 

    FUNCIÓN CalcularPromedioGrupal(estudiantes)
        suma = 0
        PARA CADA estudiante EN estudiantes HACER
            suma = estudiante.promedio
        FIN PARA
        RETORNAR suma/Cantidad(estudiantes)
    FIN FUNCIÓN

    // =====================================
    //         MÓDULO DE DATOS
    // =====================================

    FUNCIÓN CrearEstudiante(nombre, calificaciones, promedio, estado)
        estudiante.nombre = nombre
        estudiante.calificaciones = calificaciones
        estudiante.promedio = promedio
        estudiante.estado = estado

        RETORNAR estudiante
    FIN FUNCIÓN

    // =====================================
    //         MÓDULO DE DATOS
    // =====================================

    FUNCIÓN MostrarEstudiante(estudiante)
        MOSTRAR "Nombre: " + estudiante.nombre

        MOSTRAR "Calificaciones: " 
        PARA CADA calificación EN calificaciones HACER
            MOSTRAR calificación
        FIN PARA
    
        MOSTRAR "Promedio: " + estudiante.promedio
        MOSTRAR "Estado: " + estudiante.estado
    FIN FUNCIÓN 

    FUNCIÓN GenerarReporte(estudiantes)
        MOSTRAR "Reporte del grupo"
        PARA CADA estudiante EN estudiantes HACER
            MostrarEstudiante(estudiante)   
        FIN PARA

        mejor = EncontrarMejor(estudiantes)
        peor = EncontrarPeor(estudiantes)

        promedioGrupal = CalcularPromedioGrupal(estudiantes)

        MOSTRAR "Estadisticas: "
        MOSTRAR "Promedio del grupo: " + promedioGrupal
        MOSTRAR "Mejor promedio: " + mejor.nombre + "," + mejor.promedio
        MOSTRAR "Peor promedio: " + peor.nombre + "," + peor.promedio
    FIN FUNCIÓN

    // =====================================
    //         PROGRAMA PRINCIPAL
    // =====================================

    estudiantes = Lista vacía
    nombresRegistrados = Conjunto vacío
    continuar = "s"

    MIENTRAS continuar = "s" HACER
        MOSTRAR "REGISTRO DE ESTUDIANTE"
        nombre = ""

        REPETIR
            MOSTRAR "Ingrese el nombre del estudiante"
            LEER nombre
            SI NO ValidarNombreUnico(nombresRegistrados, nombre) ENTONCES
                ESCRIBIR "Error: Este nombre ya ha sido registrado"
            FIN SI
        HASTA QUE ValidarNombreUnico(nombresRegistrados, nombre)

        calificaciones = Lista vacia

        PARA i = 1 hasta 6 HACER
            REPETIR
                MOSTAR "Ingrese la calificación " + i + ": "
                LEER calificación

                SI NO ValidarCalificacion(calificación) ENTONCES
                    MOSTRAR "Error: Ingrese una calificación valida entre el 0 y 10"
                FIN SI
            HASTA QUE ValidarCalificaciones(calificación)
        
            AGREGAR calificación A calificaciones
        FIN PARA

        promedio = CalcularPromedio(calificaciones)
        estado = DeterminarEstado(promedio)

        estudiante = CrearEstudiante(nombre, calificaciones, promedio, estado)
        AGREGAR estudiante A estudiantes
        AGREGAR nombre A nombresRegistrados
        MOSTRAR "¿Desea agregar otro estudiante? (s/n)?
        LEER continuar 
    FIN MIENTRAS

    SI cantidad(estudiantes) > 0 ENTONCES
        GenerarReporte(estudiantes)
    SINO
        mostrar "No se han registrado estudiantes?
    FIN SI
FIN
```

## Diagramas de flujo
### MAIN
```mermaid
flowchart TD
A([INICIO]) --> B[estuiantes = Lista vacía]
B --> B1[nombresRegistrados = Conjunto vacío]
B1 --> B2[continuar = 's']
B2 --> C{¿continuar = 's'?}
C -->|Sí| D[Mostrar: 'REGRISTRO DE ESTUDIANTE']
D --> E[nombre = '']
E --> F[MOSTRAR: 'Ingrese el nombre del estudiante']
F --> G[/Leer nombre/]
G --> H{¿ValidarNombreUnico?}
H -->|no| I[MOSTRAR: 'Error: nombre ya registrado']
I --> F
H -->|Sí| J[calificaciones = lista vacia]
J --> K[I = 1]
K --> L{¿i <= 6?}
L --> |Sí| M[MOSTRAR: 'Ingrese calificación i']
M --> N[/Leer calificacion/]
N --> O{¿ValidarCalificación?}
O --> P[MOSTRAR: 'Error: calificación invalida']
P --> M
O --> |Sí| Q[AGREGAR calificación A calificaciones]
Q --> R[i = i + 1]
R --> L
L --> |No| S["promedio = CalcularPromedio(calificaciones)"]
S --> T["estado = DeterminarEstado(promedio)"]
T --> U["estudiante = CrearEstudiante(nombre, calificaciones, promedio, estado)"]
U --> V[AGREGAR estudiante A estudiantes]
V --> V1[AGREGAR nombre A nombresRegistrados]
V1 --> W["MOSTRAR: '¿Desea agregar otro estudiante?(s/n)"]
W --> X[/Leer continuar/]
X --> C 
C --> |No| Y{"¿Cantidad(estudiantes) > 0?"}
Y --> |Sí| Z["GenerarReporte(estudiantes)"]
Y --> |No| AA[MOSTARAR: 'No se han registrado estudiantes']
Z --> BB([FIN])
AA --> BB
```
---

### ValidarCalificación
```mermaid
flowchart TD
    A([INICIO]) --> B{"calificación >= 0 Y calificación <= 10?"}
    B -->|Sí| C[Retornar verdadero]
    B -->|No| D[Retornar falso]
    C --> E([FIN])
    D --> E
```
---

### ValidarNombreUnico
```mermaid
flowchart TD
    A([INICIO]) --> B{¿nombre NO ESTÁ EN nombres?}
    B --> |Sí| C[Retornar verdadero]
    B --> |No| D[Retornar falso]
    C --> E([FIN])
    D --> E
```
---

### CalcularPromedio
```mermaid
flowchart TD
    A([INICIO]) --> B[suma = 0]
    B --> C{¿Quedan calificaciones por iterar?}
    C --> |Sí| D[suma = suma + calificación]
    D --> C
    C --> |No| E["RETORNAR suma / Cantidad(calificaciones)"]
    E --> F([FIN]) 
```
---

### DeterminarEstado
```mermaid
flowchart TD
    A([INICIO]) --> B{¿promedio >= 6?}
    B --> |Sí| C[RETORNAR 'Aprobado']
    B --> |No| D[RETORNAR 'Reprobado']
    C --> E([FIN])
    D --> E
```
---

### EncontrarMejor
```mermaid
flowchart TD
    A([INICIO]) --> B["mejor = estudiantes[0]"]
    B --> C{¿Quedan estudiantes por iterar?}
    C --> |Sí| D{¿estudiante.promedio > mejor.promedio?}
    D --> |Sí| E[mejor = etudiante]
    D --> |No| C
    E --> C
    C --> |No| F[RETORNAR mejor]
    F --> G([FIN])
```
---

### EncontrarPeor
```mermaid
flowchart TD 
    A([INICIO]) --> B["peor = estudiantes[0]"]
    B --> C{¿Quedan estudiantes por iterar?}
    C --> |Sí| D{¿estudiante.promedio < peor.promedio?}
    D --> |Sí| E["peor = estudiante"]
    D --> |No| C
    E --> C
    C --> |NO| F[RETORNAR peor]
    F --> G([FIN])
```
---

### CalcularPromedioGrupal
```mermaid
flowchart TD
    A([INICIO]) --> B[suma = 0]
    B --> C{¿Quedan estudiantes por iterar?}
    C --> |Sí| D[suma = suma + estudiante.promedio]
    D --> C
    C --> |No| E["RETORNAR suma / Cantidad(estudiantes)"]
    E --> F([FIN])
```
---

### CrearEstudiante
```mermaid
flowchart TD
    A([INICIO]) --> B[estudiante.nombre = nombre]
    B --> C[estudiante.calificaciones = calificaciones]
    C --> D[estudiante.promedio = promedio]
    D --> E[estudiante.estado = estado]
    E --> F[RETORNAR estudiante]
    F --> G([FIN])
```
---

### MostrarEstudiante
```mermaid
flowchart TD
    A([INICIO]) --> B[MOSTRAR: estudiante.nombre]
    B --> C[MOSTRAR: 'Calificaciones: ']
    C --> D{¿Quedan calificaciones por iterar?}
    D --> |Sí| E["MOSTRAR: calificación"]
    E --> D
    D --> |No| F[MOSTRAR: estudiante.promedio]
    F --> G[MOSTRAR: estudiante.estado]
    G --> H([FIN])
```
---
### GenerarReporte
```mermaid
flowchart TD
    A([INICIO]) --> B[MOSTRAR: 'Reporte del grupo']
    B --> C{¿Quedan estudiantes por iterar?}
    C --> |Sí| D["MostrarEstudiante(estudiante)"]
    D --> C
    C --> |No| E["mejor = EncontrarMejor(estudiantes)"]
    E --> F["peor = EncontrarPeor(estudiantes)"]
    F --> G["promedioGrupal = CalcularPromedioGrupal(estudiantes)"]
    G --> H[MOSTRAR: 'Estadísticas: ']
    H --> I[MOSTRAR: 'Promedio del grupo: ' + promedioGrupal]
    I --> J[MOSTRAR: 'Mejor promedio: ' + mejor.nombre + ',' + mejor.promedio]
    J --> K[MOSTRAR: 'Peor promedio: ' + peor.nombre + ',' + peor.promedio]
    K --> L([FIN])
```