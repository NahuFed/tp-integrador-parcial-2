# 2do Parcial - Programación 1 | Mundial 2026 

## Objetivo
Aplicar estructuras de control, arreglos unidimensionales y bidimensionales, funciones con y sin retorno, parámetros por valor y por referencia, generación de números aleatorios y el algoritmo Bubble Sort para desarrollar una aplicación de consola en C#.

---

## Aclaración importante
- No es obligatorio completar el 100% del trabajo para aprobar.
- Se evaluará principalmente la comprensión del código y la defensa oral.
- Un desarrollo funcional parcial puede alcanzar la aprobación.

---

## Configuración general

La cantidad de selecciones participantes deberá ser configurable mediante una variable o constante.

Ejemplo:

```csharp
const int N = 8;
```

Todos los arreglos, matrices y ciclos deberán utilizar dicha variable evitando valores literales en el código.

---

## Estructuras de datos sugeridas

- Arreglo de strings para nombres de selecciones.
- Matriz NxN para goles.
- Otros datos calculados mediante funciones.

---

## Manejo de datos - Precarga recomendada

La persistencia de datos NO es parte de este trabajo.

### Precarga recomendada

```csharp
string[] selecciones =
{
    "Argentina",
    "Jordania",
    "Argelia",
    "Austria"
};

int[,] goles = new int[N, N];
```

---

## Generación automática de resultados

Los estudiantes deberán aplicar la clase Random para generar resultados de prueba.

Ejemplo:

```csharp
Random rnd = new Random();
goles[i,j] = rnd.Next(0,6);
```

Se puede agregar una opción de menú para generar automáticamente un torneo completo y facilitar las pruebas.

---

## Parte 1: Gestión de selecciones

1. Desarrollar una función que permita cargar los nombres de N selecciones participantes en un arreglo.
   - Sugerencia: utilizar un arreglo de tipo string.
   - Validar que no se ingresen cadenas vacías.
   - **Ejemplo de entrada/salida:**
     ```
     Ingrese selección 1: Argentina
     Ingrese selección 2: Jordania
     ...
     ✓ 32 selecciones cargadas exitosamente
     ```

2. Desarrollar una función que muestre todas las selecciones cargadas.
   - **Ejemplo de salida:**
     ```
     === SELECCIONES CARGADAS ===
     0) Argentina
     1) Jordania
     2) Argelia
     3) Austria     
     ```

3. Desarrollar una función que busque una selección por nombre y retorne su posición en el arreglo o -1 si no existe.
   - **Ejemplo de entrada/salida:**
     ```
     Buscar selección: Jordania
     ✓ Jordania encontrada en posición 1
     
     Buscar selección: Chile
     ✗ Selección no encontrada (retorna -1)
     ```

---
---

# Parte 2: Registro de partidos

## Representación de los datos

Se trabajará con una única matriz cuadrada NxN.

Se jugará a un solo partido neutral (no existen local ni visitante).

Cada posición:

```text
goles[i,j]
```

representa la cantidad de goles convertidos por la selección i frente a la selección j.

El resultado completo entre dos selecciones se obtiene utilizando ambas posiciones:

```text
goles[i,j]
goles[j,i]
```

Ejemplo:

```text
goles[Argentina,Brasil] = 3
goles[Brasil,Argentina] = 1
```

Representa:

```text
Argentina 3 - 1 Brasil
```

La diagonal principal no se utiliza porque una selección no juega contra sí misma.


### Fixture

La matriz representa un torneo todos contra todos.

Ejemplo:

```                
        ARG     JOR     ALG     AUS    
 ARG    X       3       4       2       
 JOR    1       X       2       2       
 ALG    1       2       X       1       
 AUS    0       1       1       X       

- goles[0, 1] = 3 → Argentina vs Jordania = 3 goles
- goles[1, 0] = 1 → Jordania vs Argentina = 1 gol
- goles[i, i] = X → No se usa la diagonal (un equipo no juega contra sí mismo)
```
Cada enfrentamiento queda representado por dos posiciones simétricas.

---

4. Registrar los goles en una matriz bidimensional.

5. Desarrollar una función que permita ingresar el resultado de un partido solicitando:
   - selección 1
   - selección 2
   - goles de cada selección

6. Validar correctamente todos los datos ingresados.
**Validaciones:**
   - ✅ La selección local debe existir
   - ✅ La selección visitante debe existir
   - ✅ **Los goles NO pueden ser negativos** (valor >= 0)
   - ✅ No se puede jugar contra sí misma (i ≠ j)
   
   **Ejemplo de entrada/salida:**
   ```
   === INGRESAR RESULTADO DE PARTIDO ===
   Equipo 1 (0-3): 0
   Equipo 2 (0-3): 1
   Goles del equipo 1: 3
   Goles del equipo 2: 1
   ✓ Partido registrado: Argentina 3 - 1 Jordania
   
   --- Intentos fallidos ---
   Equipo 1 (0-3): 0
   Equipo 2 (0-3): 0
   ✗ Error: un equipo no puede jugar contra sí mismo
   
   Goles del equipo local: -2
   ✗ Error: los goles no pueden ser negativos
   ```
