# Prototipos Innovation Lab

Catálogo de prototipos de aplicaciones desarrollados en el **Innovation Lab de Universidad Galileo**.

---

## Aplicaciones

| Proyecto | Dominio | Demo en Vivo | Repositorio | Descripción |
| :--- | :--- | :--- | :--- | :--- |
| **1. PreConsulta (Web)** | Salud Digital | [**telemed-preconsult-ai.vercel.app**](https://telemed-preconsult-ai.vercel.app) | [`ykro/telemed-preconsult-ai`](https://github.com/ykro/telemed-preconsult-ai) | Preparación previa a la teleconsulta: captura síntomas por voz o texto, realiza de 1 a 3 preguntas de seguimiento (*"Ayúdame con más información"*) y genera una guía para el paciente junto con la nota clínica estructurada (`SOAP` / `ISBAR`) para el médico. |
| **1B. PreConsulta (Android)** | Salud Digital / Móvil | *APK Android* | [`ykro/telemed-preconsult-android`](https://github.com/ykro/telemed-preconsult-android) | Cliente nativo en Kotlin y Jetpack Compose con soporte de procesamiento local (**Gemma 4 E2B**) para escenarios de conectividad limitada y sincronización con la nube (**Gemini 3.8 Flash**). |
| **2. Estabilizador de Ingresos** | Finanzas Personales | [**freelance-cashflow-smoother.vercel.app**](https://freelance-cashflow-smoother.vercel.app) | [`ykro/freelance-cashflow-smoother`](https://github.com/ykro/freelance-cashflow-smoother) | Presupuesto para trabajadores independientes o de ingresos variables: analiza los meses o semanas buenas y malas y calcula cuánto apartar cada semana para mantener liquidez en temporada baja. |
| **3. Estados de Cuenta** | Finanzas Personales | [**card-statement-insights.vercel.app**](https://card-statement-insights.vercel.app) | [`ykro/card-statement-insights`](https://github.com/ykro/card-statement-insights) | Análisis visual de estados de cuenta bancarios en PDF: identifica tendencias de consumo a lo largo de varios meses, separa compras regulares de cuotas/extrafinanciamientos y presenta recomendaciones concretas para tomar decisiones. |

---

## Arquitectura General

![Mapa de Prototipos de IA Aplicada](docs/diagrams/ecosystem-map.svg)

### Flujo de Captura y Análisis

![Separación de Captura y Tablero de Decisión](docs/diagrams/dual-engine-flow.svg)

---

## Resumen de los Proyectos

### 1. PreConsulta (`telemed-preconsult-ai` y `telemed-preconsult-android`)
Organiza la información del paciente antes de ingresar a la consulta médica y destaca alertas de prioridad clínica desde el inicio del resumen:
1. **Motivo de consulta:** Dictado por voz o escritura libre con registro opcional de signos vitales en casa.
2. **Ayúdame con más información:** Entre 1 y 3 preguntas puntuales generadas dinámicamente según los datos faltantes.
3. **Resumen de consulta:** Alerta clínica prioritaria en la parte superior, guía de preparación para el paciente y ficha médica `SOAP` / `ISBAR`.

### 2. Estabilizador de Ingresos (`freelance-cashflow-smoother`)
Diseñado para profesionales independientes y trabajadores con ingresos variables:
1. **Historial de ingresos:** Registro por mes o por semana.
2. **Gastos esenciales y reserva actual:** Configuración de necesidades fijas y fondo disponible.
3. **Plan semanal:** Cálculo de cuánto apartar cada semana y cuánto gastar de forma segura.
4. **Proyección y simulador:** Gráfica comparativa de ingreso real frente a ingreso estabilizado con simulación de temporada baja (`-50%`) y temporada alta (`+50%`).

### 3. Estados de Cuenta (`card-statement-insights`)
Convierte estados de cuenta bancarios en PDF en un tablero gráfico para identificar tendencias y tomar decisiones financieras:
1. **Carga de archivos PDF:** Soporte para arrastrar uno o varios estados de cuenta PDF simultáneamente.
2. **Gráficas y composición:** Visualización del gasto por categoría, comercios recurrentes y proporción de cuotas frente a compras del mes.
3. **Tendencias multi-mes:** Detección de aceleración de gasto, cargos recurrentes y proyección a 90 días al cargar múltiples períodos.
4. **Decisiones:** Acciones concretas con impacto mensual estimado sobre el próximo estado de cuenta.
