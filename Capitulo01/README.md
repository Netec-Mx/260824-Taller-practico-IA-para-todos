# Creación y validación de un asistente de IA generativa para una tarea laboral con Copilot Chat Standard

## Metadata

| Campo | Detalle |
|-------|---------|
| **Duración** | 105 minutos |
| **Complejidad** | Media |
| **Nivel de Bloom** | Crear |
| **Tecnología principal** | Microsoft Copilot Chat Standard (GPT-4o) |
| **Modalidad** | Práctica guiada individual |

---

## Descripción General

En este laboratorio diseñarás, construirás y validarás un asistente de IA generativa personalizado para una tarea real de tu entorno laboral utilizando Microsoft Copilot Chat Standard. Partirás del análisis estructurado de una necesidad profesional concreta, construirás un prompt maestro aplicando técnicas de ingeniería de prompts (zero-shot, few-shot, chain-of-thought), y evaluarás iterativamente la calidad de las respuestas del asistente mediante casos de prueba documentados. Al finalizar, tendrás un entregable reutilizable: una ficha de asistente completa que podrás aplicar inmediatamente en tu trabajo diario.

---

## Objetivos de Aprendizaje

Al completar este laboratorio, serás capaz de:

- [ ] Definir con precisión una tarea laboral real y descomponerla en componentes abordables por un asistente de IA generativa, estableciendo criterios claros de éxito.
- [ ] Construir un prompt maestro estructurado que configure el rol, tono, comportamiento, restricciones y formato de salida del asistente.
- [ ] Aplicar técnicas de ingeniería de prompts (zero-shot, few-shot, chain-of-thought) para refinar iterativamente las instrucciones y mejorar la calidad de las respuestas.
- [ ] Validar la efectividad del asistente mediante al menos 5 casos de prueba representativos, documentando fortalezas y limitaciones.
- [ ] Reflexionar sobre las implicaciones éticas, de privacidad y de uso responsable al implementar asistentes de IA en contextos laborales.

---

## Prerrequisitos

### Conocimientos previos

| Requisito | Descripción |
|-----------|-------------|
| Fundamentos de IA generativa | Comprender qué son los LLM, tokens, prompts y alucinaciones (curso *Generative AI for Everyone* o equivalente) |
| Tarea laboral identificada | Haber seleccionado previamente un ejemplo concreto de tarea, documento o necesidad real de tu trabajo |
| Navegación web básica | Saber utilizar un navegador moderno con múltiples pestañas |
| Edición de documentos | Capacidad de crear y editar documentos en Word o LibreOffice Writer |

### Acceso requerido

| Recurso | Detalle |
|---------|---------|
| Cuenta Microsoft activa | @outlook.com, @hotmail.com, @live.com, cuenta educativa @*.edu o corporativa Microsoft 365 |
| Copilot Chat Standard | Acceso verificado a https://copilot.microsoft.com |
| Conexión a internet | Mínimo 10 Mbps de descarga, estable durante 105 minutos |

---

## Entorno de Laboratorio

### Hardware mínimo

| Componente | Especificación mínima | Recomendado |
|------------|-----------------------|-------------|
| Procesador | Intel Core i5 8.ª gen / AMD Ryzen 5 3500U | Superior |
| RAM | 8 GB | 16 GB |
| Pantalla | 1366×768 px | 1920×1080 px |
| Almacenamiento libre | 2 GB | 5 GB |
| Periféricos | Teclado y mouse/trackpad funcionales | — |

### Software necesario

| Software | Versión | Propósito |
|----------|---------|-----------|
| Microsoft Edge o Google Chrome | Edge 124+ / Chrome 124+ | Navegador para acceder a Copilot |
| Microsoft Word o LibreOffice Writer | Word 2404 / LibreOffice 24.2.3 | Documentación de entregables |
| Herramienta de capturas de pantalla | Snipping Tool 11.2309+ / macOS Screenshot / GNOME Screenshot 41.0 | Evidencia visual |

### Configuración inicial del directorio de trabajo

Antes de comenzar, crea la estructura de carpetas estándar del taller en tu equipo:

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\Documents\TallerGenAI\Lab01" -Force
```

**Windows (Explorador de archivos):**
Navega a `Documentos` → Crea la carpeta `TallerGenAI` → Dentro de ella, crea `Lab01`.

**macOS (Terminal):**
```bash
mkdir -p ~/Documents/TallerGenAI/Lab01
```

**Linux (Terminal):**
```bash
mkdir -p ~/Documentos/TallerGenAI/Lab01
```

> **Nota:** Todos los archivos generados durante este laboratorio se guardarán en esta carpeta.

---

## Procedimiento Paso a Paso

### Paso 1: Verificación de acceso a Copilot Chat Standard (5 minutos)

**Objetivo:** Confirmar que tu cuenta Microsoft funciona correctamente y que puedes interactuar con Copilot Chat Standard sin restricciones.

**Instrucciones:**

1. Abre tu navegador (Edge o Chrome).
2. Navega a la URL: `https://copilot.microsoft.com`
3. Si no has iniciado sesión, haz clic en **Iniciar sesión** e ingresa las credenciales de tu cuenta Microsoft activa.
4. Una vez dentro de la interfaz de Copilot, verifica que aparece el campo de entrada de texto (prompt) en la parte inferior de la pantalla.
5. Escribe el siguiente prompt de prueba y presiona Enter:

```text
Hola, ¿puedes confirmarme que estás funcionando correctamente? Responde con una sola oración.
```

6. Espera la respuesta del modelo.
7. Toma una captura de pantalla de la interfaz mostrando tu prompt y la respuesta recibida.
8. Guarda la captura en tu directorio de trabajo con el nombre: `01_verificacion_acceso.png`

**Resultado esperado:**

Copilot responde con una oración breve confirmando que está operativo. La interfaz muestra el campo de chat activo y tu nombre de usuario en la esquina superior derecha.

**Verificación:**

- ✅ La interfaz de Copilot carga sin errores.
- ✅ Tu cuenta aparece como conectada (nombre visible).
- ✅ Recibes una respuesta coherente al prompt de prueba.
- ✅ La captura de pantalla se guardó correctamente en `Documentos/TallerGenAI/Lab01/`.

---

### Paso 2: Análisis y definición de la tarea laboral (15 minutos)

**Objetivo:** Descomponer tu tarea laboral real en componentes estructurados que un asistente de IA pueda abordar, y establecer criterios medibles de éxito.

**Instrucciones:**

1. Abre un documento nuevo en Word o LibreOffice Writer.
2. Guárdalo inmediatamente con el nombre estándar:
   `RegistroPrompts_[TuNombre]_[FechaYYYYMMDD].docx`
   
   Ejemplo: `RegistroPrompts_MariaGarcia_20240515.docx`

3. En la primera página del documento, crea la siguiente tabla de análisis y complétala con información de tu tarea laboral real:

```text
╔══════════════════════════════════════════════════════════════════╗
║ ANÁLISIS ESTRUCTURADO DE TAREA LABORAL                         ║
╠══════════════════════════════════════════════════════════════════╣
║ Nombre de la tarea:                                            ║
║ [Ej: Redacción de correos de seguimiento a clientes]           ║
╠══════════════════════════════════════════════════════════════════╣
║ Frecuencia de ejecución:                                       ║
║ [Ej: 5-10 veces por semana]                                    ║
╠══════════════════════════════════════════════════════════════════╣
║ Tiempo promedio actual:                                        ║
║ [Ej: 15-20 minutos por correo]                                 ║
╠══════════════════════════════════════════════════════════════════╣
║ Resultado esperado de la tarea:                                ║
║ [Ej: Correo profesional, claro, con tono empático y            ║
║  llamada a la acción específica]                               ║
╠══════════════════════════════════════════════════════════════════╣
║ Componentes descomponibles para IA:                            ║
║ 1. [Ej: Generar saludo personalizado según contexto]           ║
║ 2. [Ej: Estructurar cuerpo del mensaje con puntos clave]      ║
║ 3. [Ej: Proponer cierre con llamada a la acción]              ║
║ 4. [Ej: Ajustar tono según tipo de cliente]                   ║
║ 5. [Ej: Revisar gramática y coherencia]                       ║
╠══════════════════════════════════════════════════════════════════╣
║ Criterios de éxito (mínimo 3):                                 ║
║ 1. [Ej: El texto es gramaticalmente correcto]                  ║
║ 2. [Ej: El tono es apropiado para el destinatario]             ║
║ 3. [Ej: Incluye toda la información necesaria]                 ║
║ 4. [Ej: Se genera en menos de 2 minutos]                      ║
╠══════════════════════════════════════════════════════════════════╣
║ Información sensible a NO incluir en prompts:                  ║
║ [Ej: Nombres reales de clientes, datos financieros,            ║
║  información confidencial de la empresa]                       ║
╚══════════════════════════════════════════════════════════════════╝
```

4. Reflexiona sobre la última fila: identifica qué datos **nunca** debes compartir con el modelo por razones de privacidad y confidencialidad. Recuerda que los LLM como GPT-4o procesan tokens de texto y que la información ingresada puede ser utilizada según las políticas de la plataforma.

5. Guarda el documento.

**Resultado esperado:**

Un análisis completo con al menos 3 componentes descomponibles, 3 criterios de éxito medibles y una lista clara de restricciones de privacidad.

**Verificación:**

- ✅ La tarea seleccionada es una necesidad real de tu trabajo (no un ejemplo ficticio).
- ✅ Has identificado al menos 3 componentes que la IA puede abordar.
- ✅ Los criterios de éxito son específicos y verificables (no vagos).
- ✅ Has documentado explícitamente qué información sensible no compartirás.

---

### Paso 3: Diseño del prompt maestro (system prompt) (20 minutos)

**Objetivo:** Construir un prompt maestro completo y estructurado que defina el comportamiento de tu asistente de IA personalizado, utilizando la plantilla estándar del taller.

**Instrucciones:**

1. En tu documento `RegistroPrompts_[TuNombre]_[Fecha].docx`, crea una nueva sección titulada **"PROMPT MAESTRO - VERSIÓN 1"**.

2. Utiliza la siguiente plantilla estructurada. Completa cada sección con información específica para tu tarea laboral:

```text
=== PROMPT MAESTRO v1.0 ===

[ROL DEL ASISTENTE]
Eres un [rol específico] especializado en [dominio]. Tu nombre es [nombre del asistente].
Tienes experiencia en [áreas de conocimiento relevantes].

[CONTEXTO DE USO]
Trabajas como asistente para [descripción del usuario: rol profesional].
El entorno de trabajo es [tipo de organización/industria].
Las interacciones serán en español y se realizarán durante [contexto temporal/situacional].

[INSTRUCCIONES DE COMPORTAMIENTO]
1. Siempre [comportamiento principal esperado].
2. Utiliza un tono [descripción del tono: formal/semiformal/técnico/empático].
3. Estructura tus respuestas con [formato preferido: listas, párrafos, tablas].
4. Antes de responder, [proceso de razonamiento esperado].
5. Si no tienes suficiente información, [qué hacer: preguntar, indicar supuestos].

[RESTRICCIONES Y LIMITACIONES]
- NUNCA [restricción crítica 1].
- NUNCA [restricción crítica 2].
- NO inventes [tipo de información que no debe fabricar].
- Si te piden algo fuera de tu rol, responde: "[mensaje estándar de rechazo]".
- Limita tus respuestas a un máximo de [número] palabras/párrafos salvo que se pida más.

[FORMATO DE SALIDA ESPERADO]
Las respuestas deben seguir esta estructura:
1. [Sección 1 del formato]
2. [Sección 2 del formato]
3. [Sección 3 del formato]

[EJEMPLOS DE REFERENCIA (few-shot)]
--- Ejemplo 1 ---
Entrada del usuario: [ejemplo de solicitud típica]
Respuesta esperada: [ejemplo de respuesta ideal]

--- Ejemplo 2 ---
Entrada del usuario: [otro ejemplo de solicitud]
Respuesta esperada: [otra respuesta ideal]
```

3. **Ejemplo completo de referencia** — A continuación se muestra un prompt maestro completado para una tarea de redacción de correos de seguimiento comercial. Úsalo como inspiración, pero **adapta todo a tu tarea real**:

```text
=== PROMPT MAESTRO v1.0 ===

[ROL DEL ASISTENTE]
Eres un asistente de comunicación comercial especializado en redacción de correos 
de seguimiento para clientes del sector tecnológico. Tu nombre es AsistenteComm.
Tienes experiencia en comunicación corporativa, ventas consultivas y gestión de 
relaciones con clientes B2B.

[CONTEXTO DE USO]
Trabajas como asistente para un ejecutivo de cuentas en una empresa de software.
El entorno de trabajo es una empresa mediana de tecnología con clientes corporativos.
Las interacciones serán en español y se realizarán para preparar comunicaciones 
de seguimiento post-reunión o post-propuesta.

[INSTRUCCIONES DE COMPORTAMIENTO]
1. Siempre genera correos completos listos para enviar (asunto + cuerpo + cierre).
2. Utiliza un tono profesional pero cercano, evitando jerga excesivamente técnica.
3. Estructura tus respuestas con: Asunto sugerido, Cuerpo del correo, Notas internas.
4. Antes de responder, identifica el objetivo principal del seguimiento.
5. Si no tienes suficiente información sobre el contexto, pregunta antes de redactar.

[RESTRICCIONES Y LIMITACIONES]
- NUNCA inventes nombres de personas, empresas o datos específicos del cliente.
- NUNCA incluyas promesas de descuentos o condiciones comerciales no autorizadas.
- NO generes contenido que pueda interpretarse como presión indebida al cliente.
- Si te piden algo fuera de comunicación comercial, responde: "Eso está fuera de 
  mi especialidad. ¿Puedo ayudarte con algún correo o comunicación?".
- Limita el cuerpo del correo a un máximo de 150 palabras salvo indicación contraria.

[FORMATO DE SALIDA ESPERADO]
Las respuestas deben seguir esta estructura:
1. **Asunto sugerido:** [línea de asunto]
2. **Cuerpo del correo:** [texto completo]
3. **Notas internas:** [sugerencias o consideraciones para el usuario]

[EJEMPLOS DE REFERENCIA (few-shot)]
--- Ejemplo 1 ---
Entrada del usuario: Necesito un correo de seguimiento para un cliente que recibió 
nuestra propuesta hace 5 días y no ha respondido. El proyecto es una migración a la nube.
Respuesta esperada:
**Asunto sugerido:** Seguimiento: Propuesta de migración a la nube
**Cuerpo del correo:**
Estimado/a [nombre del cliente]:

Espero que se encuentre bien. Me permito dar seguimiento a la propuesta que 
compartimos el [fecha] sobre el proyecto de migración a la nube.

Quedo a su disposición para resolver cualquier duda o agendar una breve llamada 
para revisar los puntos clave. ¿Le funcionaría algún horario esta semana?

Saludos cordiales,
[Tu nombre]

**Notas internas:** Considerar si conviene mencionar algún beneficio adicional 
o caso de éxito relevante para reactivar el interés.
```

4. Revisa tu prompt maestro y verifica que:
   - El rol es específico (no genérico como "eres un asistente útil").
   - Las instrucciones de comportamiento son accionables y claras.
   - Las restricciones protegen información sensible.
   - Los ejemplos few-shot ilustran el formato de salida deseado.

5. Guarda el documento.

**Resultado esperado:**

Un prompt maestro completo de al menos 200 palabras con las 6 secciones de la plantilla rellenadas de forma específica para tu tarea laboral.

