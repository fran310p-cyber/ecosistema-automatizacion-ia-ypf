# Ecosistema de Automatización IA para Consultas Comerciales
## Proyecto Final – Arquitecto de Flujos IA

**Autor:** Francisco Ponce de León

---

# Descripción

Este proyecto implementa un ecosistema de automatización inteligente para una distribuidora de productos YPF.

El objetivo es automatizar la atención de consultas comerciales utilizando Inteligencia Artificial, una base de datos centralizada y un flujo orquestado en n8n.

El sistema recibe una consulta del usuario, obtiene la información correspondiente desde Airtable, genera una respuesta comercial mediante un modelo LLM (Groq - Llama 3.3 70B) y detiene el proceso para una validación humana antes de la acción final.

---

# Caso de Uso

Una distribuidora comercial recibe diariamente consultas relacionadas con precios de productos.

Tradicionalmente estas consultas requieren que un vendedor consulte listas de precios actualizadas y responda manualmente.

La solución desarrollada automatiza este proceso permitiendo:

- Interpretar consultas en lenguaje natural.
- Buscar automáticamente el producto solicitado.
- Obtener el precio actualizado desde Airtable.
- Generar una respuesta comercial mediante IA.
- Incorporar un punto de aprobación humana (Human in the Loop).
- Preparar la integración con un canal de salida mediante Gmail.

---

# Tecnologías utilizadas

| Tecnología | Función |
|------------|----------|
| Docker | Infraestructura local |
| n8n | Orquestador principal |
| Airtable | Base de datos |
| Groq (Llama 3.3 70B Versatile) | Motor de Inteligencia Artificial |
| Gmail | Canal de salida previsto |

---

# Arquitectura

```

Usuario

↓

Chat Trigger

↓

Search Records (Airtable)

↓

Cadena Básica de LLM

↓

Modelo Groq

↓

Wait (Formulario de aprobación)

↓

Canal de salida (Gmail)

```

---

# Human in the Loop

Con el objetivo de evitar respuestas automáticas no supervisadas, el flujo incorpora un nodo **Wait** configurado mediante un formulario de aprobación.

La ejecución se detiene hasta recibir la validación de un operador humano antes de continuar con la acción final.

Este mecanismo permite incorporar control humano sobre respuestas generadas por Inteligencia Artificial.

---

# Manejo de Errores

La arquitectura incorpora un **Error Trigger** conectado a una rama específica de tratamiento de errores.

Ante una excepción, el flujo genera una estructura normalizada con:

- Estado
- Origen
- Mensaje de error

Esta estrategia facilita futuras integraciones con sistemas de monitoreo o registro de incidentes.

---

# Variables dinámicas

El sistema utiliza variables dinámicas provenientes de Airtable para construir el prompt enviado al modelo de IA.

Ejemplo:

- Código
- Producto
- Precio

Esto permite evitar información hardcodeada y mantener la solución escalable.

---

# Archivos incluidos

- workflow.json
- README.md
- Arquitectura.pdf
- Capturas del flujo
- Evidencias de Airtable

---

# Mejoras futuras

- Integración completa con Gmail mediante OAuth2.
- Registro automático de errores en Airtable.
- Envío automático de la URL de aprobación generada por el nodo Wait.
- Incorporación de múltiples listas de precios.
- Gestión de clientes y vendedores.

---

# Conclusión

La solución desarrollada integra una base de datos dinámica, un motor de Inteligencia Artificial y un flujo de automatización completo utilizando n8n.

El proyecto demuestra una arquitectura escalable preparada para incorporar nuevos canales de comunicación y nuevas automatizaciones comerciales.
## Base de datos Airtable

Enlace (modo lectura):
https://https://airtable.com/invite/l?inviteId=invJTuJwTEZT66DsC&inviteToken=393b2f64f42023c964c86f619849015b58a4db24bd5dcd0de8baf1537e041c3c&utm_medium=email&utm_source=product_team&utm_content=transactional-alerts