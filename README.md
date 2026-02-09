

Generador de Polígonos 2D para Blender

Este script automatiza la creación de geometrías poligonales regulares dentro de Blender utilizando la API `bpy` y cálculos trigonométricos.

1. Lógica Matemática
El script utiliza el concepto de **Círculo Unitario** para determinar la posición de los vértices. Dado un número de lados $n$, el ángulo entre cada vértice se define como:

$$\theta = \frac{2\pi}{n}$$

Para cada iteración $i$, las coordenadas se calculan como:
* $x = radio \cdot \cos(i \cdot \theta)$
* $y = radio \cdot \sin(i \cdot \theta)$



2. Estructura de Datos de Geometría
El script emplea el método `from_pydata`, que es la forma más eficiente de generar mallas personalizadas en Blender. Requiere tres listas:
1.  **Vertices**: Lista de tuplas $(x, y, z)$.
2.  **Edges (Aristas)**: Tuplas que contienen los índices de los vértices a conectar (ej. `(0, 1)` conecta el primer punto con el segundo).
3.  **Faces (Caras)**: En este script se mantiene vacía `[]` para generar solo una estructura de "alambre" (wireframe).

3. Gestión de Escena
Para asegurar una generación limpia, el script incluye un bloque de **limpieza de entorno**:
* Utiliza operadores de selección global (`select_all`).
* Elimina cualquier objeto preexistente (cubos, cámaras o luces por defecto) para evitar solapamientos.



4. Algoritmo de Cierre (Módulo)
Para cerrar el polígono, se utiliza la operación de módulo:
`aristas.append((i, (i + 1) % lados))`

Esto permite que cuando el bucle llega al último vértice, el siguiente índice sea forzado a volver a `0`, creando una arista cerrada perfecta sin importar si es un triángulo, cuadrado o polígono de N lados.

5. Parámetros de Función
* `nombre`: Identificador del objeto en el Outliner de Blender.
* `lados`: Define la forma geométrica (3=triángulo, 4=cuadrado, etc.).
* `radio`: Distancia desde el centro (0,0,0) a cada vértice.
