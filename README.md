# 🚀 Lab de Prototipos — Índice General de Proyectos (Hackathon 1-Week Suite)

Repositorio central (Hub) que coordina los **3 prototipos construidos en paralelo** usando **Google Antigravity CLI (`agy`)**, **Gemini 4 Argon (Medium)** como agente de ingeniería y la API de **`gemini-3.8-flash` + `gemma-4-e2b`** dentro de los productos.

---

## 🗂️ Ecosistema de Repositorios Privados

| # | Proyecto | Repositorio GitHub | Especificación Técnica | Modelos en el Producto | Plataforma / Deploy |
| :- | :--- | :--- | :--- | :--- | :--- |
| **1** | **🩺 Telemed Pre-Consult AI**<br>Voz rápida + 3 preguntas follow-up → Ficha SOAP/ISBAR médica + Pase del Paciente | [`ykro/telemed-preconsult-ai`](https://github.com/ykro/telemed-preconsult-ai) | [Ver SPEC.md](https://github.com/ykro/telemed-preconsult-ai/blob/main/SPEC.md) | `gemini-3.8-flash` + `gemma-4-e2b` + Web Speech API | PWA Mobile-First en **Vercel** / Cloud Run |
| **2** | **🌊 Freelance Cashflow Smoother**<br>Presupuesto de ingresos variables: meses buenos/malos y cuánto apartar cada semana | [`ykro/freelance-cashflow-smoother`](https://github.com/ykro/freelance-cashflow-smoother) | [Ver SPEC.md](https://github.com/ykro/freelance-cashflow-smoother/blob/main/SPEC.md) | Algoritmo *Waterfall Buffer* + `gemini-3.8-flash` + `gemma-4-e2b` | Dashboard Web en **Vercel** / Cloud Run |
| **3** | **💳 Card Statement Insights**<br>Dashboard desde 1 estado de cuenta con motor de tendencias desbloqueable a los 3+ meses | [`ykro/card-statement-insights`](https://github.com/ykro/card-statement-insights) | [Ver SPEC.md](https://github.com/ykro/card-statement-insights/blob/main/SPEC.md) | `gemini-3.8-flash` (Multimodal PDF/CSV) + `gemma-4-e2b` (Redacción PII) | Dashboard Web en **Vercel** / Cloud Run |
| **🧪** | **📊 Gemini 4 Argon & `agy` CLI Benchmark**<br>Documentación de ingeniería, pruebas A/B y comparativa vs. Opus 5.5 | [`ykro/gemini-argon-agy-benchmark`](https://github.com/ykro/gemini-argon-agy-benchmark) | [Ver Metodología](https://github.com/ykro/gemini-argon-agy-benchmark/blob/main/METHODOLOGY.md) | **Gemini 4 Argon** vs. **Opus 5.5** en `agy` CLI | Reportes + Evidencia Directa en Git |

---

## 🏗️ Resumen Ejecutivo de Cada Entregable

### 1. 🩺 Telemed Pre-Consult AI (`telemed-preconsult-ai`)
- **Formato:** **PWA Mobile-First** (cero fricción de instalación para el paciente, funciona desde un link de WhatsApp y en escritorio para el doctor).
- **Flujo:**
  1. El paciente habla rápido (30–90s) usando **Web Speech API** (`SpeechRecognition`).
  2. La IA detecta huecos del protocolo **OPQRST** y realiza **3 preguntas rápidas de follow-up** (con voz + chips táctiles).
  3. **Doble Entregable:**
     - **Para el Médico:** Ficha **SOAP** e **ISBAR** con citas textuales (*Evidence Tracing*) y alertas de *Red Flags*.
     - **Para el Paciente:** "Pase de Pre-Consulta" descargable con resumen claro, 3 preguntas sugeridas para hacerle al médico y checklist previo a la videollamada.

### 2. 🌊 Finanzas 1: Freelance Cashflow Smoother (`freelance-cashflow-smoother`)
- **Inputs (Ultra-simples):**
  - *Configuración Base:* Piso de gastos fijos mensuales indispensables + ahorro actual + historial de 6-12 meses (o selector 1-click demo / dictado en lenguaje natural con `gemma-4-e2b`).
  - *Input de cada Viernes:* "¿Cuánto ingresó esta semana?".
- **Outputs (Dashboard de consumo en 5 segundos):**
  - **Las 3 Cubetas Semanales:** 1) 🛡️ Cuánto apartar hoy para temporada baja, 2) 🏠 Cuánto va a tus fijos, 3) ✨ Tu Sueldo Libre Seguro (o cuánto retirar del colchón si fue semana mala).
  - **Semanas de Oxígeno (Runway)** + **Gráfica Montaña Rusa vs. Sueldo Estabilizado** + **Calendario de Clima Financiero (12 meses)**.

### 3. 💳 Finanzas 2: Card Statement Insights (`card-statement-insights`)
- **Diseño Progresivo (1 Mes → 3+ Meses):**
  - **Con 1 estado de cuenta:** Entrega radiografía completa del mes (categorías, comercios top, suscripciones, gastos hormiga, MSI y ahorros inmediatos) + **Banner de progreso `1/3`** sugiriendo subir mínimo 3 estados de cuenta para detectar tendencias reales.
  - **Con 3+ estados de cuenta:** Desbloquea el **Motor de Tendencias Trimestrales** (*lifestyle creep*, aumentos silenciosos en suscripciones, evolución Mes 1 → Mes 2 → Mes 3) y el **Simulador Interactivo de Recorte**.

---

## 🌐 Estrategia de Despliegue (Vercel + Google Cloud Run)
Contamos con acceso verificado en este entorno a ambas plataformas:
- **Vercel CLI** (`aacs85-9369` / `adrian-catalans-projects`): Ideal para desplegar los frontends Next.js/PWA con URLs de preview instantáneas por cada commit y pruebas A/B.
- **Google Cloud Run** (proyecto activo `pm-innovationlab` con cuenta `aacs85@gmail.com`): Ideal si deseamos alojar contenedores unificados o microservicios de inferencia con `gemma-4-e2b` / procesamiento de PDFs pesados.