**Verificación:**

- ✅ Las 6 secciones de la plantilla están completas (ninguna vacía).
- ✅ El rol del asistente es específico y relevante para tu tarea.
- ✅ Incluyes al menos 2 ejemplos few-shot con entrada y salida esperada.
- ✅ Las restricciones incluyen al menos una protección de privacidad/datos sensibles.
- ✅ El formato de salida es claro y reproducible.

---

### Paso 4: Primera prueba del asistente en Copilot Chat Standard (10 minutos)

**Objetivo:** Introducir tu prompt maestro en Copilot Chat Standard y realizar la primera interacción para evaluar el comportamiento inicial del asistente.

**Instrucciones:**

1. Regresa a la pestaña de Copilot Chat Standard en tu navegador (`https://copilot.microsoft.com`).

2. Si tienes una conversación previa abierta, inicia una **nueva conversación** haciendo clic en el ícono de "Nuevo chat" o "New topic" (generalmente un ícono de "+" o lápiz en la esquina superior).

3. Copia tu prompt maestro completo (versión 1) desde tu documento de Word/LibreOffice.

4. Pégalo en el campo de entrada de Copilot y envíalo. Este será tu **mensaje inicial** que establece el contexto del asistente.

   > **Importante:** En Copilot Chat Standard no existe un campo separado de "system prompt". El prompt maestro se introduce como el primer mensaje de la conversación. El modelo lo utilizará como contexto para todas las interacciones subsiguientes en esa sesión.

5. Observa la respuesta de Copilot. Típicamente, el modelo confirmará que ha entendido su rol y estará listo para recibir solicitudes.

6. Ahora envía tu **primera solicitud de prueba** — un caso simple y directo de tu tarea laboral:

```text
[Tu primera solicitud basada en tu tarea real]
```

   Ejemplo para el caso de correos comerciales:
```text
Necesito un correo de seguimiento para un cliente del sector retail que asistió 
a nuestra demo de producto hace 3 días. Mostró interés en la funcionalidad de 
reportes automatizados.
```

7. Evalúa la respuesta según tus criterios de éxito definidos en el Paso 2.

8. Toma una captura de pantalla del prompt maestro enviado y la primera respuesta. Guárdala como `02_primera_prueba.png`.

9. En tu documento de registro, crea una tabla de evaluación:

```text
┌─────────────────────────────────────────────────────────────┐
│ EVALUACIÓN DE PRUEBA #1                                     │
├─────────────────────────────────────────────────────────────┤
│ Solicitud enviada: [tu solicitud]                           │
│ Respuesta recibida: [resumen de la respuesta]               │
│                                                             │
│ Criterio 1 [nombre]: ☐ Cumple  ☐ No cumple  ☐ Parcial     │
│ Criterio 2 [nombre]: ☐ Cumple  ☐ No cumple  ☐ Parcial     │
│ Criterio 3 [nombre]: ☐ Cumple  ☐ No cumple  ☐ Parcial     │
│ Criterio 4 [nombre]: ☐ Cumple  ☐ No cumple  ☐ Parcial     │
│                                                             │
│ Observaciones: [qué funcionó bien, qué necesita mejora]     │
└─────────────────────────────────────────────────────────────┘
```

**Resultado esperado:**

Copilot responde asumiendo el rol definido en tu prompt maestro, genera contenido en el formato especificado y respeta el tono indicado. La respuesta puede no ser perfecta en el primer intento — esto es esperado y se refinará en los siguientes pasos.

**Verificación:**

- ✅ Copilot reconoce y adopta el rol definido en el prompt maestro.
- ✅ La respuesta sigue (al menos parcialmente) el formato de salida especificado.
- ✅ El tono de la respuesta se alinea con lo solicitado.
- ✅ Has documentado la evaluación en tu registro de prompts.

---

### Paso 5: Refinamiento iterativo con técnicas de prompting (25 minutos)

**Objetivo:** Aplicar técnicas de ingeniería de prompts para mejorar la calidad de las respuestas del asistente, realizando al menos 3 iteraciones de refinamiento.

**Instrucciones:**

#### Iteración A: Refinamiento por especificidad (8 minutos)

1. Basándote en las observaciones de tu primera prueba, identifica el aspecto más débil de la respuesta.

2. Modifica tu prompt maestro para abordar esa debilidad. Aplica la técnica **zero-shot mejorado** — añade instrucciones más específicas sin dar ejemplos adicionales:

```text
[Instrucción adicional para corregir el problema identificado]

Ejemplo de refinamiento:
ANTES: "Utiliza un tono profesional pero cercano"
DESPUÉS: "Utiliza un tono profesional pero cercano. Esto significa: usa 'usted' 
en el saludo inicial, pero puedes usar expresiones cálidas como 'espero que se 
encuentre bien' o 'será un gusto'. Evita emojis y abreviaturas."
```

3. Inicia un **nuevo chat** en Copilot (importante: cada iteración del prompt maestro debe probarse en una conversación limpia).

4. Envía tu prompt maestro refinado (versión 1.1) y luego la misma solicitud de prueba del Paso 4.

5. Compara la nueva respuesta con la anterior. Documenta en tu registro:

```text
┌─────────────────────────────────────────────────────────────┐
│ ITERACIÓN A - Refinamiento por especificidad                │
├─────────────────────────────────────────────────────────────┤
│ Cambio realizado: [qué modificaste en el prompt]            │
│ Técnica aplicada: Zero-shot mejorado                        │
│ Mejora observada: [descripción concreta]                    │
│ Problema persistente: [si lo hay]                           │
└─────────────────────────────────────────────────────────────┘
```

#### Iteración B: Refinamiento con few-shot adicional (8 minutos)

6. Si la respuesta aún no cumple algún criterio, aplica la técnica **few-shot** — añade un ejemplo adicional que ilustre exactamente el comportamiento deseado para el caso problemático:

```text
--- Ejemplo 3 (nuevo) ---
Entrada del usuario: [caso similar al que falla]
Respuesta esperada: [respuesta ideal que quieres que el modelo imite]
```

7. Inicia un nuevo chat, envía el prompt maestro actualizado (versión 1.2) y prueba con una **nueva solicitud** diferente a la anterior (tu segundo caso de prueba).

8. Documenta los resultados usando la misma tabla de evaluación.

#### Iteración C: Refinamiento con chain-of-thought (9 minutos)

9. Para mejorar la calidad del razonamiento del asistente, aplica la técnica **chain-of-thought** (cadena de pensamiento). Añade a tu sección de [INSTRUCCIONES DE COMPORTAMIENTO]:

```text
Antes de generar tu respuesta final, sigue estos pasos internos de razonamiento:
Paso 1: Identifica el objetivo principal de la solicitud del usuario.
Paso 2: Determina qué información clave tienes y cuál te falta.
Paso 3: Si tienes toda la información necesaria, genera la respuesta. 
        Si no, formula una pregunta de clarificación.
Paso 4: Verifica que tu respuesta cumple con el formato de salida definido.

Muestra tu razonamiento brevemente antes de la respuesta final bajo el 
encabezado "💭 Análisis:" (máximo 2-3 líneas).
```

10. Inicia un nuevo chat, envía el prompt maestro actualizado (versión 1.3) y prueba con un **tercer caso de prueba** — preferiblemente uno más complejo o ambiguo.

11. Evalúa si el chain-of-thought mejora la calidad y relevancia de la respuesta.

12. Documenta los resultados de esta iteración.

13. Guarda tu documento con todas las iteraciones registradas.

**Resultado esperado:**

Después de 3 iteraciones, tu prompt maestro ha evolucionado de la versión 1.0 a la versión 1.3, con mejoras documentadas en al menos uno de tus criterios de éxito. Las respuestas del asistente son notablemente más alineadas con tus expectativas.

**Verificación:**

- ✅ Has realizado al menos 3 iteraciones con técnicas distintas (zero-shot mejorado, few-shot, chain-of-thought).
- ✅ Cada iteración está documentada con: cambio realizado, técnica aplicada, resultado observado.
- ✅ Al menos un criterio de éxito muestra mejora medible entre la versión 1.0 y la 1.3.
- ✅ Has probado con al menos 3 solicitudes diferentes (no la misma repetida).

---

### Paso 6: Batería de pruebas de validación (10 minutos)

**Objetivo:** Ejecutar un conjunto completo de al menos 5 casos de prueba para validar la robustez del asistente con tu prompt maestro final.

**Instrucciones:**

1. Inicia un **nuevo chat** en Copilot y envía tu prompt maestro en su versión final (1.3 o la última iteración que hayas alcanzado).

2. Prepara y ejecuta secuencialmente los siguientes 5 tipos de casos de prueba (adaptados a tu tarea específica):

| # | Tipo de caso | Descripción | Propósito |
|---|---|---|---|
| 1 | **Caso típico** | La solicitud más frecuente y estándar de tu tarea | Verificar funcionamiento base |
| 2 | **Caso complejo** | Una solicitud con múltiples variables o requisitos | Evaluar capacidad de manejo de complejidad |
| 3 | **Caso con información incompleta** | Una solicitud deliberadamente vaga o con datos faltantes | Verificar que el asistente pide clarificación |
| 4 | **Caso límite (edge case)** | Una solicitud inusual o en el borde del alcance definido | Evaluar robustez de las restricciones |
| 5 | **Caso fuera de alcance** | Una solicitud que NO debería atender según las restricciones | Verificar que rechaza apropiadamente |

3. Para cada caso, documenta en tu registro:

```text
┌─────────────────────────────────────────────────────────────┐
│ CASO DE PRUEBA #[N]                                         │
├─────────────────────────────────────────────────────────────┤
│ Tipo: [típico/complejo/incompleto/límite/fuera de alcance]  │
│ Solicitud enviada: [texto exacto]                           │
│ Respuesta resumida: [resumen de 2-3 líneas]                 │
│ ¿Cumple criterios?: Sí / No / Parcial                      │
│ Puntuación (1-5): [calificación subjetiva de calidad]       │
│ Observaciones: [notas relevantes]                           │
└─────────────────────────────────────────────────────────────┘
```

4. Calcula tu **tasa de éxito**: número de casos que cumplen criterios / 5 total.

5. Toma una captura de pantalla que muestre al menos 2 interacciones de prueba. Guárdala como `03_bateria_pruebas.png`.

**Resultado esperado:**

