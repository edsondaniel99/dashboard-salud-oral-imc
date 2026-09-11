# 🩺 Dashboard Ejecutivo: Triaje de Salud Oral y Estado Nutricional en Odontopediatría

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas)](https://pandas.pydata.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-Data%20Viz-3776AB?style=for-the-badge)](https://seaborn.pydata.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-Interactive%20App-FF4B4B?style=for-the-badge&logo=streamlit)](https://streamlit.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

> **Solución Analítica de Negocio:** Herramienta de soporte para la toma de decisiones clínicas y optimización de recursos operativos en unidades de odontopediatría, basada en la intersección epidemiológica entre la severidad de caries (ICDAS) y el índice de masa corporal (IMC).

---

## 📌 1. Entendimiento del Problema de Negocio

Las clínicas de odontopediatría enfrentan cuellos de botella operativos debido a la falta de triaje automatizado y a la desconexión entre el diagnóstico dental y la salud sistémica del paciente. 

### Desafíos Operativos Identificados:
* **Saturación en Sillón:** Alta demanda de tratamientos invasivos de urgencia que bloquean la capacidad instalada para procedimientos preventivos.
* **Falta de Abordaje Interdisciplinario:** La malnutrición (tanto por exceso como por déficit) interactúa con la prevalencia de lesiones cariosas, pero raramente se gestiona mediante protocolos integrados.
* **Mermas en la Calidad de Datos:** Captura incompleta de variables antropométricas en la recepción de pacientes.

**Objetivo del Proyecto:** Convertir registros clínicos crudos en un **Dashboard Ejecutivo** modular que guíe la reasignación de horas de atención, establezca prioridades de triaje (P1, P2, P3) y optimice la captación de datos.

---

## 🛠️ 2. Enfoque Metodológico

El proyecto sigue una arquitectura analítica en 4 etapas:
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│  1. Ingesta y    │───>│  2. Ingeniería   │───>│  3. EDA y        │───>│  4. Despliegue   │
│  Limpieza (EDA)  │    │  de Funciones    │    │  Visualización   │    │  Interactivo     │
└──────────────────┘    └──────────────────┘    └──────────────────┘    └──────────────────┘
1. **Ingesta y Limpieza de Datos:** Eliminación de inconsistencias, estandarización de tipos de datos y tratamiento explícito de faltantes (`Sin dato`).
2. **Ingeniería de Características / Reglas de Negocio:**
   * **Categorización ICDAS:** Agrupación de estadios de caries (0: Sano, 1-2: Inicial, 3-4: Moderado, 5-6: Severo).
   * **Mapeo Antropométrico:** Clasificación según tablas OMS de IMC pediátrico.
   * **Matriz de Priorización Operativa:**
     * **P1 (Urgencia Operatoria):** ICDAS 5-6 (Caries Severa Extensa).
     * **P2 (Tratamiento Combinado):** ICDAS 3-4 (Moderado) o ICDAS 1-2 con comorbilidad nutricional.
     * **P3 (Prevención/Seguimiento):** ICDAS 0-2 en pacientes normopeso.
3. **Visualización y Visual Storytelling:** Creación de un layout 2x2 en Matplotlib/Seaborn optimizado para consumo directivo (sin ruido visual, con anotaciones directas).
4. **Modularización e Interfaz:** Despliegue en código ejecutable con **Streamlit**.

---

## 📊 3. Hallazgos Clave e Impacto Operativo ($N=436$)

| Métrica Clave | Valor Observado | Impacto en Operaciones / Negocio |
| :--- | :---: | :--- |
| **Demanda P1 (Urgencia Operatoria)** | **68.6%** | Requiere destinar el ~70% de la agenda quirúrgica a procedimientos complejos (pulpotomías, coronas). |
| **Caries Severa Extensa (ICDAS 6)** | **47.2%** | Alerta epidemiológica: casi la mitad de los pacientes llega en estadio terminal de destrucción dental. |
| **Malnutrición Acumulada** | **47.0%** | 35.1% sobrepeso/obesidad + 11.9% bajo peso severo. Justifica un programa interdisciplinario con nutrición. |
| **Calidad de Datos (IMC Faltante)** | **11.5%** | Área de mejora en el proceso de recepción para asegurar la captura de peso/talla. |

---

## 📁 4. Arquitectura del Repositorio

```text
dashboard-salud-oral-imc/
├── README.md                   <- Documentación del proyecto
├── requirements.txt            <- Dependencias del proyecto
├── .gitignore                  <- Archivos ignorados por Git
│
├── data/
│   ├── raw/                    <- Dataset original
│   └── processed/              <- Dataset limpio (df_final.csv)
│
├── notebooks/
│   └── 01_eda_y_dashboard.ipynb<- Notebook de exploración en Google Colab
│
├── src/                        <- Módulos Python reusables
│   ├── __init__.py
│   ├── data_processing.py      <- Funciones de limpieza y cálculo de variables
│   └── visualization.py        <- Generador del dashboard (Matplotlib/Seaborn)
│
└── app.py                      <- Aplicación interactiva de Streamlit
