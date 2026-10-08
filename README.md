# 🚀 Lab de Prototipos — Índice General de Proyectos (Hackathon 1-Week Suite)

Repositorio central (Hub) que coordina los **3 prototipos construidos en paralelo** usando **Google Antigravity CLI (`agy`)**, **Gemini 4 Argon (Medium)** como agente de ingeniería y la API de **`gemini-3.8-flash` + `gemma-4`** dentro de los productos.

---

## 🌐 Proyectos Desplegados en Vivo (Producción) + Repositorios Privados

| # | Proyecto | 🌐 URL en Vivo (Producción) | 📦 Repositorio GitHub | 📋 Especificación | 🌿 Ramas Benchmark |
| :- | :--- | :--- | :--- | :--- | :--- |
| **1** | **🩺 Telemed Pre-Consult AI**<br>Voz rápida + 3 preguntas follow-up → Ficha SOAP/ISBAR médica + Pase del Paciente | **[telemed-preconsult-ai.vercel.app](https://telemed-preconsult-ai.vercel.app)** | [`ykro/telemed-preconsult-ai`](https://github.com/ykro/telemed-preconsult-ai) | [SPEC.md](https://github.com/ykro/telemed-preconsult-ai/blob/main/SPEC.md) | • [`benchmark/argon-v1`](https://github.com/ykro/telemed-preconsult-ai/tree/benchmark/argon-v1)<br>• [`benchmark/opus-5.5-v1`](https://github.com/ykro/telemed-preconsult-ai/tree/benchmark/opus-5.5-v1) |
| **2** | **🌊 Freelance Cashflow Smoother**<br>Presupuesto de ingresos variables: meses buenos/malos y cuánto apartar cada semana | **[freelance-cashflow-smoother.vercel.app](https://freelance-cashflow-smoother.vercel.app)** | [`ykro/freelance-cashflow-smoother`](https://github.com/ykro/freelance-cashflow-smoother) | [SPEC.md](https://github.com/ykro/freelance-cashflow-smoother/blob/main/SPEC.md) | • [`benchmark/argon-v1`](https://github.com/ykro/freelance-cashflow-smoother/tree/benchmark/argon-v1)<br>• [`benchmark/opus-5.5-v1`](https://github.com/ykro/freelance-cashflow-smoother/tree/benchmark/opus-5.5-v1) |
| **3** | **💳 Card Statement Insights**<br>Dashboard desde 1 estado de cuenta con motor de tendencias desbloqueable a los 3+ meses | **[card-statement-insights.vercel.app](https://card-statement-insights.vercel.app)** | [`ykro/card-statement-insights`](https://github.com/ykro/card-statement-insights) | [SPEC.md](https://github.com/ykro/card-statement-insights/blob/main/SPEC.md) | • [`benchmark/argon-v1`](https://github.com/ykro/card-statement-insights/tree/benchmark/argon-v1) |
| **🧪** | **📊 Gemini 4 Argon & `agy` CLI Benchmark**<br>Documentación de ingeniería, pruebas A/B y comparativa vs. Opus 5.5 | **[Ver Reporte Completo](https://github.com/ykro/gemini-argon-agy-benchmark/blob/main/RESULTS_ARGON_BENCHMARK.md)** | [`ykro/gemini-argon-agy-benchmark`](https://github.com/ykro/gemini-argon-agy-benchmark) | [METHODOLOGY.md](https://github.com/ykro/gemini-argon-agy-benchmark/blob/main/METHODOLOGY.md) | [Prompts Reproducibles](https://github.com/ykro/gemini-argon-agy-benchmark/tree/main/prompts) |

---

## 🏗️ Resumen Ejecutivo de Cada Entregable

### 1. 🩺 Telemed Pre-Consult AI (`telemed-preconsult-ai`)
- **URL en vivo:** https://telemed-preconsult-ai.vercel.app
- **Formato:** **PWA Mobile-First** en Light Mode clínico de nivel producción (`GTQ Q` por defecto / `USD $`).
- **Flujo:**
  1. El paciente habla rápido (30–90s) usando **Web Speech API** (`SpeechRecognition`) o carga uno de los 3 casos clínicos realistas.
  2. La IA detecta huecos del protocolo **OPQRST** y realiza **3 preguntas rápidas de follow-up** (con lectura por voz TTS + chips táctiles).
  3. **Doble Entregable:**
     - **Para el Médico:** Ficha **SOAP** e **ISBAR** con citas textuales (*Evidence Tracing*) y alertas de *Red Flags*.
     - **Para el Paciente:** "Pase de Pre-Consulta" descargable/imprimible con resumen claro, 3 preguntas sugeridas para hacerle al médico y checklist previo a la videollamada.
  4. **Prueba A/B en vivo:** Conmutador entre Variante A (`gemini-3.8-flash` directo) y Variante B (Cascada con anonimización PII local + `gemma-4` + `gemini-3.8-flash`).

### 2. 🌊 Finanzas 1: Freelance Cashflow Smoother (`freelance-cashflow-smoother`)
- **URL en vivo:** https://freelance-cashflow-smoother.vercel.app
- **Inputs (Ultra-simples en `GTQ Q` o `USD $`):**
  - *Configuración Base:* Piso de gastos fijos mensuales indispensables + ahorro actual + selector 1-click de perfiles en Guatemala/LATAM o entrada en lenguaje natural con `gemma-4` / `gemini-3.8-flash`.
  - *Input de cada Viernes:* "¿Cuánto dinero te entró esta semana?".
- **Outputs (Dashboard de consumo en 5 segundos):**
  - **Las 3 Cubetas Semanales:** 1) 🛡️ Cuánto apartar hoy para temporada baja, 2) 🏠 Cuánto va a tus fijos, 3) ✨ Tu Sueldo Libre Seguro (o cuánto retirar del colchón si fue semana mala).
  - **Semanas de Oxígeno (Runway)** + **Gráfica Montaña Rusa vs. Sueldo Estabilizado** + **Calendario de Clima Financiero (12 meses)** + **Simulador de Crisis**.

### 3. 💳 Finanzas 2: Card Statement Insights (`card-statement-insights`)
- **URL en vivo:** https://card-statement-insights.vercel.app
- **Diseño Progresivo (1 Mes → 3+ Meses en `GTQ Q` o `USD $`):**
  - **Con 1 estado de cuenta (`1/3`):** Entrega radiografía completa del mes (categorías, comercios top de Guatemala e internacionales, suscripciones, gastos hormiga, Visacuotas/MSI y ahorros inmediatos) + **Banner de progreso `1/3`** sugiriendo subir mínimo 3 estados de cuenta para detectar tendencias reales.
  - **Con 3+ estados de cuenta (`3/3`):** Desbloquea el **Motor de Tendencias Trimestrales** (*lifestyle creep*, aumentos silenciosos en suscripciones, evolución Mes 1 → Mes 2 → Mes 3) y el **Simulador Interactivo de Recorte**.