---

# Parte 3: Estadísticas básicas

7. Desarrollar una función que calcule los goles a favor de una selección.
   - **Lógica:** Sumar todos los goles que anotó esa selección (fila de la matriz)
   - **Ejemplo:** Argentina goles a favor = goles[0,1] + goles[0,2] + ... + goles[0,N-1]
8. Desarrollar una función que calcule los goles en contra de una selección.
   - **Lógica:** Sumar todos los goles que recibió esa selección (columna de la matriz)
   - **Ejemplo:** Argentina goles en contra = goles[1,0] + goles[2,0] + ... + goles[N-1,0]
9. Desarrollar una función que determine para una seleccion en particular la cantidad de:
   - partidos ganados 
   - empatados
   - perdidos
   - **Lógica:** Comparar goles[i,j] vs goles[j,i] para cada posición
   Ejemplo para Argentina:
   - Ganados: 3
   - Empatados: 0
   - Perdidos: 0

10. Calcular puntos obtenidos.

- Victoria: 3 puntos.
- Empate: 1 punto.
- Derrota: 0 puntos.

---

# Parte 4: Tabla de posiciones

11. Desarrollar una función que genere los datos necesarios para la tabla de posiciones.
    - Crear un arreglo o estructura con: nombre, puntos, goles a favor, goles en contra, diferencia, partidos ganados, etc.

12. Ordenar la tabla utilizando Bubble Sort.

## Criterio de ordenamiento

Ordenar únicamente por:

1. Mayor cantidad de puntos.

Si dos selecciones poseen la misma cantidad de puntos podrán permanecer en cualquier orden relativo.

Ejemplo:

```csharp
if (tabla[j].Puntos < tabla[j + 1].Puntos)
{
    Intercambiar(...);
}
```

13. Mostrar la tabla ordenada.
    - **Ejemplo de salida:**
    ```
    === TABLA DE POSICIONES ===
    Pos | Equipo    | PJ | G | E | P | GF | GC | DG | Pts
    ----|-----------|----|---|---|---|----|----|----|----
     1. | Argentina |  3 | 3 | 0 | 0 | 9  | 2  | +7 | 9
     2. | Jordania  |  3 | 1 | 1 | 1 | 5  | 6  | -1 | 4
     3. | Argelia   |  3 | 0 | 2 | 1 | 4  | 7  | -3 | 2
     4. | Austria   |  3 | 0 | 1 | 2 | 2  | 5  | -3 | 1
    
    ```
14. Mostrar la selección con mayor cantidad de puntos.
15. Mostrar la selección con mayor cantidad de goles convertidos.
16. Mostrar la selección con menor cantidad de goles recibidos.

---

# Parte 5: Menú principal

Implementar un menú utilizando switch.

Ejemplo:

```text
===== MUNDIAL 2026 =====
1. Cargar selecciones
2. Mostrar selecciones
3. Buscar selección
4. Ingresar resultado de partido
5. Ver estadísticas de una selección
6. Mostrar tabla de posiciones
7. Generar torneo aleatorio
8. Estadísticas del torneo
9. (insertar texto para el ejercicio adicional)
10. Salir
```

El menú deberá repetirse hasta seleccionar la opción salir.

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
Desarrollar una función que determine y muestre la cantidad total de partidos que finalizaron en:

- Victoria de alguna selección.
- Empate.

##  Ejercicio 14
Desarrollar una función que determine y muestre la selección con mayor cantidad de empates obtenidos durante el torneo.

---

# Requisitos técnicos obligatorios

- Uso de if y switch.
- Uso de for, while o do while.
- Uso de arreglos unidimensionales.
- Uso de matrices bidimensionales.
- Uso de funciones con y sin retorno.
- Uso de parámetros por valor y referencia.
- Uso de Random.
- Uso de Bubble Sort.
- Aplicación de consola en C#.
- **En el caso de usar IA para la resolucion de los ejercicios, deberán documentar tanto los prompts como las salidas de los prompts que se hicieron, pueden adjuntar capturas de pantalla para esto.**
---

# Evaluación

- Funcionamiento del programa.
- Uso correcto de funciones.
- Uso de estructuras vistas en clase.
- Claridad del código.
- Defensa oral individual.

---

# Notas finales

- Sin persistencia de datos.
- Validar correctamente todos los ingresos.
- Utilizar Random para acelerar pruebas.
- La diagonal principal de la matriz debe permanecer anulada.
- Consultar al docente ante cualquier duda.

¡Éxito en el parcial!

# Link del repositorio del parcial:
[2do Parcial Programacion 1](https://github.com/NahuFed/tp-integrador-parcial-2)
