# 2do Parcial - Programación 1 | Mundial 2026

## Objetivo
Aplicar estructuras de control, arreglos unidimensionales y bidimensionales, funciones con y sin retorno, parámetros por valor y por referencia, y el algoritmo Bubble Sort para desarrollar una aplicación de consola en C#.

---

## Aclaración importante
- No es obligatorio completar el 100% del trabajo para aprobar.
- Se evaluará principalmente la comprensión del código y la defensa oral.
- Un desarrollo funcional parcial puede alcanzar la aprobación.

---



**Estructuras de datos sugeridas:**
- Arreglo de strings para nombres de selecciones
- Matriz 6x6 para goles
- Otros datos los calculan a través de funciones

---

## Manejo de datos - Precarga recomendada

**La persistencia de datos NO es parte de este trabajo.** Todos los datos se manejan en memoria durante la ejecución.

### Opción 1: Carga manual (tedioso pero válido)
El usuario ingresa todos los datos a través del menú. Para acelerar pruebas, pueden ingresar datos de ejemplo:

```
Argentina vs Brasil: 3 - 1
Brasil vs Uruguay: 2 - 2
Uruguay vs Argentina: 1 - 1
```

### Opción 2: Precarga de datos (RECOMENDADA)
Al iniciar, cargan datos de ejemplo directamente en el código. Ejemplo:

```csharp
// En Main, antes del menú:
string[] selecciones = { "Argentina", "Brasil", "Uruguay", 
                         "Paraguay", "Chile", "Colombia" };

int[,] goles = new int[6, 6];

// Precargando algunos partidos:
goles[0, 1] = 3; // Argentina vs Brasil: 3 goles
goles[1, 0] = 1; // Brasil vs Argentina: 1 gol

goles[1, 2] = 2; // Brasil vs Uruguay: 2 goles
goles[2, 1] = 2; // Uruguay vs Brasil: 2 goles

// ... etc
```

Esto permite **probar el programa inmediatamente** sin perder tiempo en entrada de datos.

---

## Parte 1: Gestión de selecciones

1. Desarrollar una función que permita cargar los nombres de 6 selecciones participantes en un arreglo.
   - Sugerencia: utilizar un arreglo de tipo string.
   - Validar que no se ingresen cadenas vacías.
   - **Ejemplo de entrada/salida:**
     ```
     Ingrese selección 1: Argentina
     Ingrese selección 2: Brasil
     ...
     ✓ 6 selecciones cargadas exitosamente
     ```

2. Desarrollar una función que muestre todas las selecciones cargadas.
   - **Ejemplo de salida:**
     ```
     === SELECCIONES CARGADAS ===
     0) Argentina
     1) Brasil
     2) Uruguay
     ...
     ```

3. Desarrollar una función que busque una selección por nombre y retorne su posición en el arreglo o -1 si no existe.
   - **Ejemplo de entrada/salida:**
     ```
     Buscar selección: Brasil
     ✓ Brasil encontrada en posición 1
     
     Buscar selección: Francia
     ✗ Selección no encontrada (retorna -1)
     ```

---

## Parte 2: Registro de partidos

Se trabajará con un arreglo bidimensional (matriz) de tamaño 6x6.

### Representación sugerida de los datos

Cada fila representa una selección como equipo local.
Cada columna representa una selección como equipo visitante.

**Ejemplo visual:**

```
                Col 0   Col 1   Col 2   Col 3   Col 4   Col 5
                (ARG)   (BRA)   (URU)   (PAR)   (CHI)   (COL)
Fila 0 (ARG)    X       3       1       0       2       1
Fila 1 (BRA)    1       X       2       2       1       3
Fila 2 (URU)    1       2       X       1       0       2
Fila 3 (PAR)    0       1       1       X       1       1
Fila 4 (CHI)    2       1       0       1       X       1
Fila 5 (COL)    1       3       2       1       1       X

- goles[0, 1] = 3 → Argentina (local) vs Brasil (visitante) = 3 goles
- goles[1, 0] = 1 → Brasil (local) vs Argentina (visitante) = 1 gol
- goles[i, i] = X → No se usa la diagonal (un equipo no juega contra sí mismo)
```

### Validaciones obligatorias para ingreso de partidos

4. Registrar los goles en una matriz bidimensional.

