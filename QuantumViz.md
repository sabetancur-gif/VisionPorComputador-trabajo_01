---
title: "Taller 1: Fundamentos y calibración de cámara"
description: "Visión por Computador — Universidad Nacional de Colombia — Taller 1: calibración, transformaciones y segmentación."
layout: default
permalink: /
theme: minimal
---

<style>

/* Fuentes */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap');

:root{
  --bg:#f6f8fb;
  --card:#ffffff;
  --muted:#6b7280;
  --accent:#0f172a;
  --accent-2:#0ea5a4;
  --maxw:1200px;
}

/* Reset / body */
html,body{height:100%}
body{
  margin:0;
  padding:28px;
  font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
  background:linear-gradient(180deg,#fbfdff 0%, var(--bg) 100%);
  color:var(--accent);
  -webkit-font-smoothing:antialiased;
}

/* Layout */
.pro-wrapper{
  max-width: var(--maxw);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 28px;
  align-items: start;
  box-sizing: border-box;
  padding-bottom: 64px;
}

/* Sidebar */
#toc-sidebar{
  position: sticky;
  top: 28px;
  background: var(--card);
  border-radius: 12px;
  padding: 18px;
  box-shadow: 0 8px 24px rgba(11,15,30,0.06);
  border: 1px solid rgba(15,23,42,0.04);
  height: calc(100vh - 56px);
  overflow: auto;
}
#toc-sidebar h4{margin:0 0 10px 0;color:var(--accent-2);font-size:13px}
#toc-list{list-style:none;padding:0;margin:0}
#toc-list li{margin:8px 0;font-size:14px}
#toc-list li.h3{margin-left:10px;font-size:13px;color:var(--muted)}
#toc-list a{color:var(--accent);text-decoration:none}
#toc-list a:hover{text-decoration:underline}

