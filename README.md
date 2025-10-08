# Asistente RAG para RRHH

![IA aplicada a RRHH](images/ia_rrhh.png)


## Introducción
En un entorno empresarial donde la información crece exponencialmente, los departamentos de **RRHH** necesitan herramientas inteligentes capaces de **transformar datos dispersos** en **conocimiento accionable**. Este proyecto demuestra cómo la **inteligencia artificial** puede convertirse en un **copiloto corporativo**, optimizando la gestión documental y mejorando la toma de decisiones.

Este trabajo forma parte del **Trabajo Final de Máster en Data Science con IA de BIG school**.

## Objetivo del proyecto
Construir un **sistema RAG (Retrieval-Augmented Generation)** capaz de:
- **Consultar**
- **Analizar**
- **Generar respuestas**
A partir de documentos reales del área de **Recursos Humanos (RRHH)** dentro de una empresa simulada llamada **BCN Tech Solutions**.

## Acceso al Notebook completo

Puedes explorar y ejecutar el proyecto íntegro desde Google Colab:  
**[Abrir notebook en Colab](https://colab.research.google.com/drive/1_po4KRbvx0rT8_L3A2SeTea4jsJuVOvI?usp=sharing)**

## Descripción general

El asistente permite **formular preguntas en lenguaje natural** y obtener respuestas precisas basadas en documentación interna de RRHH, como políticas corporativas, descripciones de puesto, evaluaciones de desempeño y currículums de empleados.  
El sistema combina **búsqueda semántica (FAISS)** y **modelos de lenguaje (LLMs)** para ofrecer resultados relevantes y contextualizados.

![BCN Tech Solutions](images/bcntech.png)

## Impacto en RRHH
El asistente reduce el tiempo de búsqueda documental, centraliza el conocimiento corporativo y minimiza el riesgo de errores humanos en procesos de selección, evaluación o comunicación interna. Su aplicación práctica permite que los equipos de **RRHH dediquen más tiempo a la estrategia y menos a la gestión manual de información**.

## Pipeline del sistema

El flujo completo del asistente se basa en la arquitectura **RAG (Retrieval-Augmented Generation)**, con las siguientes etapas:

![Pipeline del sistema](images/pipeline.png)

### 1. Ingesta documental
- Lectura de archivos en formato **PDF**, **DOCX** y **Markdown**.
- Limpieza y normalización de texto mediante `BeautifulSoup`, `markdown` y `PyMuPDF`.

### 2. Chunking y vectorización
- División adaptativa de documentos en fragmentos equilibrados (`chars` y `doctype`).
- Generación de **embeddings** con modelos locales y OpenAI (`MiniLM`, `MPNet`, `OAI-1536`, `OAI-3072`).
- Almacenamiento vectorial con **FAISS** para búsquedas eficientes.

### 3. Recuperación y generación
- Búsqueda semántica (`top-k`) para seleccionar los fragmentos más relevantes.
- Generación de respuestas con un **LLM (GPT-4o-mini)**, guiado por el contexto recuperado.
- Evaluación mediante métricas **Hit@K**, **MRR** y **nDCG@K**.

### 4. Visualización y evaluación
- Representación 2D de los embeddings con **PCA** para analizar la separación semántica de los documentos.

![Visualización PCA](images/pca.png)


## Modelos y herramientas utilizadas

| Tipo | Herramienta / Modelo | Descripción |
|------|-----------------------|--------------|
| **Embeddings** | `all-MiniLM-L6-v2`, `all-mpnet-base-v2`, `text-embedding-3-small`, `text-embedding-3-large` | Modelos de Sentence Transformers y OpenAI |
| **Vector DB** | `FAISS` | Búsqueda semántica rápida en espacios vectoriales |
| **LLM** | `GPT-4o-mini` | Generación de respuestas contextualizadas |
| **Procesamiento** | `PyMuPDF`, `python-docx`, `BeautifulSoup`, `markdown` | Limpieza y extracción de texto |
| **Visualización** | `matplotlib`, `seaborn`, `wordcloud`, `PCA` | Análisis visual y explicativo |
| **Evaluación** | `sklearn.metrics` (nDCG, cosine_similarity) | Evaluación cuantitativa de la recuperación |


## Resultados destacados
- El espacio de **chunking** `chars` mostró mejor rendimiento que `doctype` en términos de ordenación semántica.
- Los **embeddings de OpenAI (`text-embedding-3-large`)** ofrecieron los mejores resultados:
  - `Hit@K = 1.0`  
  - `nDCG@K ≈ 0.76`  
  - `MRR ≈ 0.65`
- **FAISS**, como **Vector DB**, es una base ligera, eficiente y 100 % ejecutable en local para indexar grandes volúmenes.
- **GPT-4o-mini** Ofrece la mejor relación coste-rendimiento para generación contextual. Las respuestas generadas con el **LLM** fueron **coherentes, contextuales y verificables** respecto a los documentos fuente.


## Valor y conclusiones

El sistema demuestra cómo un pipeline RAG puede **optimizar la gestión documental en RRHH**, reduciendo tiempo de búsqueda y mejorando la precisión en la toma de decisiones.  
Además, integra una **evaluación cuantitativa y cualitativa** que permite medir objetivamente la calidad del modelo y su impacto operativo.
En futuras versiones, este asistente podría integrarse con sistemas de gestión como **SAP SuccessFactors** o **BambooHR**, añadiendo capacidades de resumen automático de desempeño, clasificación de candidatos o generación de informes ejecutivos.
El proyecto demuestra que la combinación de **RAG + LLM** no solo mejora la eficiencia, sino que **redefine la forma en que los equipos humanos interactúan con la información corporativa**.



