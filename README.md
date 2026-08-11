# Ecosistema de Automatización IA para Gestión de Leads Inmobiliarios

Proyecto Final – AI Automation  
Coderhouse

## Descripción

Este proyecto implementa un ecosistema de automatización para la recepción, clasificación y gestión de leads inmobiliarios.

El sistema recibe nuevos leads desde Google Sheets, valida los datos ingresados y utiliza Inteligencia Artificial para determinar su prioridad comercial. Posteriormente registra la información en Airtable y solicita la aprobación de un responsable comercial antes de contactar al potencial cliente.

La arquitectura incorpora mecanismos de validación, gestión de errores y Human-in-the-Loop (HITL) para evitar que una acción comercial crítica sea ejecutada únicamente por decisión de la IA.

## Tecnologías utilizadas

- **n8n:** orquestación del workflow.
- **Google Sheets:** fuente de entrada de nuevos leads.
- **Groq – Llama 3.1 8B Instant:** clasificación y análisis mediante IA.
- **Airtable:** base de datos, relaciones entre registros y dashboard de control.
- **Gmail:** aprobación humana y comunicación con el cliente.

## Flujo general

```text
Google Sheets
      ↓
Validación de datos
      ↓
Procesamiento individual
      ↓
Clasificación con IA
      ↓
Búsqueda del proyecto
      ↓
Registro en Airtable
      ↓
Solicitud de aprobación por Gmail
      ↓
Human-in-the-Loop
      ↓
  ┌─────────────┐
Aprobar      Rechazar
  ↓              ↓
Contactar      Actualizar
cliente         estado
  ↓
Actualizar estado
```

El sistema también incorpora rutas específicas para registrar datos incompletos y fallas durante el procesamiento de IA.

## Documentación

La documentación se encuentra organizada de acuerdo con los cinco criterios de evaluación del proyecto:

1. [Diagrama de Arquitectura](documentacion/01_Diagrama_Arquitectura_Sistema_Leads.pdf)
2. [Estructuras de Datos y Esquemas JSON](documentacion/02_Estructuras_de_Datos_y_Esquemas_JSON.pdf)
3. [Optimización de Costos](documentacion/03_Optimizacion_de_Costos.pdf)
4. [Seguridad y Resiliencia](documentacion/04_Seguridad_y_Resiliencia.pdf)
5. [Dashboard de Control](documentacion/05_Dashboard_de_Control.pdf)

## Dashboard de Control

El sistema cuenta con una interfaz desarrollada en Airtable para monitorear los leads procesados, sus estados, prioridades asignadas por IA y las excepciones detectadas durante la ejecución.

**Acceso en modo solo lectura:**
https://airtable.com/appy0np7Tx4kGzlQ3/shruikNDWnqzL7yPT

## Workflow n8n

El archivo JSON exportado del workflow se encuentra disponible en:

[Workflow – Gestión Inteligente de Leads](workflow/Workflow_Gestion_Leads_n8n.json)

Las credenciales y API Keys utilizadas por las integraciones no se encuentran incluidas en el archivo publicado.

## Evidencias

La carpeta [`evidencias`](evidencias/) contiene capturas del funcionamiento del sistema, incluyendo:

- Workflow completo en n8n.
- Entrada de leads desde Google Sheets.
- Registro de Leads en Airtable.
- Tabla vinculada de Proyectos.
- Dashboard de control.
- Control de errores.
- Solicitud de aprobación humana por Gmail.
- Comunicación automática al cliente luego de la aprobación.

## Pruebas realizadas

El sistema fue probado con múltiples leads y diferentes escenarios de ejecución.

Durante el test final se ingresaron **12 registros**:

- **11 leads** completaron el circuito válido.
- **1 registro** fue derivado automáticamente a la ruta de errores por ausencia de un dato obligatorio.

Esto permitió comprobar tanto el camino principal como el denominado **camino infeliz**.

El workflow también fue probado con decisiones humanas de aprobación y rechazo, verificando ambas ramas del Human-in-the-Loop.

## Seguridad y resiliencia

El flujo incorpora:

- Validación de campos obligatorios.
- Validación numérica del presupuesto.
- Procesamiento secuencial mediante `Loop Over Items`.
- Reintentos automáticos ante fallas de IA.
- Registro de excepciones en Airtable.
- Variables dinámicas sin datos comerciales hardcodeados.
- Credenciales administradas mediante n8n.
- Validación humana antes del contacto al cliente.

## Video Demo

Demostración del funcionamiento completo del sistema:

https://drive.google.com/file/d/1U8PEZBeIsD5yLfcrzPk3KG_loghJTPd9/view?usp=sharing

## Estructura del repositorio

```text
ecosistema-automatizacion-ia-leads/
│
├── README.md
│
├── documentacion/
│   ├── 01_Diagrama_Arquitectura_Sistema_Leads.pdf
│   ├── 02_Estructuras_de_Datos_y_Esquemas_JSON.pdf
│   ├── 03_Optimizacion_de_Costos.pdf
│   ├── 04_Seguridad_y_Resiliencia.pdf
│   └── 05_Dashboard_de_Control.pdf
│
├── workflow/
│   └── Clasificación Inteligente de Lead.json
│
└── evidencias/
    └── Capturas del funcionamiento del sistema
```

## Resultado

La solución integra entrada de datos, procesamiento mediante IA, persistencia estructurada, gestión de errores, aprobación humana y comunicación automática dentro de un único workflow orquestado en n8n.