Al menos 3 de 5 casos (60%) cumplen satisfactoriamente los criterios de éxito. El caso fuera de alcance es rechazado apropiadamente. El caso con información incompleta genera una pregunta de clarificación.

**Verificación:**

- ✅ Has ejecutado exactamente 5 casos de prueba de tipos diferentes.
- ✅ Cada caso está documentado con solicitud, respuesta y evaluación.
- ✅ La tasa de éxito es al menos 60% (3/5 casos exitosos).
- ✅ El asistente maneja correctamente al menos 1 caso de rechazo o clarificación.

---

### Paso 7: Documentación en la Ficha de Asistente (15 minutos)

**Objetivo:** Consolidar todo el trabajo realizado en un documento entregable estandarizado y reutilizable: la Ficha de Asistente de IA.

**Instrucciones:**

1. Crea un **nuevo documento** en Word o LibreOffice Writer.

2. Guárdalo con el nombre estándar:
   `FichaAsistente_[TuNombre]_[FechaYYYYMMDD].docx`
   
   Ejemplo: `FichaAsistente_MariaGarcia_20240515.docx`

3. Completa la ficha con la siguiente estructura:

```text
════════════════════════════════════════════════════════════════
        FICHA DE ASISTENTE DE IA GENERATIVA
════════════════════════════════════════════════════════════════

1. DATOS GENERALES
   ─────────────────
   • Nombre del asistente: [nombre que le asignaste]
   • Autor/a: [tu nombre completo]
   • Fecha de creación: [fecha del taller]
   • Versión del prompt: [ej: 1.3]
   • Plataforma: Microsoft Copilot Chat Standard (GPT-4o)
   • Tarea laboral que apoya: [nombre de la tarea]

2. PROMPT MAESTRO FINAL
   ─────────────────────
   [Copia aquí tu prompt maestro en su versión final completa]

3. INSTRUCCIONES DE USO
   ─────────────────────
   Para utilizar este asistente:
   a) Abrir un nuevo chat en copilot.microsoft.com
   b) Pegar el prompt maestro como primer mensaje
   c) Esperar confirmación del asistente
   d) Enviar solicitudes según los ejemplos documentados
   
   Tipos de solicitudes que atiende:
   • [Tipo 1]
   • [Tipo 2]
   • [Tipo 3]
   
   Tipos de solicitudes que NO atiende:
   • [Tipo 1]
   • [Tipo 2]

4. RESULTADOS DE VALIDACIÓN
   ─────────────────────────
   Tasa de éxito general: [X/5] = [porcentaje]%
   
   Fortalezas identificadas:
   • [Fortaleza 1]
   • [Fortaleza 2]
   • [Fortaleza 3]
   
   Limitaciones identificadas:
   • [Limitación 1]
   • [Limitación 2]
   
   Áreas de mejora futura:
   • [Mejora 1]
   • [Mejora 2]

5. CONSIDERACIONES ÉTICAS Y DE PRIVACIDAD
   ────────────────────────────────────────
   • Datos que NUNCA deben ingresarse: [lista]
   • Riesgos de alucinación identificados: [descripción]
   • Necesidad de revisión humana: [Sí/No y en qué casos]
   • Sesgo potencial detectado: [si aplica]

6. HISTORIAL DE VERSIONES
   ───────────────────────
   v1.0 - [fecha] - Versión inicial
   v1.1 - [fecha] - [cambio realizado, técnica: zero-shot mejorado]
   v1.2 - [fecha] - [cambio realizado, técnica: few-shot]
   v1.3 - [fecha] - [cambio realizado, técnica: chain-of-thought]

════════════════════════════════════════════════════════════════
```

4. Revisa que todas las secciones estén completas y que el prompt maestro final sea una copia exacta y funcional (que alguien más podría copiar y usar directamente).

5. Guarda el documento final.

**Resultado esperado:**

Un documento completo de 2-4 páginas que cualquier colega podría utilizar para replicar tu asistente de IA sin asistencia adicional.

**Verificación:**

- ✅ Las 6 secciones de la ficha están completas.
- ✅ El prompt maestro final es una copia exacta y funcional (copiar-pegar directo).
- ✅ Las instrucciones de uso son claras para un tercero.
- ✅ La sección de ética y privacidad contiene reflexiones específicas (no genéricas).
- ✅ El historial de versiones refleja las iteraciones reales realizadas.

---

### Paso 8: Reflexión ética y cierre (5 minutos)

**Objetivo:** Reflexionar críticamente sobre las implicaciones de implementar tu asistente en un contexto laboral real.

**Instrucciones:**

1. En tu documento de Registro de Prompts, añade una sección final titulada **"REFLEXIÓN ÉTICA"**.

2. Responde brevemente (3-5 oraciones cada una) las siguientes preguntas:

```text
REFLEXIÓN ÉTICA SOBRE MI ASISTENTE DE IA
─────────────────────────────────────────

a) ¿Qué pasaría si mi asistente genera una respuesta incorrecta (alucinación) 
   y yo la uso sin verificar? ¿Cuál sería el impacto en mi trabajo?

   [Tu respuesta]

b) ¿Qué información de mi trabajo NO debería nunca ingresar en esta herramienta, 
   incluso si mejoraría las respuestas? ¿Por qué?

   [Tu respuesta]

c) ¿En qué situaciones es indispensable la revisión humana de las respuestas 
   del asistente antes de usarlas?

   [Tu respuesta]

d) ¿Cómo puedo asegurarme de que el uso de este asistente no reemplace 
   mi criterio profesional sino que lo complemente?

   [Tu respuesta]
```