5. Desarrollar una función que permita ingresar el resultado de un partido solicitando:
   - selección local
   - selección visitante
   - goles de cada equipo

   **Validaciones:**
   - ✅ La selección local debe existir
   - ✅ La selección visitante debe existir
   - ✅ **Los goles NO pueden ser negativos** (valor >= 0)
   - ✅ No se puede jugar contra sí misma (índice_local ≠ índice_visitante)
   
   **Ejemplo de entrada/salida:**
   ```
   === INGRESAR RESULTADO DE PARTIDO ===
   Equipo local (0-5): 0
   Equipo visitante (0-5): 1
   Goles del equipo local: 3
   Goles del equipo visitante: 1
   ✓ Partido registrado: Argentina 3 - 1 Brasil
   
   --- Intentos fallidos ---
   Equipo local (0-5): 0
   Equipo visitante (0-5): 0
   ✗ Error: un equipo no puede jugar contra sí mismo
   
   Goles del equipo local: -2
   ✗ Error: los goles no pueden ser negativos
   ```

6. Validar:
   - que la selección local y visitante existan
   - que no se pueda jugar contra sí misma
   - que los goles sean valores no negativos

---

## Parte 3: Estadísticas básicas

7. Desarrollar una función que calcule los goles a favor de una selección.
   - **Lógica:** Sumar todos los goles que anotó esa selección (fila de la matriz)
   - **Ejemplo:** Argentina goles a favor = goles[0,1] + goles[0,2] + ... + goles[0,5]

8. Desarrollar una función que calcule los goles en contra de una selección.
   - **Lógica:** Sumar todos los goles que recibió esa selección (columna de la matriz)
   - **Ejemplo:** Argentina goles en contra = goles[1,0] + goles[2,0] + ... + goles[5,0]

9. Desarrollar una función que determine:
   - cantidad de partidos ganados
   - empatados
   - perdidos
   - **Lógica:** Comparar goles[i,j] vs goles[j,i] para cada posición

10. Desarrollar una función que calcule los puntos obtenidos por una selección.
    - Victoria: 3 puntos
    - Empate: 1 punto
    - Derrota: 0 puntos
    - **Ejemplo:** Argentina: 3 victorias = 9 pts, 1 empate = 1 pt, 1 derrota = 0 pts → **Total: 10 puntos**

---

## Parte 4: Tabla de posiciones

11. Desarrollar una función que genere los datos necesarios para la tabla de posiciones.
    - Crear un arreglo o estructura con: nombre, puntos, goles a favor, goles en contra, diferencia, partidos ganados, etc.

12. Ordenar la tabla utilizando el algoritmo Bubble Sort.

### Criterio de ordenamiento (importante)

Comparar en el siguiente orden:

1. Mayor cantidad de puntos
2. Mayor diferencia de gol (goles a favor - goles en contra)
3. Mayor cantidad de goles a favor

El ordenamiento debe ser descendente (mejor rendimiento primero).

**Pseudocódigo sugerido:**
```
for i = 0 to longitud-2
    for j = 0 to longitud-2-i
        if (tabla[j].puntos < tabla[j+1].puntos) 
           OR (tabla[j].puntos == tabla[j+1].puntos AND tabla[j].diferencia < tabla[j+1].diferencia)
           OR (tabla[j].puntos == tabla[j+1].puntos AND tabla[j].diferencia == tabla[j+1].diferencia 
               AND tabla[j].golesFavor < tabla[j+1].golesFavor)
            intercambiar(tabla[j], tabla[j+1])
```

13. Mostrar la tabla ordenada de forma clara.
    - **Ejemplo de salida:**
    ```
    === TABLA DE POSICIONES ===
    Pos | Equipo    | PJ | G | E | P | GF | GC | DG | Pts
    ----|-----------|----|----|---|----|----|----
     1. | Argentina |  5 | 3 | 1 | 1 | 10 |  5 | +5 | 10
     2. | Brasil    |  5 | 3 | 0 | 2 |  9 |  7 | +2 |  9
     3. | Uruguay   |  5 | 2 | 1 | 2 |  7 |  8 | -1 |  7
     4. | Paraguay  |  5 | 1 | 2 | 2 |  5 |  8 | -3 |  5
     5. | Chile     |  5 | 1 | 1 | 3 |  5 |  9 | -4 |  4
     6. | Colombia  |  5 | 0 | 1 | 4 |  4 | 10 | -6 |  1
    ```

14. Mostrar la selección con mayor cantidad de puntos.
15. Mostrar la selección con mayor cantidad de goles convertidos.
16. Mostrar la selección con menor cantidad de goles recibidos.

---

## Parte 5: Menú principal

17. Implementar un menú utilizando switch que permita acceder a todas las funcionalidades.

