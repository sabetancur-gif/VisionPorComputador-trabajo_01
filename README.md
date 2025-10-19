# Vision por Computador: QuantumViz


# Trabajo 01: fundamentos y calibración de una cámara

**Descripción**

Este repositorio contiene el folder QuantumViz_Vision-Computadoro en el cual encontraran una estructura de carpetas al igual que el notebook Trabajo_01_VisionPorComputador.ipynb, el cual presenta la solución propuesta por el grupo QuantumViz a los ejercicios solicitados, haciendo uso de técnicas de procesamiento de imágenes y transformaciones geométricas (rotaciones, traslaciones, generación de GIFs y videos, detección de esquinas, entre otras).


## Requisitos

Los paquetes necesarios están listados en 'requirements.txt'. Para instalarlos localmente:

bash
python -m pip install -r requirements.txt

## Ejecutar el notebook

En primera instancia, debe descargarse completamente el contenido del repositorio y posteriormente abrirlo en Visual Studio Code. Asegúrese de tener instalados los requerimientos que aparecen en el archivo *requirements.txt*.
Luego, ejecute el archivo *Trabajo_01_VisionPorComputador.ipynb*, ubicado en la raíz del proyecto.
A medida que se ejecute celda por celda, el programa hará uso de la estructura de carpetas creada.

## Estructura

La estructura de carpetas desarrollada por el equipo para este trabajo, presenta la siguiente forma

QUANTUMVIZ_VISION-COMPUTADORA/Trabajo_01
├─ Trabajo_01_VisionPorComputador.ipynb
├─ requirements.txt
├─ README.md
├─ Dataset/ `Contiene los archivos requeridos en cada punto`
  ├─ Tablero/ `Imagenes necesarias para el desarrollo del punto 1`
      └─ img_*.jpeg `Donde * varia desde 7 hasta 30`
  ├─ Fachada/ `Imagenes necesarias para el desarrollo del punto 2 y 4`
    ├─ fachada_dia.jpg
    └─ fachada_noche.jpg
  ├─ paisaje.jpg `Imagen necesaria para la ejecucion del punto 3`
  └─ escritorio.jpg `respectivo input para la solucion del punto5`
├─ Resultados/
  ├─ resultados_calibracion `Resultados ejercicio 1`
  ├─ transformaciones_intensidad `Resultados ejercicio 2`
  ├─ transformaciones_geometricas `Resultados ejercicio 3`
  ├─ distribucion_intensidades `Resultados ejercicio 4`
  └─ segmentacion `Resultados ejercicio 5`
└─ Documentacion
  └─ QuantumViz.PDF ` PDF con teoría, metodología, resultados y análisis`
  
> Nota: 
> En el punto 3, en los resultados mostrados en la celda correspondiente dentro del archivo .ipynb, no se visualizará el GIF. Para poder verlo, deberá acceder a la carpeta donde se encuentra almacenado el archivo generado. (Resultados/transformaciones_geometricas/transformaciones.gif)