3. Guarda el documento final.

4. Verifica que tienes los siguientes archivos en tu carpeta `Documentos/TallerGenAI/Lab01/`:

```text
Documentos/TallerGenAI/Lab01/
├── 01_verificacion_acceso.png
├── 02_primera_prueba.png
├── 03_bateria_pruebas.png
├── RegistroPrompts_[TuNombre]_[Fecha].docx
└── FichaAsistente_[TuNombre]_[Fecha].docx
```

**Resultado esperado:**

Una reflexión honesta y específica que demuestra comprensión de los riesgos reales (alucinaciones, privacidad, dependencia excesiva) y cómo mitigarlos en tu contexto laboral particular.

**Verificación:**

- ✅ Las 4 preguntas de reflexión están respondidas con contenido específico (no genérico).
- ✅ Mencionas al menos un riesgo concreto de alucinación relevante para tu tarea.
- ✅ Identificas datos sensibles específicos de tu contexto laboral.
- ✅ Todos los archivos del laboratorio están guardados en la carpeta correcta.

---

## Validación y Pruebas Finales

Utiliza la siguiente lista de verificación integral para confirmar que has completado exitosamente el laboratorio:

### Lista de verificación de entregables

| # | Entregable | Criterio de aceptación | Estado |
|---|---|---|---|
| 1 | Captura de verificación de acceso | Muestra Copilot activo con tu cuenta | ☐ |
| 2 | Análisis de tarea laboral | Mínimo 3 componentes + 3 criterios de éxito | ☐ |
| 3 | Prompt maestro v1.0 | 6 secciones completas de la plantilla | ☐ |
| 4 | Registro de iteraciones | Mínimo 3 iteraciones con técnicas distintas | ☐ |
| 5 | Batería de 5 pruebas | 5 casos documentados con evaluación | ☐ |
| 6 | Tasa de éxito ≥ 60% | Al menos 3/5 casos exitosos | ☐ |
| 7 | Ficha de Asistente completa | 6 secciones, prompt copiable, instrucciones claras | ☐ |
| 8 | Reflexión ética | 4 preguntas respondidas con especificidad | ☐ |
| 9 | Archivos organizados | 5 archivos en la ruta correcta | ☐ |

### Prueba de funcionalidad final

Para confirmar que tu asistente es reutilizable:

1. Abre un **nuevo chat** completamente limpio en Copilot.
2. Copia el prompt maestro final directamente desde tu Ficha de Asistente.
3. Pégalo y envíalo.
4. Envía una solicitud que **no** hayas usado durante las pruebas anteriores (un sexto caso nuevo).
5. Verifica que la respuesta cumple con tus criterios de éxito.

Si la respuesta es satisfactoria, tu asistente está validado y listo para uso en producción. Si no lo es, identifica qué ajuste adicional necesitaría y anótalo en la sección "Áreas de mejora futura" de tu ficha.

---

## Solución de Problemas

### Problema 1: Copilot no adopta el rol definido en el prompt maestro

**Síntomas:** Después de enviar tu prompt maestro, Copilot responde de forma genérica, ignora el rol asignado, no sigue el formato especificado o responde como si fuera un asistente general sin personalización.

**Causa:** El prompt maestro es demasiado largo y las instrucciones clave se diluyen, o la estructura no es lo suficientemente directiva. Copilot Chat Standard procesa el primer mensaje como contexto, pero si el mensaje es ambiguo o excesivamente extenso (>2000 palabras), puede perder adherencia a las instrucciones iniciales. También puede ocurrir si el modelo interpreta el prompt como una consulta informativa en lugar de instrucciones de configuración.

**Solución:**

1. **Reestructura el inicio del prompt** — Comienza con una instrucción directiva inequívoca:
```text
INSTRUCCIONES DE SISTEMA: A partir de este momento, adopta el siguiente rol 
y compórtate EXACTAMENTE como se describe a continuación. No rompas este 
personaje en ninguna respuesta posterior.
```

2. **Reduce la extensión** — Si tu prompt supera las 800 palabras, prioriza las secciones [ROL], [INSTRUCCIONES DE COMPORTAMIENTO] y [RESTRICCIONES]. Los ejemplos few-shot pueden proporcionarse en un segundo mensaje.

3. **Usa formato imperativo** — Cambia frases pasivas ("Se espera que uses un tono formal") por directivas ("USA un tono formal en TODAS las respuestas").

4. **Envía una confirmación explícita** — Después del prompt maestro, envía:
```text
Confirma que has entendido tu rol respondiendo con: tu nombre, tu especialidad 
y las 3 reglas principales que seguirás.
```

5. Si el problema persiste, divide el prompt en dos mensajes: primero el rol y restricciones, luego los ejemplos y formato.

---

### Problema 2: Las respuestas contienen información inventada (alucinaciones)

**Síntomas:** El asistente genera datos, nombres, estadísticas, fechas o referencias que parecen plausibles pero son fabricados. Por ejemplo, inventa nombres de clientes, cita políticas inexistentes o proporciona datos numéricos sin fuente.

