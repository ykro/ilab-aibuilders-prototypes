# Arquitectura General de los Prototipos

Detalle de la arquitectura transversal y del flujo de captura y análisis de los prototipos desarrollados en el **Innovation Lab de Universidad Galileo**.

---

## 1. Mapa del Ecosistema

![Mapa de Prototipos de IA Aplicada](./diagrams/ecosystem-map.svg)

### Flujo de Captura y Tablero de Decisión

![Separación de Captura y Tablero de Decisión](./diagrams/dual-engine-flow.svg)

---

## 2. Resumen Funcional por Proyecto

### 1. PreConsulta (`telemed-preconsult-ai` y `telemed-preconsult-android`)
Organiza la información del paciente antes de ingresar a la consulta médica y destaca alertas de prioridad clínica desde el inicio del resumen:
1. **Motivo de consulta:** Dictado por voz o escritura libre con registro opcional de signos vitales en casa.
2. **Ayúdame con más información:** Entre 1 y 3 preguntas puntuales generadas dinámicamente según los datos faltantes (con stepper de 1 pregunta a la vez en Android).
3. **Resumen de consulta:** Alerta clínica prioritaria en la parte superior, guía de preparación para el paciente y ficha médica `SOAP` / `ISBAR` / `OPQRST`.

### 2. Estabilizador de Ingresos (`freelance-cashflow-smoother`)
Diseñado para profesionales independientes y trabajadores con ingresos variables en un flujo de 3 pantallas:
1. **1. Ingresos:** Registro histórico por mes o por semana en Quetzales (`Q`) y Dólares (`$`).
2. **2. Gastos:** Configuración de gastos esenciales fijos y reserva disponible.
3. **3. Tu Plan:** Cálculo de cuánto apartar cada semana, sueldo seguro disponible y gráfica interactiva de ingreso real frente a sueldo estabilizado con simulador de temporada baja (`-50%`) y alta (`+50%`).

### 3. Estados de Cuenta (`card-statement-insights`)
Convierte estados de cuenta bancarios en PDF en un tablero gráfico para identificar tendencias y tomar decisiones financieras:
1. **Carga de archivos PDF:** Soporte para arrastrar uno o varios estados de cuenta PDF simultáneamente.
2. **Resumen y gráficas:** Visualización del gasto por categoría (`Q` y `$`), comercios recurrentes y proporción de cuotas/extrafinanciamiento frente a compras del mes.
3. **Tendencias multi-mes:** Detección de aceleración de gasto, cargos recurrentes y proyección a 90 días al acumular múltiples períodos.
4. **Decisiones:** Acciones concretas con impacto mensual estimado sobre el próximo estado de cuenta (`Actual` vs. `Meta`).
