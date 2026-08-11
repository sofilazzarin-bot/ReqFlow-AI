# 🤖 ReqFlow AI – Requerimientos Inteligentes

## 📌 Descripción

ReqFlow AI es un ecosistema de automatización basado en Inteligencia Artificial diseñado para recibir, analizar, clasificar y gestionar requerimientos de negocio de extremo a extremo.

El sistema utiliza **Make** como orquestador, **GPT-5 mini** como motor de IA, **Airtable** como memoria y base de datos, **Telegram** para la validación humana (Human-in-the-loop) y **Gmail** como canal de comunicación final.

## 🎯 Objetivo

Automatizar el procesamiento de requerimientos recibidos por correo electrónico, reduciendo tareas manuales y manteniendo trazabilidad sobre cada solicitud.

El sistema permite:

- Identificar si el mensaje corresponde a un requerimiento.
- Detectar requerimientos con información incompleta.
- Determinar prioridad mediante IA.
- Generar User Stories y criterios de aceptación.
- Registrar la información en Airtable.
- Solicitar aprobación humana antes de una acción crítica.
- Registrar aprobación o rechazo.
- Notificar el resultado mediante Gmail.
- Gestionar rutas alternativas y errores del proceso.

## 🏗️ Arquitectura

El flujo principal implementado es:

`Mailhook → Airtable → GPT-5 mini → Parse JSON → Airtable → Router`

A partir del Router se gestionan tres caminos principales:

### 1. Requerimiento completo
`Airtable → Telegram → Human-in-the-loop → Router → Aprobado/Rechazado → Airtable → Gmail`

### 2. Datos incompletos
`Airtable → Gmail`

### 3. No corresponde
`Airtable`

## 🧠 Procesamiento con IA

GPT-5 mini analiza dinámicamente el mensaje recibido y genera una respuesta estructurada en JSON.

Entre las variables procesadas se encuentran:

- `es_requerimiento`
- `esta_completo`
- `prioridad`
- `user_story`
- `criterios_aceptacion`
- `datos_faltantes`
- `area_responsable`

La salida estructurada permite que Make utilice los resultados en filtros, routers y actualizaciones posteriores.

## 🗄️ Base de datos

Airtable funciona como memoria y sistema de trazabilidad de ReqFlow AI.

Se registran datos como:

- ID del requerimiento
- Fecha de recepción
- Remitente
- Asunto
- Mensaje original
- Estado
- Clasificación realizada por IA
- Prioridad
- User Story
- Criterios de aceptación
- Datos faltantes
- Aprobación humana
- Área responsable
- Logs

## 👤 Human-in-the-loop (HITL)

Antes de ejecutar la comunicación final, ReqFlow AI incorpora una instancia de validación humana.

Telegram envía al responsable una solicitud con dos alternativas:

- ✅ Aprobar
- ❌ Rechazar

La decisión se procesa nuevamente en Make y determina la ruta que continuará el requerimiento.

Este mecanismo evita que una decisión crítica dependa exclusivamente del modelo de IA.

## 🛡️ Seguridad y resiliencia

El escenario contempla:

- Error Handler sobre el procesamiento de IA.
- Reintentos automáticos ante fallas temporales.
- Directiva Break para ejecuciones incompletas.
- Rutas específicas para datos incompletos.
- Validación humana antes de acciones críticas.
- Uso de variables dinámicas.
- Minimización de datos.
- Credenciales administradas mediante las conexiones seguras de Make.
- Blueprint público sanitizado sin credenciales personales.

## 💰 Optimización de costos

GPT-5 mini fue seleccionado como modelo principal por su relación entre capacidad, velocidad y costo para tareas de clasificación, razonamiento y generación de estructuras JSON.

La documentación del proyecto incluye una matriz comparativa de modelos y alternativas de procesamiento para cargas masivas.

## 📊 Dashboard de Control

Airtable incluye un Dashboard de Control para monitorear:

- Total de requerimientos.
- Requerimientos por estado.
- Aprobados y rechazados.
- Datos incompletos.
- Prioridades.
- Indicadores operativos.
- Tasa de errores.

### 🔗 Enlaces

**Base de datos – Vista de solo lectura:**  
https://airtable.com/invite/l?inviteId=invPwJw6UFAfIzq0C&inviteToken=51e77cb30b753055f5977910fc37710f4a7126807bed7b5b04d270c72a8c6924&utm_medium=email&utm_source=product_team&utm_content=transactional-alerts  

**Dashboard de Control:**  
https://airtable.com/appdLt19ukvyXPqY5/pagJEjeJvkRvcmYqy 

## 🧪 Pruebas

El sistema fue probado mediante múltiples ejecuciones contemplando caminos felices e infelices, incluyendo:

- Requerimiento completo.
- Aprobación humana.
- Rechazo humano.
- Datos incompletos.
- Mensaje que no corresponde a un requerimiento.
- Manejo de errores.

## 🛠️ Stack tecnológico

| Categoría | Tecnología |
|---|---|
| Orquestación | Make |
| Inteligencia Artificial | OpenAI – GPT-5 mini |
| Base de datos | Airtable |
| HITL | Telegram Bot |
| Comunicación final | Gmail |
| Formato de intercambio | JSON |
| Documentación | PDF + GitHub |

## 📁 Contenido del repositorio

- `README.md` – Descripción general del proyecto.
- `ReqFlow_AI_Entrega_Final.pdf` – Documentación completa.
- `ReqFlow_AI_Blueprint_PUBLIC.json` – Blueprint sanitizado del escenario de Make.
- `evidencias/` – Capturas de funcionamiento del sistema.

## 🔐 Importante

Este repositorio no contiene API Keys, tokens, contraseñas ni credenciales privadas.

El Blueprint publicado fue sanitizado para proteger los datos asociados a las conexiones utilizadas durante el desarrollo.

## 🎓 Proyecto Final

Proyecto desarrollado como entrega final de la carrera **AI Automation – Coderhouse**.

**Proyecto:** ReqFlow AI  
**Tipo:** Ecosistema de Automatización IA Autónomo para Negocios  
**Alumna:** Sofia Lazzarin
