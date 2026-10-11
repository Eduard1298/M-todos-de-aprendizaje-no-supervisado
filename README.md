# Sistema de Transporte de Tunja — Aprendizaje No Supervisado 🚌📊

**Actividad 4 — Métodos de aprendizaje no supervisado**
Curso de Inteligencia Artificial

## Introducción

En las actividades anteriores se desarrollaron sistemas de transporte urbano de Tunja utilizando reglas lógicas y métodos de aprendizaje supervisado. En esta actividad se implementa un enfoque diferente mediante **aprendizaje no supervisado**, utilizando el algoritmo **K-Means** para identificar grupos de viajes similares según su distancia y tiempo de recorrido.

El objetivo del proyecto es analizar los patrones de movilidad del sistema de transporte simulado de Tunja, agrupando los viajes automáticamente sin indicarle al modelo cuáles tienen transbordo o cuáles corresponden a trayectos directos.

Para desarrollar el ejercicio, se genera un **dataset sintético de 350 viajes**, construido a partir de lugares, rutas y tiempos de referencia definidos en el código. Posteriormente, se utiliza `scikit-learn` para aplicar K-Means, dividir los viajes en tres grupos y visualizar los resultados mediante una gráfica.

Es importante aclarar que los tiempos y las distancias son simulados para fines académicos y no corresponden a mediciones reales del sistema de transporte.

## Objetivos del proyecto

* Aplicar el algoritmo K-Means como método de aprendizaje no supervisado.
* Generar datos simulados de viajes entre diferentes lugares de Tunja.
* Agrupar los viajes según la distancia recorrida y el tiempo de viaje.
* Analizar las características de los grupos identificados por el modelo.
* Evaluar si los grupos encontrados presentan diferencias en la frecuencia de transbordos.
* Asignar un viaje nuevo a uno de los grupos y visualizar los resultados.

## Contenido del repositorio

```text
├── sistema_transporte_tunja_kmeans.py  # Código fuente del proyecto
├── README.md                           # Documentación del proyecto
```

Al ejecutar el programa, se genera una gráfica con los grupos identificados y los centros de cada agrupación.

## ¿Cómo funciona el programa?

El sistema se desarrolla en seis etapas:

1. **Base de conocimiento:** se definen 21 lugares, 10 rutas de transporte y sus tiempos de referencia. Esta información sirve como base para simular los recorridos.

2. **Generación de datos:** mediante la función `simular_viaje()`, se calculan el número de paradas, la distancia aproximada y el tiempo estimado. También se simulan condiciones como la hora pico, la lluvia y los transbordos. El programa genera hasta 350 viajes válidos y utiliza una semilla aleatoria para favorecer la reproducibilidad de los resultados.

3. **Preparación de los datos:** se seleccionan las variables `distancia_km` y `tiempo_viaje_min`. Posteriormente, se aplica `StandardScaler` para estandarizar ambas variables y evitar que sus diferentes escalas afecten desproporcionadamente el agrupamiento.

4. **Entrenamiento del modelo:** se configura K-Means con tres grupos (`n_clusters=3`). El algoritmo identifica agrupaciones a partir de la similitud entre las distancias y los tiempos de viaje, sin utilizar etiquetas previamente definidas.

5. **Interpretación e inferencia:** se analizan los promedios de distancia, tiempo y transbordos de cada grupo. Después, se clasifica un viaje nuevo de 2,0 km y 25 minutos para identificar a qué grupo pertenece.

6. **Visualización:** se genera una gráfica de dispersión que muestra los viajes agrupados por colores y los centros de cada cluster, representados con una X negra.

## Variables utilizadas

| Variable           | Tipo          | Descripción                                   |
| ------------------ | ------------- | --------------------------------------------- |
| `num_paradas`      | Entero        | Número de paradas recorridas en el trayecto.  |
| `distancia_km`     | Decimal       | Distancia aproximada del viaje en kilómetros. |
| `hora_pico`        | Binaria (0/1) | Indica si el viaje ocurre en hora pico.       |
| `lluvia`           | Binaria (0/1) | Indica si se simulan condiciones de lluvia.   |
| `transbordo`       | Binaria (0/1) | Indica si el recorrido requiere transbordo.   |
| `tiempo_viaje_min` | Decimal       | Tiempo simulado del viaje en minutos.         |
| `cluster`          | Entero        | Grupo asignado por el algoritmo K-Means.      |

