# Predicción de Resultados de Citas Médicas y Mitigación de Sesgos 🏥⚖️

Este proyecto desarrolla un modelo de clasificación para predecir el estado final de las citas médicas (`ESTAFINAL`) utilizando un dataset de gestión de citas de 2013. El objetivo principal es no solo maximizar el desempeño predictivo, sino también garantizar la **equidad (Fairness)** y la **explicabilidad (XAI)** del modelo, auditando y mitigando posibles sesgos hacia grupos sensibles.

## 📋 Tabla de Contenidos
- [Descripción del Proyecto](#descripción-del-proyecto)
- [Dataset](#dataset)
- [Instalación y Requisitos](#instalación-y-requisitos)
- [Metodología](#metodología)
  - [1. Análisis Exploratorio (EDA)](#1-análisis-exploratorio-eda)
  - [2. Modelado](#2-modelado)
  - [3. Auditoría de Sesgos (Fairness)](#3-auditoría-de-sesgos-fairness)
  - [4. Explicabilidad (XAI)](#4-explicabilidad-xai)
- [Resultados Clave](#resultados-clave)
- [Integrantes](#integrantes)

---

## 📖 Descripción del Proyecto
El sistema predice si una cita médica resultará en una de tres categorías (`1`, `2`, o `3`). Dado que las decisiones automáticas en salud pueden afectar desproporcionadamente a ciertos grupos, este taller se enfoca en identificar disparidades en las métricas de desempeño según el **Género**, **Tipo de Afiliación** y **Rango de Edad**.

## 📊 Dataset
Los datos contienen información de **67,650 registros** en el set de entrenamiento y **16,864** en el de prueba.
* **Características Principales:**
    * `GENERO`: Masculino / Femenino.
    * `EDAD`: Edad numérica del paciente.
    * `ESPECIALIDAD`: Área médica (32 especialidades distintas).
    * `TIPO_AFILIACION`: Categorías (Gold, Silver, Convenio).
    * `FECHA_CITA`: Fecha programada de la cita.
* **Variable Objetivo (`ESTAFINAL`):** * Clase 2: 63.6% (Mayoritaria)
    * Clase 3: 18.7%
    * Clase 1: 17.7%

## 🛠️ Instalación y Requisitos
Asegúrate de tener Python 3.8+ instalado. Puedes instalar las dependencias necesarias con:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn shap lime tqdm

# 📊 Análisis de los Datos

El dataset (`citaschallenge.xlsx`) consta de **67,650 registros** y cuenta con las siguientes variables clave:

### Características (Features)
* **GENERO:** Masculino o Femenino.
* **EDAD:** Edad del paciente (con posterior agrupación por rangos).
* **ESPECIALIDAD:** 32 especialidades médicas (ej. Fisioterapia, Odontología).
* **TIPO_AFILIACION:** Categorías *Gold*, *Silver* y *Convenio*.
* **FECHA_CITA:** Marca de tiempo de la cita.

### Variable Objetivo
* **ESTAFINAL:** Clase dominante **2** (representa el **63.6%** de los datos).

---

## ⚙️ Metodología

1.  **Carga y Limpieza:** Tratamiento de tipos de datos y verificación de nulos/duplicados.
2.  **Análisis Exploratorio (EDA):** Identificación de la distribución de clases y perfiles de pacientes.
3.  **Auditoría de Sesgo:** Evaluación de métricas (**Accuracy**, **F1-Macro**) segmentadas por grupos sensibles.
4.  **Entrenamiento:** Implementación de un `RandomForestClassifier` con pesos de clase balanceados.
5.  **Mitigación:** Ajuste del modelo para reducir brechas de desempeño. 
    > **Resultado clave:** En la variable `GENERO`, la brecha de accuracy se redujo de un **7.05%** a solo un **1.02%**.

---

## 📈 Resultados y Fairness

El modelo base alcanzó un **Accuracy global** aproximado del **59.76%**. Tras el proceso de mitigación:

* Se logró un **equilibrio más justo** entre las clases minoritarias.
* Se redujeron significativamente las brechas de desempeño en las variables `TIPO_AFILIACION` y `GENERO`.

---

## 🔍 Interpretabilidad (XAI)

Para entender las decisiones del modelo de forma transparente, se integraron:

| Herramienta | Aplicación |
| :--- | :--- |
| **SHAP** | Identifica la importancia **global** de las variables en las predicciones. |
| **LIME** | Explica casos **individuales** de forma local. |





# 📊 Informe de Análisis Interpretativo y Ético del Modelo

## 🔍 Transparencia del Modelo
La transparencia técnica del modelo se identifica como **moderada**. Se ha logrado explicar, mediante herramientas de interpretabilidad como **LIME**, cómo se descomponen las decisiones locales en factores comprensibles. 

Factores como los **rangos de edad** o **tipos de afiliación específicos** son determinantes para predecir el estado final de las citas (cumplimiento o insistencia).

---

## ⚠️ Riesgos Éticos y Sociales de la Implementación
Se han identificado tres riesgos críticos que podrían surgir al poner el sistema en producción:

1. **Sesgo por Tipo de Afiliación:** El modelo puede aprender y perpetuar desigualdades socioeconómicas. Al ser una variable principal, el sistema corre el riesgo de priorizar o penalizar a ciertos grupos según el convenio o plan que poseen.
2. **Discriminación por Edad o Género:** Si el modelo asocia erróneamente el incumplimiento con un género o rango de edad específico, podría generar barreras de acceso a la salud para estos grupos vulnerables.
3. **Deshumanización del Servicio:** La automatización basada puramente en probabilidades de asistencia, sin considerar factores externos (emergencias, problemas de transporte), afecta la calidez y justicia en la prestación de servicios médicos.

---

## 🛠️ Consideraciones para Mejorar el Modelo

| Propuesta | Descripción |
| :--- | :--- |
| **Variables Externas** | Integrar datos de clima, tráfico o ubicación para entender las causas reales del incumplimiento. |
| **Balanceo de Datos** | Asegurar que las clases del estado final estén equilibradas para evitar el sesgo hacia la clase mayoritaria. |
| **Monitoreo Continuo** | Implementar auditorías periódicas para detectar si el modelo comienza a discriminar a grupos específicos con el tiempo. |

---

## 💡 Reflexión sobre el Proceso

### ¿Cómo toma decisiones el modelo?
Se determinó que el proceso de decisión **no es lineal**; el modelo analiza múltiples características de manera simultánea. 
> **Hallazgo Clave:** Mediante LIME se observó que, para predicciones en rangos de edad específicos (ej. menores de 29 años), el modelo busca patrones históricos en las combinaciones de variables para asignar un peso probabilístico al resultado final.

### ¿Hay variables con peso excesivo?
Basados en el análisis de importancia, las variables **ESPECIALIDAD** y **TIPO_ESPECIALIDAD** muestran una influencia significativa. 
* *Ejemplo:* El rango de afiliación puede marcar un peso negativo de **0.19**, siendo un factor determinante para la predicción en ciertos casos.

### Impacto de implementar el modelo sin Explicabilidad (XAI)
Omitir la interpretación del modelo generaría los siguientes conflictos:
* **Falta de Confianza:** El personal administrativo y médico no aceptaría decisiones que no comprenden.
* **Incapacidad de Corrección:** No se podrían identificar ni ajustar las variables que causan sesgos.
* **Vulnerabilidad del Paciente:** El usuario no tendría una justificación clara de por qué se le asignó o denegó una cita basada en una predicción automatizada.


