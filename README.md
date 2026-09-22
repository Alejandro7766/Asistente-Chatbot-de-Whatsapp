# Asistente Chatbot de WhatsApp:

Chatbot de atención al cliente por WhatsApp construido con n8n, la Meta Cloud API oficial y la API de Claude. Diseñado originalmente para el sector salud (clínicas), gestiona conversaciones con memoria de contexto y automatiza recordatorios de citas.

Descripción general:

Este proyecto automatiza la atención al cliente de un negocio a través de WhatsApp. Un usuario escribe un mensaje al número de WhatsApp Business del negocio, y el sistema responde de forma automática manteniendo el contexto de la conversación, apoyándose en la API de Claude para interpretar la intención del mensaje y generar una respuesta adecuada.

Además del chatbot conversacional, el repositorio incluye un segundo workflow independiente que envía recordatorios automáticos de citas 24 horas antes de la cita, consultando los datos desde una hoja de cálculo de Google Sheets.

Arquitectura:

El flujo principal funciona de la siguiente manera: el usuario envía un mensaje por WhatsApp, que llega a través del webhook oficial de la Meta Cloud API a una instancia de n8n. Dentro de n8n, el workflow gestiona el historial de la conversación, realiza una llamada a la API de Claude mediante un nodo HTTP Request, y envía la respuesta generada de vuelta al usuario a través de la propia Meta Cloud API.

El workflow de recordatorios funciona de forma separada: una tarea programada (cron) revisa diariamente la hoja de cálculo de citas y envía un aviso por WhatsApp 24h antes de la cita a los clientes con cita al día siguiente.

Stack técnico:

El proyecto está construido sobre n8n como orquestador de los workflows, desplegado en modalidad self-hosted mediante Docker en un servidor propio. La comunicación con WhatsApp se realiza a través de la Meta Cloud API, la vía oficial de WhatsApp Business Platform, en lugar de librerías no oficiales que pueden derivar en el bloqueo de la cuenta. El procesamiento de lenguaje natural y la generación de respuestas se apoya en la API de Claude (Anthropic). El almacenamiento de citas y datos de clientes se gestiona en Google Sheets.

Contenido del repositorio:

El archivo Asistente Demo Clinicas.json contiene el workflow principal del chatbot conversacional. El archivo Recordatorios de Citas 24h — Demo Clinicas.json contiene el workflow de recordatorios automáticos. Ambos son exports directos de n8n y pueden importarse en cualquier instancia desde la opción "Import from File" del editor.

Instalación y configuración:

Para poner en marcha este proyecto es necesario disponer de una instancia de n8n, ya sea self-hosted o en n8n Cloud. Una vez importados los archivos JSON de este repositorio, hay que configurar en n8n las credenciales propias necesarias: un token de acceso y el Phone Number ID de una app de WhatsApp Business para la Meta Cloud API, una API key de Anthropic para el nodo de Claude, y las credenciales OAuth junto con el ID de una hoja de cálculo propia para Google Sheets.

Ninguna credencial real forma parte de este repositorio. Los tokens, claves de API e identificadores de hojas de cálculo con datos de clientes se gestionan a través del sistema de credenciales cifradas de n8n, que no se incluye al exportar un workflow.

Aspectos a destacar:

Este proyecto utiliza la API oficial de Meta para WhatsApp Business, evitando soluciones no oficiales que pueden comprometer la cuenta del cliente. Incorpora gestión de memoria conversacional para mantener coherencia entre mensajes sucesivos, y separa la lógica en dos workflows independientes: uno conversacional y otro de automatización de recordatorios. El despliegue se realiza sobre infraestructura propia mediante Docker, sin depender de servicios de terceros de pago. Se trata además de un caso de uso aplicado a un cliente real del sector salud, no de un ejercicio teórico.

Estado

Proyecto en desarollo y funcional.
