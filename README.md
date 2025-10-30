# ARES: AI Race Engineer 🏁 (Proyecto Showcase)

[![Estado: Privado](https://img.shields.io/badge/Estado-Privado_(S%C3%B3lo_Showcase)-red?style=for-the-badge)](https://#)

> **Atención:** Este es un repositorio "escaparate". El código fuente es **privado** debido a planes de futura comercialización. El propósito de este `README` es describir la arquitectura, funcionalidad y tecnologías del proyecto.

**ARES** es una aplicación de escritorio que actúa como un ingeniero de pista virtual para ***Assetto Corsa Competizione (ACC)***.

Analiza datos de telemetría (`.ld`), ficheros de *setup* (`.json`) y el *feedback* subjetivo del piloto para diagnosticar problemas y sugerir cambios de ajuste precisos, utilizando la API de Google Gemini.

---

## 🎥 Demostración de la Aplicación


<img width="1920" height="1080" alt="Captura de pantalla (1)" src="https://github.com/user-attachments/assets/1a94fc41-259a-4e77-b3af-7f2d512c01e6" />
<p align="center">Captura de la interfaz de Angular principal con texto de prueba</p>


<img width="1920" height="1080" alt="Captura de pantalla (2)" src="https://github.com/user-attachments/assets/166fcaa4-310f-4d25-9365-b88b7eb2c986" />
<p align="center">Captura de la respuesta de la herramienta a la consulta anterior.</p>

---

## 🚀 Características Clave (Features)

* **Análisis de Telemetría Complejo:** Procesa ficheros `.ld` de MoTeC para extraer *insights* clave sobre temperaturas de neumáticos (camber), actividad del ABS (reparto de frenada) y recorrido de suspensión (topes).
* **Ingeniería de Prompts Avanzada:** Construye un contexto detallado para el LLM (Gemini), incluyendo el *setup* actual, el *feedback* del piloto y los *insights* de la telemetría para obtener respuestas de alta calidad.
* **Memoria de Sesión Iterativa:** ARES recuerda los cambios previos y el *feedback* del piloto dentro de una misma sesión, permitiendo un bucle de afinamiento continuo, igual que un ingeniero real.
* **Interfaz de Escritorio Unificada:** El backend (FastAPI) y el frontend (Angular) están empaquetados en una única aplicación de escritorio nativa usando PyWebView, creando una experiencia de usuario fluida sin necesidad de un navegador web.

---

## 🛠️ Stack Tecnológico y Arquitectura

### Stack Principal
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)&nbsp;
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)&nbsp;
![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)&nbsp;
![Google Gemini](https://img.shields.io/badge/Gemini_API-4285F4?style=for-the-badge&logo=google&logoColor=white)&nbsp;
![SCSS](https://img.shields.io/badge/SCSS-CC6699?style=for-the-badge&logo=sass&logoColor=white)&nbsp;

### Packaging y Librerías Clave
![PyWebView](https://img.shields.io/badge/PyWebView-007ACC?style=for-the-badge&logo=python&logoColor=white)&nbsp;
![PyInstaller](https://img.shields.io/badge/PyInstaller-8A2BE2?style=for-the-badge&logo=python&logoColor=white)&nbsp;
`ldparser` (Lectura de telemetría)

---

### 🏛️ Arquitectura de la Aplicación

ARES funciona como una aplicación de escritorio local que "envuelve" un stack web moderno.

1.  **`PyWebView`** (Contenedor nativo) inicia un servidor **`Uvicorn/FastAPI`** en segundo plano al ejecutar el `.exe`.
2.  `PyWebView` carga el *build* de producción de **`Angular`** como la interfaz de usuario.
3.  El **Frontend (Angular)** hace peticiones HTTP locales (a `localhost`) al **Backend (FastAPI)**.
4.  El **Backend** procesa la lógica: lee los ficheros locales (`.ld`, `.json`) y se comunica con la **API de Google Gemini** para el análisis de IA.

     F --> C;
     C --> D;
     D --> A;