18. El menú deberá repetirse hasta que el usuario seleccione la opción salir.

**Estructura sugerida:**
```
===== MUNDIAL 2026 =====
1. Cargar selecciones
2. Mostrar selecciones
3. Buscar selección
4. Ingresar resultado de partido
5. Ver estadísticas de una selección
6. Mostrar tabla de posiciones
7. Estadísticas del torneo
8. Salir

Ingrese opción: _
```

---

# Parte 6: Consigna específica por grupo

Además de completar todas las consignas anteriores, cada grupo deberá implementar la funcionalidad asignada mediante sorteo.

##  Ejercicio 1
Desarrollar una función que muestre el ranking de selecciones ordenado por cantidad de goles convertidos utilizando el algoritmo Bubble Sort.

##  Ejercicio 2
Desarrollar una función que muestre el ranking de selecciones ordenado por cantidad de goles recibidos utilizando el algoritmo Bubble Sort.

##  Ejercicio 3
Desarrollar una función que muestre el ranking de selecciones ordenado por cantidad de victorias utilizando el algoritmo Bubble Sort.

##  Ejercicio 4
Desarrollar una función que muestre el ranking de selecciones ordenado por cantidad de empates utilizando el algoritmo Bubble Sort.

##  Ejercicio 5
Desarrollar una función que muestre el historial completo de partidos disputados por una selección ingresada por el usuario, indicando rival y resultado de cada encuentro.

##  Ejercicio 6
Desarrollar una función que determine y muestre el partido con mayor cantidad total de goles convertidos.

##  Ejercicio 7
Desarrollar una función que determine y muestre el partido con menor cantidad total de goles convertidos.

##  Ejercicio 8
Desarrollar una función que muestre todas las selecciones invictas del torneo (sin derrotas), indicando además la cantidad de victorias y empates obtenidos.

##  Ejercicio 9
Desarrollar una función que muestre todas las selecciones que no obtuvieron ninguna victoria, indicando además la cantidad de empates y derrotas obtenidos.

##  Ejercicio 10
Desarrollar una función que calcule y muestre el promedio de goles convertidos por cada selección.

##  Ejercicio 11
Desarrollar una función que determine y muestre la selección que participó en el partido con mayor diferencia de gol, indicando el resultado correspondiente.

##  Ejercicio 12
Desarrollar una función que determine y muestre la selección que sufrió la mayor goleada del torneo, indicando rival y resultado.

##  Ejercicio 13
Desarrollar una función que muestre la cantidad total de partidos que finalizaron en:

- Victoria local.
- Victoria visitante.
- Empate.

##  Ejercicio 14
Desarrollar una función que determine y muestre la selección con mayor cantidad de empates obtenidos durante el torneo.


---

## Requisitos técnicos obligatorios

- Uso de estructuras de control: if, switch
- Uso de ciclos: for, while o do while
- Uso de arreglos unidimensionales
- Uso de arreglos bidimensionales (matrices)
- Uso de funciones con y sin retorno
- Uso de parámetros por valor y por referencia
- Uso del algoritmo Bubble Sort
- Aplicación de consola en C#

---

## Recomendaciones de trabajo

- 1- Cargar selecciones y validar. Luego, ingreso de partidos con validaciones.
- 2- Funciones de estadísticas básicas. Generación de tabla de posiciones.
- 3- Implementar Bubble Sort. Menú interactivo. Consigna específica del grupo.
- Dividir el problema en funciones pequeñas y testear cada una antes de continuar.
- Validar entradas del usuario en todo momento.
- Usar nombres claros para variables y funciones.

---

## Evaluación

Se evaluará:

- **Funcionamiento del programa** — ¿Las funciones hacen lo que se pide?
- **Uso correcto de funciones** — ¿Hay parámetros y retornos apropiados?
- **Uso de estructuras vistas en clase** — ¿Utilizan todos los conceptos obligatorios?
- **Claridad del código** — ¿El código es legible y bien comentado?
- **Defensa oral individual** — Cada integrante debe poder explicar su parte del código.

---

## Notas finales

- **Sin persistencia:** Los datos se pierden al cerrar el programa. Use precarga de datos durante desarrollo.
- **Validación es clave:** Verifiquen goles no negativos, selecciones válidas, y que no haya auto-enfrentamientos.
- **Bubble Sort:** Practiquen primero con arreglos 1D antes de aplicar a la tabla.
- **Consulten al docente:** Si algo no queda claro, pregunten durante las clases.

¡Éxito en el trabajo práctico!
