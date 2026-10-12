# Prototipos Innovation Lab

Catálogo e índice de prototipos de inteligencia artificial aplicada desarrollados en el **Innovation Lab de Universidad Galileo** alrededor de tres retos de producto:
1. **Salud Digital (Pre-consulta médica asistida por IA)**
2. **Finanzas Personales (Estabilización y análisis de ingresos variables)**
3. **Finanzas Personales (Análisis de estados de cuenta y reducción de gastos)**

Los tres prototipos de referencia iniciales (incluyendo las versiones Web y Android de PreConsulta) fueron desarrollados por **Adrián** (`ykro`). Adicionalmente, **Cathy (Catherine Batres)**, **Emily (Emily Curin)** y **Luis (`cuprumbot`)** desarrollaron sus propias versiones e implementaciones independientes para cada uno de los tres retos.

---

## 1. Prototipos Desarrollados por Adrián (`ykro`)

| Proyecto | Dominio | Demo en Vivo | Repositorio | Descripción |
| :--- | :--- | :--- | :--- | :--- |
| **1. PreConsulta (Web)** | Salud Digital | [**telemed-preconsult-ai.vercel.app**](https://telemed-preconsult-ai.vercel.app) | [`ykro/telemed-preconsult-ai`](https://github.com/ykro/telemed-preconsult-ai) | Preparación previa a la teleconsulta: captura síntomas por voz o texto, realiza de 1 a 3 preguntas de seguimiento (*"Ayúdame con más información"*) y genera el Pase del Paciente junto con la ficha clínica (`SOAP` / `ISBAR`). |
| **1B. PreConsulta (Android)** | Salud Digital / Móvil | *APK Android* | [`ykro/telemed-preconsult-android`](https://github.com/ykro/telemed-preconsult-android) | Cliente nativo en Kotlin y Jetpack Compose con soporte de procesamiento local (**Gemma 4 E2B**) para operación offline y sincronización con la nube (**Gemini 3.8 Flash**). |
| **2. Estabilizador de Ingresos** | Finanzas Personales | [**freelance-cashflow-smoother.vercel.app**](https://freelance-cashflow-smoother.vercel.app) | [`ykro/freelance-cashflow-smoother`](https://github.com/ykro/freelance-cashflow-smoother) | Presupuesto para ingresos variables en `Q` y `$`: analiza meses o semanas buenas y malas y calcula cuánto apartar cada semana para mantener liquidez en temporada baja. |
| **3. Estados de Cuenta** | Finanzas Personales | [**card-statement-insights.vercel.app**](https://card-statement-insights.vercel.app) | [`ykro/card-statement-insights`](https://github.com/ykro/card-statement-insights) | Análisis visual de estados de cuenta bancarios en PDF: identifica tendencias multi-mes, separa compras regulares de cuotas/extrafinanciamientos y simula decisiones de ahorro. |

---

## 2. Versiones Desarrolladas por Cathy, Emily y Luis

| Proyecto | Autora / Autor | Dominio | Demo / Ejecución | Repositorio | Descripción |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1. PreConsulta** | **Cathy** (Catherine Batres) | Salud Digital | [**preconsulta-iota.vercel.app**](https://preconsulta-iota.vercel.app/) | [`CatherineBatres/preconsulta`](https://github.com/CatherineBatres/preconsulta) | Aplicación web móvil (Next.js) que convierte una nota de voz de hasta 2 minutos (`MediaRecorder`) o texto en una ficha médica estándar de 13 campos con `gemini-3.8-flash`. Realiza de 3 a 5 preguntas de seguimiento (una a la vez, con respuesta en audio de 45s o texto), detecta signos de alarma y genera en el navegador un PDF clínico editable (`jsPDF`) listo para compartir por WhatsApp o correo sin enviar el nombre ni contacto del paciente al servidor. |
| **2. Integral · Ingresos Variables** | **Emily** (Emily Curin) | Finanzas Personales | Local (`127.0.0.1:8765` · Python / FastAPI) | [`EmilyCurin/Integral-ingresos-variables`](https://github.com/EmilyCurin/Integral-ingresos-variables) | Aplicación web 100% local para importar documentos financieros (CSV, Excel, PDF con `PyMuPDF` e imágenes/capturas con OCR `Tesseract`), revisar propuestas de importación y construir un Libro de Ingresos clasificado (`recurrente`, `variable`, `extraordinario`, `gasto`, `excluido`). Calcula escenarios *conservador*, *esperado* (mediana) y *optimista* ($\pm 1\sigma$), cifra la bóveda en SQLite con `Fernet`/`scrypt` e integra **Ollama (`gemma3:4b`)** opcionalmente para interpretar notas personales. |
| **3. Expense Tracker (Control de Gastos)** | **Luis** (`cuprumbot`) | Finanzas Personales | Web (Next.js / TypeScript) | [`cuprumbot/expense-tracker`](https://github.com/cuprumbot/expense-tracker) | Aplicación de control y reducción de gastos mensuales a partir de un estado de cuenta en PDF o archivo CSV. Implementa una arquitectura *Split-Brain*: parsea localmente estados de cuenta de **Banco G&T Continental** (`pdf-parse`), clasifica comercios guatemaltecos con un catálogo local de reglas y detecta suscripciones recurrentes. Para bancos no soportados o gastos desconocidos (`> 5`), anonimiza PII localmente con confirmación del usuario antes de consultar a **Gemini Pro**. |

---

## 3. Comparación entre las Implementaciones de Adrián y las de Cathy, Emily y Luis

Aunque cada par de proyectos resuelve el mismo problema de fondo, las decisiones de producto, privacidad, arquitectura e integración de IA difieren de forma importante:

### 3.1. PreConsulta Médica: Adrián (`telemed-preconsult-ai` / `android`) vs. Cathy (`CatherineBatres/preconsulta`)

| Dimensión | Implementación de Adrián (`ykro`) | Implementación de Cathy (`CatherineBatres`) |
| :--- | :--- | :--- |
| **Plataformas y Despliegue** | Doble cliente: **Web** (Next.js en Vercel) + **App nativa Android** (Kotlin / Jetpack Compose). | Cliente **Web responsivo** (Next.js App Router en Vercel) pensado para abrirse desde un enlace en el teléfono sin instalar nada. |
| **Motor de IA e Inferencia** | **Híbrido Cloud + Edge:** `Gemini 3.8 Flash` en la nube y modelo local **Gemma 4 E2B** (~1.3 GB vía MediaPipe) corriendo 100% offline en GPU/NPU Android. | **Cloud Multimodal:** `gemini-3.8-flash` (`@google/genai` Interactions API con `store: false` y `thinking_level: "low"`) invocado desde una ruta serverless (`/api/ficha`). |
| **Captura de Voz y Audio** | Transcripción en vivo en el cliente mediante `Web Speech API` / `RecognizerIntent` (`es-GT`) y lectura en voz alta (`TextToSpeech`), más captura opcional de signos vitales en casa. | Grabación de audio binario (`MediaRecorder` en `audio/webm` o `audio/mp4`, hasta 120s en relato y 45s por respuesta) enviado como `multipart/form-data` para que Gemini escuche y transcriba el audio directamente. |
| **Interrogatorio de Seguimiento** | Evalúa brechas semiológicas (`OPQRST`) para formular de **1 a 3 preguntas** adaptativas focalizadas en síntomas faltantes. | Formula de **3 a 5 preguntas** una a la vez para completar un esquema fijo de **13 campos clínicos** (motivo, inicio, duración, intensidad, factores, síntomas asociados y 7 campos de antecedentes). |
| **Entregable y Privacidad** | **Doble entregable simultáneo:** *Pase del Paciente* (lenguaje claro con alerta clínica prioritaria) + *Ficha Médica* (`SOAP` / `ISBAR` / `OPQRST`). Sanitiza PII (DPI/teléfonos) por regex en memoria. | **Hoja clínica única editable en pantalla** (toque para corregir cualquier campo) que se convierte localmente en **PDF (`jsPDF`)** o texto formateado para WhatsApp (`navigator.share` / `wa.me`). El nombre y contacto nunca salen del navegador. |

### 3.2. Ingresos Variables: Adrián (`freelance-cashflow-smoother`) vs. Emily (`Integral-ingresos-variables`)

| Dimensión | Implementación de Adrián (`ykro`) | Implementación de Emily (`EmilyCurin`) |
| :--- | :--- | :--- |
| **Enfoque de Producto** | **Estabilizador de flujo de caja** en 3 pasos (`1. Ingresos`, `2. Gastos`, `3. Tu Plan`) centrado en calcular cuánto apartar en semanas/meses altos para cubrir temporadas bajas. | **Libro contable e importador documental** con 4 modalidades de análisis (mensual, trimestral, anual e historial completo) enriquecido con **notas personales cualitativas** sobre pagos atípicos. |
| **Entrada de Datos** | Ingreso directo de series históricas por mes o por semana (con conversión reversible `4.333`) en **dos monedas nativas (`GTQ Q` y `USD $`)**. | **Importación multiformato** de archivos CSV, Excel (`openpyxl`), PDF (`PyMuPDF`) y fotos/capturas de transferencias mediante **OCR local (`Tesseract`)**, con bandeja de revisión previa antes de confirmar cada movimiento. |
| **Modelo Matemático** | Algoritmo determinista (`calculateSmoothing` y `computeDynamicTargetPct`) que detecta regímenes estacionales ($\ge 1.15\times$ alta, $\le 0.85\times$ baja), calcula tasa de retención acotada (`5%`–`45%`), semanas de *runway* y simulador interactivo (`-50%` a `+50%`). | Estadística descriptiva sobre categorías de ingreso (`recurrente`, `variable`, `extraordinario`): calcula promedio observado, escenario **esperado** (mediana mensual excluyendo extraordinarios), **conservador** y **optimista** ($\pm 1$ desviación estándar) y sugiere ahorrar el 50% del excedente sobre el presupuesto. |
| **Arquitectura y Uso de IA** | SPA en **React + Vite + Recharts** ejecutada en el navegador y desplegada en Vercel. | Servidor local en **Python + FastAPI + SQLite** (`127.0.0.1:8765`, ejecutable con doble clic en `.bat`/`.sh`). Cifra campos sensibles y documentos con **Fernet + `scrypt`** y conecta opcionalmente con **Ollama (`gemma3:4b`)** en local para interpretar notas sin usar APIs en la nube. |

### 3.3. Estados de Cuenta y Gastos: Adrián (`card-statement-insights`) vs. Luis (`cuprumbot/expense-tracker`)

| Dimensión | Implementación de Adrián (`ykro`) | Implementación de Luis (`cuprumbot`) |
| :--- | :--- | :--- |
| **Ingesta y Extracción de Archivos** | **Carga múltiple simultánea de PDFs.** Utiliza un parser propio de bajo nivel sobre streams PDF (`zlib.inflateSync` y coordenadas `BT...ET`) que extrae ~100 transacciones en `~6 ms` sin usar LLMs para leer el PDF. | **Carga individual de PDF o CSV** (con modal de mapeo de columnas si el CSV es ambiguo). Usa `pdf-parse` para extraer texto: si detecta **Banco G&T Continental**, aplica un parser tabular local; si es otro banco, pasa al flujo de anonimización + extracción con **Gemini Pro**. |
| **Privacidad y Arquitectura Split-Brain** | Procesamiento de extracción 100% determinista sin exponer el documento ni datos personales a servicios externos. | **Anonimizador local de PII con confirmación visual:** redacta nombres, direcciones, IBAN, cuentas, DPI y correos (`[NOMBRE_REDACTADO]`, `[CUENTA_REDACTADA]`), muestra una vista previa editable al usuario y valida con guardias regex antes de enviar el texto a Gemini Pro. |
| **Monedas y Estructura de Deuda** | **Bimonetario (`GTQ Q` y `USD $`)** con máquina de estados léxica que separa **3 libros**: consumos regulares en `Q`, consumos en `$` y **cuotas/extrafinanciamientos (`FIN/CT`, `FIN/IN`)**. | **Monomonetario en Quetzales (`GTQ Q`)** enfocado en débitos y gastos corrientes del mes, filtrando pagos de tarjeta, notas de crédito, saldos y líneas informativas. |
| **Clasificación, Persistencia y Ahorro** | Enfoque en **inteligencia multi-mes**: matriz de velocidad de gasto (`spendVelocity`), variación mes a mes (`MoM`), proyección a 90 días y simulador interactivo de decisiones (`Actual` vs. `Meta`). | Enfoque en **clasificación híbrida y control por categoría**: clasifica comercios locales con `merchant-catalog.json`, invoca a Gemini Pro solo si quedan `> 5` gastos pendientes, detecta **suscripciones recurrentes** y permite crear categorías personalizadas y editar transacciones con persistencia en `localStorage`. |

---

## Documentación y Artículos (Implementaciones de Adrián)

- **Arquitectura General y Flujos:** [`docs/ARCHITECTURE.md`](./docs/ARCHITECTURE.md)
- **Temas para Artículos Técnicos y de Producto:** [`docs/ARTICLES.md`](./docs/ARTICLES.md)