**Causa:** Los LLM como GPT-4o generan texto prediciendo el siguiente token más probable. Cuando la solicitud requiere información específica que no está en el contexto proporcionado, el modelo "completa" con contenido plausible pero ficticio. Esto es inherente a la arquitectura Transformer y ocurre con mayor frecuencia cuando: (a) el prompt no establece claramente qué hacer ante falta de información, (b) se piden datos específicos sin proporcionarlos, o (c) no hay restricciones explícitas contra la fabricación de datos.

**Solución:**

1. **Añade una restricción anti-alucinación explícita** en tu sección [RESTRICCIONES]:
```text
- Si no tienes la información específica solicitada, indica claramente: 
  "No cuento con ese dato. Por favor proporciónalo para continuar."
- NUNCA inventes datos, nombres, cifras, fechas o referencias. 
  Usa marcadores como [DATO PENDIENTE] o [INSERTAR NOMBRE] cuando 
  necesites información que no te he proporcionado.
- Distingue siempre entre hechos verificables y sugerencias/recomendaciones.
```

2. **Proporciona el contexto necesario** en cada solicitud — En lugar de pedir "redacta un informe sobre las ventas del trimestre", proporciona los datos: "redacta un informe con estos datos de ventas: [datos]".

3. **Añade una instrucción de verificación** al formato de salida:
```text
Al final de cada respuesta, incluye una sección:
⚠️ VERIFICAR: [lista de afirmaciones que el usuario debe confirmar antes de usar]
```

4. **Establece el hábito de revisión** — Siempre lee las respuestas del asistente antes de usarlas. Ningún LLM actual es 100% confiable para datos factuales.

---

## Limpieza del Entorno

Al finalizar el laboratorio:

1. **Cierra las sesiones de chat** en Copilot que ya no necesites (puedes mantener la última para referencia futura).

2. **Verifica tus archivos** — Confirma que todos los documentos están guardados correctamente en `Documentos/TallerGenAI/Lab01/`.

3. **No elimines tu directorio de trabajo** — Los archivos generados son tu entregable del taller y podrás reutilizarlos en tu trabajo diario.

4. **Opcional:** Si deseas compartir tu Ficha de Asistente con colegas, asegúrate de:
   - Eliminar cualquier referencia a datos sensibles o confidenciales.
   - Verificar que los ejemplos few-shot no contienen información real de clientes o proyectos.
   - Reemplazar nombres reales por marcadores genéricos ([nombre del cliente], [empresa]).

5. **Cierra sesión de tu cuenta Microsoft** si estás en un equipo compartido.

---

## Resumen

### Lo que lograste en este laboratorio

En 105 minutos has completado el ciclo completo de creación de un asistente de IA generativa personalizado:

1. **Analizaste** una tarea laboral real y la descompusiste en componentes abordables por IA.
2. **Diseñaste** un prompt maestro estructurado con 6 secciones (rol, contexto, instrucciones, restricciones, formato, ejemplos).
3. **Aplicaste** tres técnicas de ingeniería de prompts: zero-shot mejorado, few-shot y chain-of-thought.
4. **Iteraste** al menos 3 veces sobre tu diseño, mejorando la calidad de las respuestas.
5. **Validaste** con 5 casos de prueba y documentaste una tasa de éxito medible.
6. **Documentaste** todo en una ficha reutilizable que puedes aplicar mañana en tu trabajo.
7. **Reflexionaste** sobre las implicaciones éticas y de privacidad del uso de IA en tu contexto.

### Conceptos clave aplicados

| Concepto | Aplicación en el laboratorio |
|----------|------------------------------|
| LLM y arquitectura Transformer | Comprender por qué Copilot genera respuestas probabilísticas, no determinísticas |
| Tokens | Entender las limitaciones de longitud del prompt y las respuestas |
| Alucinaciones | Diseñar restricciones que minimicen la fabricación de información |
| Ingeniería de prompts | Técnicas zero-shot, few-shot y chain-of-thought para mejorar resultados |
| Alineación (RLHF) | Comprender por qué el modelo sigue instrucciones de rol y restricciones |

### Próximos pasos recomendados

- **Usa tu asistente diariamente** durante al menos una semana y anota los casos donde falla.
- **Itera sobre el prompt** cada vez que identifiques un patrón de error recurrente.
- **Comparte tu ficha** con colegas de tu equipo para que puedan beneficiarse y dar retroalimentación.
- **Explora variaciones**: crea versiones del asistente para subtareas diferentes dentro de tu trabajo.
- **Mantente actualizado**: los modelos de IA se actualizan frecuentemente; tu prompt puede necesitar ajustes cuando cambie la versión del modelo.

### Recursos adicionales

| Recurso | Enlace |
|---------|--------|
| Documentación oficial de Microsoft Copilot | https://support.microsoft.com/copilot |
| Guía de prompting de OpenAI | https://platform.openai.com/docs/guides/prompt-engineering |
| Curso NLP de Hugging Face (español) | https://huggingface.co/learn/nlp-course/es/chapter1/1 |
| Artículo "Attention is All You Need" | https://arxiv.org/abs/1706.03762 |
| Principios de IA responsable de Microsoft | https://www.microsoft.com/ai/responsible-ai |

---
