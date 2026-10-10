# Temas para Artículos Técnicos y de Producto

Compendio de temas de producto, diseño e ingeniería identificados a partir del desarrollo de los prototipos del **Innovation Lab de Universidad Galileo**.

---

## 1. Arquitectura Transversal del Ecosistema

1. **Arquitectura de Prompts con Contratos JSON Tipados y Degradación Determinista:** Separación entre extracción semántica probabilística y motores de reglas deterministas con esquemas estrictos y respaldo local sin caída de servicio.
2. **Ingeniería de Privacidad Local-First en Web y Móvil (`IndexedDB`, `FileReader` y `MediaPipe`):** Procesamiento de documentos financieros y relatos clínicos en el borde sin almacenar PII en servidores intermedios.
3. **Orquestación de Subagentes Especializados para Auditoría y Refactorización de UI/UX:** Uso de agentes de diseño e inspección visual sobre capturas reales de emulador (`adb screencap` + `uiautomator`) para iterar interfaces nativas y web.

---

## 2. PreConsulta (`telemed-preconsult-ai` y `telemed-preconsult-android`)

### Producto y Dominio Clínico
1. **Interrogatorio clínico adaptativo (1 a 3 preguntas) mediante evaluación de brechas semiológicas OPQRST:** Reemplazo de formularios médicos estáticos por un flujo conversacional que identifica únicamente las variables clínicas faltantes (*Aparición, Provocación, Calidad, Irradiación, Severidad y Tiempo*).
2. **Generación simultánea de doble entregable clínico:** Transformación de una misma captura en dos documentos sincronizados: el **Pase del Paciente** en lenguaje claro con alerta de prioridad visible y la **Ficha Médica (`SOAP` / `ISBAR`)** para el médico.
3. **IA en el dispositivo (`Gemma 4 E2B` en Android nativo) frente a inferencia en la nube (`Gemini 3.8 Flash` en Web):** Criterios de arquitectura sobre descarga persistente (~1.3 GB), aceleración en GPU/NPU móvil y operación offline en brigadas rurales frente al acceso inmediato sin instalación en navegador web.

### Ingeniería de Software
4. **Validación determinista de esquemas JSON clínicos y sanitización regex de PII en memoria:** Contratos estrictos de salida para notas `SOAP`, `ISBAR` y `OPQRST` junto con filtros locales que enmascaran DPI y teléfonos antes de serializar peticiones HTTP.
5. **Ejecución de inferencia local en Android con Kotlin Coroutines (`Dispatchers.IO`) y controles vectoriales en `Canvas`:** Aislamiento del motor local fuera del hilo principal de UI y renderizado directo con `DrawScope` sin dependencias pesadas de íconos.
6. **Integración reactiva de voz en Web (`SpeechRecognition` / `speechSynthesis`) y Android (`RecognizerIntent` / `TextToSpeech`):** Gestión del ciclo de vida de captura continua en español (`es-GT`) y acordeones progresivos de una pregunta a la vez en Material 3.

---

## 3. Estabilizador de Ingresos (`freelance-cashflow-smoother`)

### Producto y Finanzas Personales
1. **Algoritmos de suavizado estacional de ingresos para trabajadores independientes:** Modelado de la asimetría entre semanas o meses de cosecha alta y temporada baja para calcular cuánto apartar cada semana y cuál es el sueldo seguro disponible.
2. **Presupuestos bimonetarios nativos (`GTQ Q` y `USD $`) sin perder trazabilidad cambiaria:** Operación simultánea de ingresos en dólares y gastos esenciales en moneda local sin forzar una conversión destructiva.
3. **Diseño de interfaces financieras de baja carga cognitiva:** Separación en 3 pantallas (`1. Ingresos`, `2. Gastos`, `3. Tu Plan`) integrando métricas clave y simulador gráfico interactivo (`-50%` a `+50%`) en una sola vista de decisión.

### Ingeniería de Software
4. **Formulación matemática de `calculateSmoothing` y `computeDynamicTargetPct`:** Detección automática de regímenes estacionales (`>= 1.15x` temporada alta, `<= 0.85x` temporada baja), coeficiente de variación y tasa de retención acotada entre `5%` y `45%`.
5. **Normalización temporal reversible (`Por Mes` <-> `Por Semana` con factor `4.333`):** Transformación en vivo de series históricas bimonetarias sin deriva por redondeo.
6. **Optimización de simulaciones financieras interactivas en React con `useMemo` y Recharts:** Recálculo instantáneo de la curva estabilizada, superávit, retiro de reserva y semanas de liquidez (*runway*).

---

## 4. Estados de Cuenta (`card-statement-insights`)

### Producto y Finanzas Personales
1. **Extracción determinista en milisegundos (~6 ms) de estados de cuenta PDF frente a OCR y LLMs multimodales:** Lectura instantánea de cerca de 100 transacciones bimonetarias evitando latencias y timeouts por imágenes incrustadas en estados de cuenta bancarios.
2. **De estados de cuenta aislados a inteligencia de tendencias multi-mes:** Análisis progresivo de 1 a 3+ cortes mensuales para detectar aceleración de gasto por categoría, cargos hormiga y peso del extrafinanciamiento.
3. **Diseño de tableros financieros orientados a la decisión (`Actual` vs. `Meta`):** Escenarios interactivos que cuantifican el ahorro directo sobre el próximo corte de tarjeta en Quetzales y Dólares.

### Ingeniería de Software
4. **Anatomía de un parser PDF bancario en Node.js sin dependencias nativas (`zlib.inflateSync` y bloques `BT...ET`):** Descompresión de streams `/FlateDecode`, reconstrucción posicional por coordenadas (`Td`, `TD`, `Tm`) y decodificación octal/hexadecimal en `6.38 ms`.
5. **Máquina de estados léxica para separar consumos regulares (`GTQ` y `USD`) de tablas de extrafinanciamiento (`FIN/CT`, `FIN/IN`):** Partición en tres libros simultáneos para no distorsionar el gasto corriente del mes con saldos financiados a plazos.
6. **Fusión incremental multi-PDF en el cliente (`DataTransfer` / `FileList`) y matrices de velocidad de gasto (`spendVelocity`):** Deduplicación cronológica de períodos, cálculo de variaciones mes a mes (`MoM`) y proyección a 90 días.