**Importante:** el modelo utiliza únicamente `distancia_km` y `tiempo_viaje_min` para construir los grupos. Las demás variables permiten describir los viajes y analizar los resultados, pero no se utilizan para entrenar el agrupamiento.

## Algoritmo utilizado: K-Means

K-Means es un algoritmo de aprendizaje no supervisado que agrupa datos según su similitud. Para este proyecto se establecen tres clusters, de manera que el algoritmo busque tres grupos de viajes con características similares.

El procedimiento consiste en:

* Definir la cantidad de grupos que se desean identificar.
* Inicializar los centros de los clusters.
* Asignar los viajes al centro más cercano según las variables estandarizadas.
* Actualizar los centros de acuerdo con los datos asignados.
* Repetir el proceso hasta alcanzar la convergencia.

En este ejercicio, los grupos se forman considerando la distancia y la duración de los viajes. Posteriormente, se comparan con la variable `transbordo` para observar si determinados grupos presentan una mayor proporción de recorridos con transbordo.

Esta comparación es únicamente interpretativa: **K-Means no recibe la información de transbordo durante el entrenamiento ni garantiza que pueda identificarla correctamente**.

## Tecnologías utilizadas

| Tecnología   | Uso                                                       |
| ------------ | --------------------------------------------------------- |
| Python       | Lenguaje de programación.                                 |
| NumPy        | Operaciones numéricas y generación de valores aleatorios. |
| Pandas       | Organización y análisis de los datos en tablas.           |
| Scikit-learn | Implementación de K-Means y estandarización de variables. |
| Matplotlib   | Creación de la gráfica de agrupamiento.                   |

## Cómo instalar y ejecutar el proyecto

### 1. Requisitos previos

* Tener Python 3.10 o una versión compatible instalada.
* Disponer del archivo `sistema_transporte_tunja_kmeans.py`.
* Contar con una terminal o consola de comandos.

### 2. Instalar las dependencias

Abre una terminal en la carpeta del proyecto y ejecuta:

```bash
pip install numpy pandas scikit-learn matplotlib
```

### 3. Ejecutar el programa

```bash
python sistema_transporte_tunja_kmeans.py
```

Si el comando `python` no funciona en Windows, puedes intentar:

```bash
py sistema_transporte_tunja_kmeans.py
```

### 4. Consultar los resultados

Al ejecutar el programa, se muestran en la consola:

* La cantidad de viajes simulados.
* Los primeros registros utilizados para el agrupamiento.
* La cantidad de viajes asignados a cada cluster.
* Los promedios de distancia, tiempo y transbordos por grupo.
* Una interpretación de las características de cada agrupación.
* El cluster asignado a un viaje nuevo de 2,0 km y 25 minutos.

Finalmente, se abre una ventana con la gráfica de dispersión y los centros de los tres grupos.

## Resultados y análisis

El programa genera tres clusters que representan agrupaciones de viajes con características similares en distancia y duración.

Los resultados se pueden interpretar de la siguiente manera:

* **Grupos de viajes cortos:** pueden concentrar recorridos con distancias y tiempos relativamente bajos.
* **Grupos de viajes intermedios:** pueden representar trayectos con duraciones y distancias moderadas.
* **Grupos de viajes largos:** pueden reunir recorridos con mayores distancias o tiempos de viaje.

Estas descripciones son orientativas. La interpretación definitiva debe realizarse a partir de los promedios que imprime el programa, ya que K-Means no garantiza que los grupos correspondan exactamente a esas categorías.

La variable `transbordo` permite examinar si existen diferencias entre los clusters. Sin embargo, encontrar esas diferencias no demuestra que el algoritmo haya aprendido a detectar transbordos, pues la agrupación se realiza exclusivamente con la distancia y el tiempo.

## Conclusiones

* Se implementó un modelo de aprendizaje no supervisado utilizando el algoritmo K-Means para agrupar viajes simulados del sistema de transporte de Tunja.
* La estandarización de las variables permitió trabajar con la distancia y el tiempo en escalas comparables.
* El modelo identificó tres agrupaciones sin utilizar etiquetas previas, demostrando el funcionamiento básico del aprendizaje no supervisado.
* El análisis de las características de cada cluster permitió explorar patrones entre las distancias, los tiempos y la presencia de transbordos.
* El uso de datos sintéticos facilita las pruebas y la reproducibilidad del ejercicio, aunque para obtener conclusiones sobre la movilidad real de Tunja sería necesario trabajar con datos observados.

## Autores
Natalia Espinosa y Eduard Rojas
