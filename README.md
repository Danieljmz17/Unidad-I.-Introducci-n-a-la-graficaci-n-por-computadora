# Unidad-I.-Introducci-n-a-la-graficaci-n-por-computadora

1.1 Historia y Evolución de la Graficación por Computadora

La graficación por computadora surge en la década de 1950 con el uso de pantallas de rayos catódicos (CRT) para visualizar datos científicos y trayectorias militares.
En los años 60, Ivan Sutherland desarrolló Sketchpad, considerado el primer sistema interactivo de gráficos por computadora, marcando el inicio de la interacción humano-máquina.
Durante los 80 y 90, con la aparición de las computadoras personales y tarjetas VGA, surge la era del rasterizado, permitiendo gráficos a color y el nacimiento de las interfaces gráficas (GUI).
En los 2000, con el desarrollo de las GPU programables, se introducen técnicas como sombreado en tiempo real y renderizado avanzado (Ray Tracing).
Actualmente, la graficación incluye realidad virtual, inteligencia artificial y simulación física avanzada.

1.2 Áreas de Aplicación

La graficación por computadora tiene múltiples aplicaciones:
Ciencia y medicina (visualización MRI y tomografías)
Arquitectura (recorridos virtuales)
Videojuegos y cine
Simulación y capacitación
Interfaces UI/UX

1.3 Aspectos Matemáticos de la Graficación

La graficación se fundamenta en:
Geometría analítica
Álgebra lineal (vectores y matrices)
Transformaciones (traslación, rotación, escalado)
Trigonometría (seno y coseno)

Ejemplo:
En Blender usamos:

x = radio * cos(angulo)
y = radio * sin(angulo)
para posicionar objetos en un patrón circular.

1.4 Modelos de Color: RGB, CMY, HSV y HSL
RGB (Red, Green, Blue)
Modelo aditivo usado en pantallas.
Combina luz roja, verde y azul.
CMY (Cyan, Magenta, Yellow)
Modelo sustractivo usado en impresión.
HSV (Hue, Saturation, Value)
Organiza el color según tono, saturación y brillo.
HSL (Hue, Saturation, Lightness)
Similar a HSV pero con mejor control de luminosidad.

Iluminar un cubo en Blender
Crear un cubo.
Agregar luz tipo Point o Sun.
Activar modo Rendered.
Ajustar intensidad y posición.
Aplicar material con Principled BSDF.
Modificar Roughness y Metallic.
Ajustar sombras.

1.5 Representación y Trazo de Líneas y Polígonos
Las líneas y polígonos son la base del modelado gráfico.
Una línea se define por dos puntos (x1, y1) y (x2, y2).
Un polígono es una figura cerrada formada por múltiples segmentos.
En gráficos rasterizados se usan algoritmos como:
• Algoritmo de Bresenham
• Algoritmo DDA

1.5.1 Formatos de Imagen
BMP: mapa de bits sin compresión
JPEG: compresión con pérdida
PNG: compresión sin pérdida
GIF: animación básica
SVG: vectorial
TIFF: alta calidad

# Prácticas incluidas

• Dibujo de un polígono en Blender

import bpy
import math

def crear_poligono_2d(nombre, lados, radio):
    # Crear malla y objeto
    malla = bpy.data.meshes.new(nombre)
    objeto = bpy.data.objects.new(nombre, malla)
    bpy.context.collection.objects.link(objeto)

    vertices = []
    aristas = []

    # Crear vértices
    for i in range(lados):
        angulo = 2 * math.pi * i / lados
        x = radio * math.cos(angulo)
        y = radio * math.sin(angulo)
        vertices.append((x, y, 0))

    # Crear aristas
    for i in range(lados):
        aristas.append((i, (i + 1) % lados))

    # Construir la malla
    malla.from_pydata(vertices, aristas, [])
    malla.update()


Borrar objetos existentes
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Crear el polígono
crear_poligono_2d("poligono2D", lados=6, radio=5)

<img width="1528" height="915" alt="image" src="https://github.com/user-attachments/assets/82b28418-e15e-48d9-96c0-2a699a903865" />



# Generación de la Flor de la Vida usando trigonometría

import bpy
import math

# Limpiar escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura
radio = 3
angulo_actual = 0
paso_angular = 60  # Cada 60 grados

# Círculo central
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

while angulo_actual < 360:

    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))

    bpy.ops.mesh.primitive_circle_add(
        radius=radio,
        location=(x, y, 0),
        vertices=64
    )

    # Evita bucle infinito
    angulo_actual += paso_angular

<img width="1542" height="957" alt="image" src="https://github.com/user-attachments/assets/acf56d28-9bc7-408b-888b-d7b1008bdf29" />


1.6 Procesamiento de Mapas de Bits

Un mapa de bits está compuesto por píxeles organizados en una matriz.

Operaciones comunes:

Filtros (blur, sharpen)
Conversión a escala de grises
Manipulación por canales RGB

Cada píxel almacena información de color.

Bibliografía

Foley, J. D., van Dam, A., Feiner, S. K., & Hughes, J. F. (1996). Computer graphics: Principles and practice. Addison-Wesley.

Shirley, P., & Marschner, S. (2009). Fundamentals of computer graphics. A K Peters.

Blender Foundation. (2024). Blender Documentation. https://docs.blender.org/

Sutherland, I. (1963). Sketchpad: A man-machine graphical communication system. MIT.