/* Main content */
.pro-content{background:transparent;word-break:break-word}
.header-card{
  background:var(--card);
  padding:18px;
  border-radius:12px;
  box-shadow:0 8px 24px rgba(11,15,30,0.06);
  border:1px solid rgba(15,23,42,0.04);
  margin-bottom:18px;
}
.header-meta{display:flex;gap:20px;flex-wrap:wrap;color:var(--muted);font-size:14px}
.pro-content h1{font-size:28px;margin-top:4px;margin-bottom:8px}
.pro-content h2{font-size:20px;margin-top:28px;margin-bottom:8px}
.pro-content h3{font-size:16px;margin-top:18px;margin-bottom:6px}
.pro-content p{margin:8px 0;color:#10203a}
.pro-content ul{margin:6px 0 12px 20px}
.pro-content pre{background:#0b1220;color:#e6eef6;padding:12px;border-radius:8px;overflow:auto}

/* Section cards */
.section-card{
  background: var(--card);
  padding:20px;
  border-radius:12px;
  margin-bottom:18px;
  border: 1px solid rgba(15,23,42,0.04);
  box-shadow: 0 6px 18px rgba(11,15,30,0.03);
}

/* Floating actions */
.top-actions{
  position: fixed;
  right: 18px;
  bottom: 18px;
  display:flex;
  flex-direction:column;
  gap:10px;
  z-index:1200;
}
.btn{
  display:inline-flex;align-items:center;gap:8px;padding:10px 14px;background:var(--accent-2);color:white;border-radius:12px;border:none;box-shadow:0 8px 18px rgba(14,165,164,0.18);cursor:pointer;font-weight:700;text-decoration:none;font-size:14px;
}
.btn.secondary{background:#0f172a;padding:9px 12px}

.muted{color:var(--muted);font-size:13px}

/* Responsive */
@media (max-width:980px){
  .pro-wrapper{grid-template-columns:1fr;padding:0 12px}
  #toc-sidebar{position:relative;top:0;height:auto;margin-bottom:14px}
}

@media print{
  body{background:white;padding:0}
  #toc-sidebar{display:none}
  .pro-wrapper{grid-template-columns:1fr}
}

/* Smooth anchor scroll */
html { scroll-behavior: smooth; }
<style>

<!-- Layout HTML: sidebar + content wrapper -->
  
<div class="pro-wrapper">

  <aside id="toc-sidebar" aria-label="Tabla de contenido" role="navigation">
    <h4>📑 Índice</h4>
    <ul id="toc-list" aria-hidden="false"></ul>
    <div style="height:12px"></div>
    <div class="muted">Versión profesional · Responsive · Imprimible</div>
  </aside>

  <main class="pro-content" id="pro-content">
  
<!-- START: contenido original -->

# Taller 1 — Fundamentos y calibración de cámara

**Visión por Computador**  
**Universidad Nacional de Colombia**  
**Docente:** Juan David Ospina Arango

**Estudiantes:**  
- Santiago Betancur Montoya  
- Reinaldo David Lopez Narvaez  
- Jose Sebastian Garzon Parra  
- Monica Paola Vargas Tirado

---

## 📑 Tabla de contenido

1. [Introducción](#introducción)  
2. [Marco teórico](#marco-teórico)  
   1. [Distorsión de lente (barril/cojín)](#distorsión-de-lente-barrilcojín)  
   2. [Calibración de cámara](#calibración-de-cámara)  
   3. [Transformaciones geométricas](#tranformciones-geometricas)  
   4. [Transformaciones de intensidad a nivel de píxel](#transformaciones-de-intensidad-a-nivel-de-pixel)  
   5. [Ecualización de histogramas](#ecualización-de-histogramas)  
   6. [Segmentación por color](#segmentación-por-color)  
3. [Metodología](#metodología)  
   1. [Calibración de cámaras](#calibración-de-cámaras)  
   2. [Transformaciones de intensidad a nivel de píxel](#transformaciones-de-intensidad-a-nivel-de-pixel-1)  
   3. [Transformaciones de rotación y traslación](#transformaciones-de-rotación-y-traslación)  
   4. [Distribución de intensidades de una imagen](#distribución-de-intensidades-de-una-imagen)  
   5. [Segmentación de imágenes](#segmentación-de-imágenes)  
4. [Resultados y Análisis](#resultados-y-análisis)  
5. [Conclusión](#conclusion)  
6. [Reporte de contribución individual](#reporte-de-contribución-individual)  
7. [Referencias bibliográficas](#referencias-bibliográficas)

---

## Introducción

El procesamiento digital de imágenes constituye uno de los pilares fundamentales de la visión por computador, al permitir la interpretación automática de información visual mediante algoritmos matemáticos. En este primer taller se exploran los conceptos esenciales de calibración de cámara, transformaciones de intensidad y geométricas, ecualización de histogramas y segmentación por color, con el propósito de comprender y manipular digitalmente la información contenida en las imágenes.

El ejercicio se desarrolla de manera práctica utilizando fotografías capturadas con un teléfono celular, lo que permite simular un entorno real de adquisición de datos. A partir de dichas imágenes, se aplican técnicas básicas de preprocesamiento y análisis que permiten corregir distorsiones ópticas, modificar el brillo, contraste y niveles de iluminación, realizar transformaciones espaciales, mejorar la distribución tonal mediante ecualización y finalmente segmentar regiones de interés con base en sus características cromáticas.

Estas actividades permiten no solo afianzar los fundamentos teóricos del procesamiento de imágenes, sino también evidenciar cómo cada operación afecta la percepción visual y la información contenida en los píxeles. De esta forma, el taller integra conceptos de geometría, estadística e interpretación visual para construir una comprensión sólida del flujo de trabajo que precede a tareas más avanzadas de visión artificial, como la detección de objetos, clasificación o reconocimiento de patrones.

---

## Marco teórico

### Distorsión de lente (barril/cojín)

La distorsión de lente es una aberración óptica que provoca que las líneas rectas en una escena aparezcan curvadas en la imagen capturada. Este efecto se debe a la geometría y a la forma en que la lente proyecta la luz sobre el sensor de la cámara. Existen principalmente dos tipos de distorsión: la distorsión de barril, donde las líneas rectas se curvan hacia afuera desde el centro de la imagen, común en lentes gran angulares; y la distorsión de cojín, donde las líneas se curvan hacia adentro, típica en lentes teleobjetivos. Matemáticamente, estas distorsiones pueden modelarse mediante funciones polinomiales que dependen de la distancia radial al centro óptico. Corregir este tipo de errores requiere aplicar una transformación inversa basada en los parámetros intrínsecos de la cámara, lo cual permite obtener una imagen rectificada que se aproxima a la proyección ideal

### Calibración de cámara

El proceso de calibración de cámara se basa en estimar los parámetros intrínsecos (como la longitud focal, el centro óptico y los coeficientes de distorsión radial y tangencial) y los parámetros extrínsecos (rotación y traslación del sistema de cámara respecto al mundo) para establecer una relación precisa entre un punto 3D del mundo y su proyección 2D en la imagen capturada (Sadekar & Mallick, 2020).
Para obtener estos parámetros se capturan múltiples vistas de un patrón calibrado (frecuentemente un tablero de ajedrez), se localizan sus esquinas en la imagen, se asocian con las coordenadas del mundo definidas y se aplica un algoritmo como OpenCV calibrateCamera() para calcular la matriz intrínseca, los coeficientes de distorsión, y los vectores de rotación y traslación. Este procedimiento permite corregir distorsiones y mejorar mediciones basadas en imagen para aplicaciones como robótica, visión por computador y automóviles autónomos (GeeksforGeeks, 2025).

### Tranformciones Geometricas

Las transformaciones geométricas sobre imágenes permiten modificar su posición, orientación o tamaño sin alterar su contenido visual (al trabajar sobre la intensidad de cada pixel). Para representar estas transformaciones de manera uniforme y eficiente, se emplean las coordenadas homogéneas, que añaden una dimensión extra al sistema de coordenadas tradicional. Esto facilita expresar traslaciones, rotaciones y escalados mediante una única matriz homogénea, la cual combina todas estas operaciones en una misma formulación matemática. De esta forma, las transformaciones pueden aplicarse mediante multiplicaciones matriciales, simplificando el procesamiento y la composición de múltiples cambios geométricos sobre la imagen.

### Transformaciones de intensidad a nivel de pixel

El procesamiento digital de imágenes se fundamenta en la aplicación de transformaciones puntuales que modifican las propiedades visuales de una imagen a nivel de píxel. Entre las más comunes se encuentran el ajuste de brillo, que incrementa o reduce la luminosidad global al sumar o restar un valor constante; el ajuste de contraste, que amplía o comprime el rango tonal para acentuar o suavizar las diferencias entre zonas claras y oscuras; y la corrección gamma, una operación no lineal que compensa las características de visualización de los dispositivos y la percepción humana, equilibrando el brillo y el contraste de forma más natural. Estas transformaciones son esenciales para optimizar la visualización y mejorar la calidad perceptual de las imágenes digitales (López, 2012).
Asimismo, el tratamiento de imágenes puede incluir operaciones aritméticas como suma, resta, multiplicación y división entre imágenes o con constantes. Estas permiten realizar tareas de realce, fusión o comparación visual, destacando diferencias o atenuando regiones específicas. Por ejemplo, la suma puede aumentar el brillo o combinar dos imágenes, la resta resalta variaciones entre ellas, la multiplicación se emplea para aplicar máscaras o modificar la iluminación, y la división sirve para detectar cambios o corregir irregularidades de luz. En conjunto, estas transformaciones constituyen la base del análisis y procesamiento visual en múltiples aplicaciones de la visión por computador y la ingeniería digital (Solución Ingenieril, s. f.).

### Ecualización de histogramas

La ecualización de histograma es una técnica de mejora del contraste que busca redistribuir los niveles de intensidad de una imagen para utilizar de manera más uniforme todo el rango dinámico disponible.
Este proceso se basa en la función de distribución acumulada (CDF) del histograma original, que transforma los valores de intensidad r en nuevos valores s, dando como resultado una imagen con un contraste más equilibrado y una mejor diferenciación entre regiones claras y oscuras. Esta técnica es especialmente útil en imágenes con iluminación desigual o bajo contraste, como fotografías nocturnas o subexpuestas, aunque puede incrementar el ruido en áreas uniformes.

### Segmentación por color

La segmentación de imágenes permite dividir una imagen en regiones que representan objetos o áreas de interés, facilitando su análisis. En este caso, se utiliza para reconocer objetos de distintos colores, contarlos y calcular su tamaño en píxeles.

Para lograrlo, se emplean los espacios de color HSV y LAB, que ayudan a distinguir mejor los tonos y la iluminación. Con el uso de máscaras y operaciones morfológicas, se aísla la zona de interés (como la mesa) y se eliminan ruidos del fondo. Finalmente, se obtienen los contornos y el área de cada objeto, permitiendo una identificación precisa y visualmente clara de los colores presentes en la escena.

---

## Metodología

### Calibración de cámaras

Se imprime un patrón calibrado (por ejemplo un tablero de ajedrez) y se toman múltiples imágenes desde distintas orientaciones y distancias para abarcar diversas perspectivas del patrón. Luego se detectan las esquinas del patrón en cada imagen y se asocian estos puntos 2D con sus coordenadas espaciales 3D conocidas, tras lo cual se aplica la función de calibración (OpenCV calibrateCamera()) para estimar los parámetros intrínsecos (matriz de cámara) y de distorsión, así como los vectores de rotación y traslación, y finalmente se verifican los resultados undistorcionando nuevas imágenes y comprobando el error de reproyección.

### Transformaciones de intensidad a nivel de pixel

Se definieron diversas funciones para realizar transformaciones sobre las imágenes, entre ellas ajuste_brillo(), ajuste_contraste() y corrección_gamma(), junto con funciones auxiliares destinadas al manejo y normalización de las mismas. Posteriormente, se procedió a cargar las fotografías de la fachada tomadas a las 6:00 a.m. y a las 7:00 p.m., sobre las cuales se aplicaron las transformaciones mencionadas, con el propósito de analizar y visualizar los efectos de cada ajuste sobre la imagen original.

De manera complementaria, se implementaron funciones para realizar operaciones aritméticas entre imágenes, tales como suma(), resta(), multiplicación() y división(). Estas operaciones se aplican igualmente a las imágenes capturadas a las 6:00 a.m. y 7:00 p.m., con el fin de observar cómo dichas combinaciones matemáticas afectan la composición visual y los valores de intensidad de los píxeles, permitiendo una comprensión más profunda de los principios de procesamiento digital de imágenes.

### Transformaciones de rotación y traslación

Iniciamos con la creación de funciones que permiten construir matrices en coordenadas homogéneas para las transformaciones de rotación, escalamiento y traslación, cada una definida según los parámetros específicos que la determinan. Con estas funciones se desarrolla posteriormente una rutina que genera la matriz homogénea compuesta, la cual combina las transformaciones básicas en una única representación matricial, facilitando su aplicación sobre imágenes digitales.

A partir de esta composición, se generan múltiples matrices homogéneas (por defecto, ocho) modificando los parámetros de rotación, escalamiento y traslación para cada una. Estas matrices se aplican a una imagen previamente cargada, obteniendo un conjunto de resultados que se almacenan como frames. Posteriormente, los frames se integran para formar un GIF que muestra la secuencia de transformaciones. Todas las operaciones se realizaron tomando como referencia el centro de la imagen, por lo que la aplicación de cada transformación depende directamente de sus dimensiones. Además, se aplicó un padding a cada frame con el fin de evitar la aparición de zonas negras alrededor de la imagen transformada.

### Distribución de intensidades de una imagen

Se cargaron dos imágenes de la misma fachada tomadas en diferentes condiciones de iluminación (6 AM y 7PM). Ambas fueron redimensionadas y convertidas a escala de grises para analizar únicamente la distribución de intensidades. Posteriormente, se aplicó la ecualización de histograma utilizando la función cv.equalizeHist() de OpenCV, con el fin de redistribuir los niveles de brillo y mejorar el contraste.

Finalmente, se calcularon y graficaron los histogramas y funciones de distribución acumulada (CDF) antes y después del proceso para comparar los cambios en la representación tonal entre la imagen diurna y la nocturna.

### Segmentación de imágenes

Para esta actividad, nuestro grupo capturó una imagen en una oficina con varios objetos de diferentes colores sobre una mesa, usando la cámara de un teléfono celular. Empleando las librerías OpenCV y NumPy para el manejo de imágenes y operaciones numéricas. La imagen fue cargada, redimensionada y convertida a los espacios de color HSV y LAB, lo que permitió trabajar con información de tono, saturación y luminosidad de forma más precisa que en el formato RGB.

El paso más importante fue la creación de máscaras, utilizadas para aislar la superficie de la mesa y excluir el fondo o las paredes. Estas máscaras se generaron mediante condiciones de brillo y saturación, y luego se limpiaron con operaciones morfológicas de apertura y cierre para eliminar el ruido. La máscara final definió la región de interés, sobre la cual se realizó toda la segmentación por color, evitando errores en zonas no relevantes.

Finalmente, se aplicaron rangos de color en el espacio HSV para detectar objetos azules, verdes, rojos, naranjas, blancos y grises. Con las máscaras de cada color se identificaron los contornos de los objetos, se filtraron por área mínima y se calculó su tamaño en píxeles. Los resultados se visualizaron en una imagen anotada que muestra los objetos detectados y sus áreas, comprobando la efectividad del uso de las máscaras y las librerías empleadas para la segmentación.

---

## Resultados y Análisis

### Calibración de cámaras

Los resultados obtenidos del proceso de calibración muestran una buena consistencia en los parámetros intrínsecos y una representación fiel del comportamiento óptico de la cámara. Se determinó que la distorsión predominante es de tipo barril, lo cual se evidencia tanto en los valores positivos de los coeficientes radiales 𝑘_2 y 𝑘_3, como en la curvatura convexa de las líneas rectas hacia los bordes de las imágenes originales. Los valores de las longitudes focales 𝑓_𝑥 = 280.4 y 𝑓_𝑦 = 281.6 resultaron muy similares, indicando una correcta proporción entre los ejes del sensor y una calibración precisa, sin deformaciones anisótropas significativas. Asimismo, el punto principal (𝑐_𝑥, 𝑐_𝑦) = (183.67, 164.88) se encuentra próximo al centro de la imagen, lo que confirma una adecuada alineación entre el eje óptico y el sensor. En conjunto, estos resultados reflejan una calibración estable y coherente, reforzada por un bajo error RMS de reproyección (≈ 0.27), que garantiza una correspondencia precisa entre los puntos proyectados y observados. La corrección aplicada eliminó eficazmente la distorsión radial, obteniendo imágenes rectificadas con líneas bien alineadas, lo cual valida la calidad del modelo de cámara empleado.

### Transformaciones de intensidad a nivel de pixel

La aplicación de transformaciones de intensidad a nivel de píxel permitió modificar de forma controlada las características visuales de las imágenes según las condiciones de iluminación. En la imagen diurna, los ajustes de brillo y contraste evidenciaron que el aumento del brillo realza las zonas claras pero puede provocar pérdida de detalle por saturación, mientras que un incremento del contraste mejora la definición de bordes y sombras al ampliar el rango tonal. Por su parte, la corrección gamma (γ < 1) permitió iluminar de manera más uniforme sin saturar los valores altos de intensidad, siendo especialmente útil para compensar condiciones de baja iluminación.

En la imagen nocturna, los mismos ajustes contribuyeron a resaltar detalles ocultos en las sombras, aunque un incremento excesivo del brillo introdujo cierto ruido visual. Las operaciones aritméticas entre imágenes (A y B) mostraron diferentes comportamientos: la suma (A + B) generó una fusión más brillante que combina información de ambas tomas; la resta (|A − B|) resaltó las diferencias de iluminación y color entre el día y la noche; la multiplicación (A × B) oscureció la escena, siendo útil para analizar regiones comunes; y la división (A ÷ B) amplificó las diferencias de luminancia, destacando las estructuras más iluminadas. En conjunto, estos resultados demuestran que las transformaciones de intensidad son herramientas fundamentales en visión por computador, al mejorar la percepción visual, realizar correcciones fotométricas y facilitar la segmentación o detección de características bajo condiciones de iluminación variables.

### Transformaciones de rotación y traslación

Al implementar y aplicar las transformaciones de rotación y traslación, se obtuvieron resultados visuales claros del efecto progresivo de cada operación. El código desarrollado permitió cargar una imagen base y generar entre ocho y doce transformaciones sucesivas, variando los parámetros de rotación, traslación y escala en cada paso. Cada resultado intermedio se almacenó como un frame, evidenciando los cambios graduales en la posición y orientación de la imagen. Finalmente, la secuencia completa de frames se integró en un GIF animado que muestra de manera continua y dinámica el proceso de transformación. Este resultado permite observar cómo la composición de transformaciones homogéneas produce efectos coherentes y visualmente fluidos sobre la imagen original.

Además, para evitar la aparición de zonas negras en los bordes de la imagen durante las transformaciones, se implementó un método de padding basado en el reflejo de los píxeles del borde. Esta técnica permitió extender el contenido de la imagen hacia las áreas que quedaban vacías tras las rotaciones o traslaciones, logrando que cada frame mantuviera una apariencia uniforme y continua. Gracias a este procedimiento, el GIF final presenta una transición más limpia y sin interrupciones visuales en los límites de la imagen.

### Distribución de intensidades de una imagen

Tras aplicar la ecualización del histograma, se observó un incremento notable en el contraste general de ambas imágenes, especialmente en la fotografía nocturna.
En la imagen diurna, la ecualización generó cambios leves al redistribuir los valores de intensidad, ya que la iluminación original ya era uniforme. En contraste, la imagen nocturna presentó una ampliación significativa del rango dinámico, evidenciada en el histograma, que pasó de estar concentrado en los niveles bajos a distribuirse de manera más homogénea en todo el espectro de intensidades.

El resultado visual confirma que la ecualización mejora la visibilidad de detalles en escenas subexpuestas, permitiendo distinguir elementos que antes estaban ocultos por la baja iluminación. Sin embargo, también se aprecia un aumento del ruido en algunas zonas oscuras debido al realce de las diferencias de intensidad.

En conjunto, el análisis demuestra que la ecualización del histograma es especialmente efectiva para mejorar el contraste en condiciones de iluminación deficiente, aunque su efecto en imágenes bien expuestas es más limitado.

### Segmentación de imágenes

El programa logró reconocer correctamente los objetos de distintos colores que aparecen en la imagen tomada en la oficina. En total se identificaron 15 objetos: 4 azules, 1 verde, 2 naranjas, 3 blancos, 3 grises y 2 rojos. A cada uno se le calculó su tamaño en píxeles, mostrando una buena relación con su tamaño real en la foto. En la imagen final se pueden ver los contornos bien marcados y los colores detectados con bastante precisión.

Las máscaras fueron muy importantes porque ayudaron a concentrar la detección solo en la mesa y a evitar confusiones con el fondo o las paredes. Gracias a esto, los resultados fueron mucho más limpios y ordenados. En general, el programa funcionó bien, ya que pudo diferenciar los colores sin problemas y mostrar claramente los objetos presentes en la escena.

---

## Conclusion

En conclusión, el desarrollo de este taller permitió comprender de manera integral los fundamentos teóricos y prácticos del procesamiento digital de imágenes aplicados a la calibración de cámaras y al análisis visual. A través de las distintas actividades, desde la corrección de distorsiones ópticas hasta la segmentación por color, se evidenció cómo las transformaciones geométricas, de intensidad y el manejo de histogramas contribuyen a mejorar la calidad, precisión y utilidad de la información visual. Además, la implementación práctica con herramientas de *OpenCV* y *Python* facilitó la conexión entre la teoría y la aplicación real, fortaleciendo la comprensión del flujo de trabajo en visión por computador. En conjunto, el taller consolidó habilidades esenciales para futuras tareas de detección, reconocimiento y análisis automático de imágenes en diversos entornos.

---

## Reporte de contribución individual

- Punto 01: Realizado entre todos
- Punto 01: Reinaldo David Lopez Narvaez
- Punto 03: Santiago Betancur Montoya
- Punto 04: Monica Paola Vargas Tirado
- Punto 05: Jose Sebastian Garzon Parra

Posteriormente, nos fuimos reuniendo de forma periódica para revisar conjuntamente la solución de los diferentes puntos.
Luego, tomamos la decisión de crear un archivo .ipynb, de modo que cada integrante tuviera un espacio para escribir e implementar la forma en que pensó y ejecutó el ejercicio.
En cuanto al informe, la estructura de carpetas y otros aspectos a desarrollar, su elaboración fue un trabajo conjunto.

---

## Referencias bibliográficas

- Solución Ingenieril. (s. f.). *Operaciones aritméticas con imágenes - Visión artificial*. [https://solucioningenieril.com/vision_artificial/operaciones_aritméticas_con_imágenes](https://solucioningenieril.com/vision_artificial/operaciones_aritméticas_con_imágenes)  
- López, J. F. (2012, noviembre 2). *Procesamiento digital de imágenes*. Blog de WordPress. [https://procesamientodigitalimagenes.wordpress.com/](https://procesamientodigitalimagenes.wordpress.com/)  
- GeeksforGeeks. (2025, julio 15). Camera Calibration with Python – OpenCV. https://www.geeksforgeeks.org/python/camera-calibration-with-python-opencv/  
- Sadekar, K., & Mallick, S. (2020, febrero 25). Camera Calibration using OpenCV. https://learnopencv.com/camera-calibration-using-opencv/?authuser=1

<!-- END: contenido original -->

  </main>
</div>

<script>
/*
  Genera la TOC sidebar a partir de los headings h2/h3 que ya estarán presentes
  en el HTML final. Esta versión es segura dentro de Jekyll si se envuelve con raw.
*/
(function(){
  function slugify(s){
    return String(s).toLowerCase().trim()
      .replace(/[^a-z0-9\\s-áéíóúñü]/g,'')
      .replace(/\\s+/g,'-');
  }

  function buildTOC(){
    var toc = document.getElementById('toc-list');
    if(!toc) return;
    // busca headings dentro del main
    var container = document.getElementById('pro-content') || document;
    var nodes = container.querySelectorAll('h2, h3');
    toc.innerHTML = '';
    nodes.forEach(function(h){
      if(!h.id) h.id = slugify(h.textContent);
      var li = document.createElement('li');
      li.className = h.tagName.toLowerCase();
      var a = document.createElement('a');
      a.href = '#'+h.id;
      a.textContent = h.textContent;
      li.appendChild(a);
      if(h.tagName.toLowerCase() === 'h3') li.classList.add('h3');
      toc.appendChild(li);
    });
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', buildTOC);
  } else {
    buildTOC();
  }
})();
</script>

<!-- Accesos rápidos -->
<div class="top-actions" aria-hidden="false">
  <a class="btn" href="#pro-content">🔎 Ir al contenido</a>
  <a class="btn secondary" href="#toc-sidebar">📑 Índice</a>
</div>

