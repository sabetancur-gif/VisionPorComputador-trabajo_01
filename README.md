# Visión por Computador: QuantumViz

## 🧠 Trabajo 01: Fundamentos y calibración de una cámara

### 📄 Descripción

Este repositorio contiene el folder **`QuantumViz_Vision-Computador`**, en el cual se encuentra la estructura de carpetas del proyecto y el notebook **`Trabajo_01_VisionPorComputador.ipynb`**, que presenta la solución propuesta por el grupo **QuantumViz** a los ejercicios solicitados.

Se emplean técnicas de procesamiento de imágenes y transformaciones geométricas, incluyendo rotaciones, traslaciones, generación de GIFs y videos, detección de esquinas, entre otras.

---

### ⚙️ Requisitos

Los paquetes necesarios están listados en el archivo **`requirements.txt`**.  
Para instalarlos localmente, ejecute en la terminal:

```bash
python -m pip install -r requirements.txt
```

### ▶️ Ejecución del notebook

Descargue completamente el contenido del repositorio.

Ábralo en **Visual Studio Code** (o el entorno de su preferencia).

Asegúrese de tener instalados los requerimientos que aparecen en el archivo **`requirements.txt`**.

Ejecute el archivo **`Trabajo_01_VisionPorComputador.ipynb`**, ubicado en la raíz del proyecto.

Durante la ejecución celda por celda, el programa hará uso de la estructura de carpetas creada para almacenar y acceder a los resultados.


### 📂 Estructura del proyecto

```plaintext
QUANTUMVIZ_VISION-COMPUTADORA/
│
├─ Trabajo_01_VisionPorComputador.ipynb
├─ requirements.txt
├─ README.md
│
├─ Dataset/                         # Archivos requeridos en cada punto
│  ├─ Tablero/                      # Imágenes para el punto 1
│  │   └─ img_*.jpeg                # Donde * varía de 7 hasta 30
│  ├─ Fachada/                      # Imágenes para los puntos 2 y 4
│  │   ├─ fachada_dia.jpg
│  │   └─ fachada_noche.jpg
│  ├─ paisaje.jpg                   # Imagen para el punto 3
│  └─ escritorio.jpg                # Input para el punto 5
│
├─ Resultados/
│  ├─ resultados_calibracion/       # Resultados ejercicio 1
│  ├─ transformaciones_intensidad/  # Resultados ejercicio 2
│  ├─ transformaciones_geometricas/ # Resultados ejercicio 3
│  ├─ distribucion_intensidades/    # Resultados ejercicio 4
│  └─ segmentacion/                 # Resultados ejercicio 5
│
└─ Documentacion/
   └─ QuantumViz.pdf                # PDF con teoría, metodología, resultados y análisis
```

> Nota:
> En el punto 3, en los resultados mostrados en la celda correspondiente dentro del archivo .ipynb, no se visualizará el GIF. Para poder verlo, deberá acceder a la carpeta donde se encuentra almacenado el archivo generado. (Resultados/transformaciones_geometricas/transformaciones.gif)



