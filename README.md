# 🚗 Proyecto: Coche Arduino con Inteligencia Artificial

Ivo Giuliano Cappetto

Este proyecto consiste en implementar un **modelo de red neuronal** entrenado en **Python (Colab)** y luego llevarlo a un **Arduino Uno** utilizando la simulación en **Wokwi**.  
El objetivo fue que el coche (simulado) pueda tomar decisiones en función de dos entradas, sin usar condicionales `if/else`, sino a partir del aprendizaje automático.

---

## 🧠 1. Arquitectura observada en el proyecto

Durante el análisis del proyecto original de Aprende Machine Learning, identificamos una red neuronal de tipo **feed-forward**, compuesta por:

| Capa | Descripción | Neuronas |
|------|--------------|----------|
| Entrada | Sensores (por ejemplo, distancia izquierda y derecha) | 2 |
| Oculta | Procesamiento interno con función de activación `tanh` | 3 |
| Salida | Acciones del coche (por ejemplo, avanzar, girar, detener) | 4 |

Se trata de una red pequeña, pensada para ser implementada en hardware limitado como el Arduino Uno.

---

## 🧩 2. Enfoques de resolución de problemas aplicados

| Enfoque | Descripción |
|----------|-------------|
| **Aprendizaje supervisado** | Se definieron ejemplos de entrada y salida esperados (tabla de verdad) para que la red aprenda el comportamiento del coche. |
| **Normalización** | Se escalaron los datos entre −1 y 1 para que la función `tanh` funcione correctamente. |
| **Entrenamiento iterativo** | Los pesos se ajustaron durante miles de épocas en Colab. |
| **Generalización** | La red puede responder a combinaciones nuevas sin usar reglas fijas. |
| **Despliegue embebido** | Los pesos obtenidos se cargaron en Arduino para ejecutarse directamente. |

---

## ⚙️ 3. Entrenamiento de la red (Colab)

El entrenamiento se realizó en Google Colab usando NumPy, con una red de arquitectura `[2, 3, 4]`.  
Luego de entrenar, se exportaron los pesos obtenidos:

**Pesos capa 1:**
[[0.0, 0.0, 0.0],
[-0.123, 2.352, -2.79],
[-2.153, 0.998, 0.839]]

**Pesos capa 2:**
[[1.275, 0.773, 1.572, 1.313],
[-1.265, -1.36, -1.156, -1.0],
[0.002, -0.446, 2.157, -2.299],
[2.304, -2.296, -0.427, -0.327]]


---

## 🧮 4. Simulación y nuevas pruebas

En la etapa siguiente, se agregaron dos entradas nuevas y una salida adicional para comprobar la capacidad de ajuste de la red.  
Se volvió a entrenar con la nueva tabla de verdad y se verificaron las salidas esperadas.  
Luego, con los pesos finales, se implementó el modelo en Arduino (Wokwi).

---

## 🧪 5. Resultados obtenidos en la simulación

Al ejecutar el código en **Wokwi** (monitor serial), se observaron las siguientes salidas:

=== Simulación de red neuronal ===

Entrada: (-1.00, -1.00)

Salida 1: 0.33

Salida 2: -0.61

Salida 3: 0.20

Salida 4: -0.18

Entrada: (0.00, 1.00)

Salida 1: 0.66

Salida 2: -0.72

Salida 3: 0.67

Salida 4: -0.03

Entrada: (1.00, -1.00)

Salida 1: 0.19

Salida 2: 0.59

Salida 3: -0.34

Salida 4: 0.76


Las respuestas varían suavemente según las entradas, lo que confirma que el modelo aprendió un comportamiento no lineal.

---

## 🔧 6. Implementación en Arduino (resumen)

El código del microcontrolador (archivo `sketch.ino`) reproduce el modelo matemático de la red, aplicando los pesos obtenidos en Python.

Se simularon tres entradas de prueba con resultados coherentes al entrenamiento previo.

---
