# Telecom X - Parte 2: Modelado Predictivo de Churn de Clientes

Este repositorio contiene la segunda fase del proyecto de análisis de datos para Telecom X, centrada en la construcción y evaluación de modelos de Machine Learning para predecir la evasión de clientes (Churn).

## 🎯 Propósito del Análisis

El objetivo principal de este proyecto es desarrollar un modelo predictivo robusto capaz de identificar a los clientes con alta probabilidad de cancelar su servicio. Al predecir el churn de manera proactiva, Telecom X puede implementar estrategias de retención dirigidas, reducir la pérdida de ingresos y mejorar la lealtad de sus clientes.

## 📁 Estructura del Proyecto

El repositorio está organizado de la siguiente manera para facilitar su comprensión y ejecución:
## ⚙️ Proceso de Preparación de Datos

Para asegurar el máximo rendimiento de los modelos, los datos (provenientes del archivo datos_para_modelo.csv) pasaron por un riguroso proceso de preprocesamiento:

1.  **Clasificación y Codificación de Variables:**
    *   Las variables categóricas (ej. Contract, InternetService) fueron transformadas a un formato numérico utilizando la técnica de **One-Hot Encoding** (pd.get_dummies). Esto es esencial, ya que los algoritmos de Machine Learning operan con datos numéricos.

2.  **Manejo del Desbalance de Clases:**
    *   Se detectó un desbalance moderado en la variable objetivo Churn (74% de clientes activos vs. 26% que cancelaron). Para corregirlo, se aplicó la técnica **SMOTE (Synthetic Minority Over-sampling Technique)**, que generó ejemplos sintéticos de la clase minoritaria, resultando en un conjunto de datos perfectamente balanceado (50/50).

3.  **Estandarización de Datos:**
    *   Todas las características numéricas fueron estandarizadas utilizando StandardScaler de Scikit-learn. Este paso asegura que todas las variables tengan una media de 0 y una desviación estándar de 1, evitando que modelos sensibles a la escala (como la Regresión Logística) se vean sesgados por la magnitud de los datos.

4.  **Separación en Entrenamiento y Prueba:**
    *   El conjunto de datos final fue dividido en un **80% para entrenamiento** y un **20% para prueba** (train_test_split). Esta separación es crucial para evaluar de manera objetiva el rendimiento de los modelos en datos que nunca han visto.

## 🤖 Justificación de la Modelización

Se entrenaron dos modelos con enfoques diferentes para tener una visión comparativa:

*   **Regresión Logística:** Se eligió como un modelo de base (baseline) por su simplicidad, rapidez y alta interpretabilidad a través de sus coeficientes. Requiere que los datos estén estandarizados para funcionar correctamente.
*   **Random Forest:** Se seleccionó como un modelo más complejo y potente, basado en árboles de decisión. No es sensible a la escala de los datos, pero se beneficia de un buen preprocesamiento. Es conocido por su alto rendimiento y su capacidad para medir la importancia de las variables.

El modelo **Random Forest** demostró un desempeño superior, con una **exactitud del 85%**, y sus resultados sobre la importancia de las variables fueron más consistentes con el análisis exploratorio.

## 📊 Ejemplo de Insight del Análisis (EDA)

Durante el análisis, se confirmó que la **antigüedad (tenure)** y el **tipo de contrato** son los factores más determinantes. El siguiente gráfico ilustra cómo los clientes con contratos mes a mes son significativamente más propensos a la cancelación.

## 🚀 Instrucciones para Ejecutar el Cuaderno

Para replicar este análisis, sigue los siguientes pasos en Google Colab:

1.  **Cargar los Datos:**
    *   Sube el archivo datos_para_modelo.csv a tu sesión de Google Colab o móntalo desde tu Google Drive.
    *   Asegúrate de ajustar la ruta del archivo en la celda de carga de datos del notebook: `pd.read_csv("tu/ruta/a/datos_para_modelo.csv")`.

2.  **Instalar Bibliotecas:**
    *   El notebook requiere la biblioteca imbalanced-learn para el balanceo de datos. La primera celda de código del notebook incluye el comando para instalarla. Asegúrate de ejecutarla:
        `!pip install imbalanced-learn`

3.  **Ejecutar el Notebook:**
    *   Una vez cargados los datos y la biblioteca instalada, puedes ejecutar todas las celdas en orden desde el menú Entorno de ejecución > Ejecutar todo. El cuaderno te guiará a través de cada paso del preprocesamiento, modelado y evaluación.
