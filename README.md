# AI Agency — n8n Workflow Automation

Workspace de automatización para una agencia de IA. Contiene workflows de n8n, scripts de soporte y configuraciones de integración para servicios entregados a clientes.

## Estructura del Proyecto

```
Automatizacion/
├── workflows/
│   ├── lead-gen/          # Calificación y captación de leads
│   ├── content/           # Producción de contenido con IA
│   └── client-ops/        # Operaciones y onboarding de clientes
├── vps_agents/
│   └── youtube-hermes/    # Agente Hermes desplegado en VPS de Hostinger
├── n8n-skills/            # Skills personalizados para Claude Code + n8n
└── CLAUDE.md              # Instrucciones de contexto para Claude
```

## Qué se Automatiza

- **Onboarding de clientes** — Flujos de bienvenida, recopilación de datos, notificaciones
- **Generación de leads** — Calificación automática con IA, seguimiento por email
- **Producción de contenido** — Redacción, clasificación y publicación asistida por LLMs
- **Reportes** — Sincronización de datos y dashboards periódicos

## Integraciones Principales

| Servicio | Uso |
|---|---|
| OpenAI / Claude (Anthropic) | Generación de texto, clasificación, extracción |
| Google Sheets / Airtable | Almacenamiento de datos |
| Gmail / SMTP | Automatización de correos |
| Slack / Telegram | Notificaciones internas |
| Webhooks | Disparadores externos (formularios, Make, Zapier) |

## Convenciones de Workflows

- Un archivo `.json` por workflow, exportado directamente desde n8n
- Nombres descriptivos: `lead-qualification-ai.json`, `email-responder-gpt.json`
- Credenciales referenciadas por nombre, nunca hardcodeadas

## Agentes en VPS

El agente **Hermes** corre en un VPS de Hostinger (`srv1698088.hstgr.cloud`, puerto 4860). Documentación en [`vps_agents/youtube-hermes/`](vps_agents/youtube-hermes/).

## Skills de n8n para Claude Code

El directorio `n8n-skills/` contiene skills que potencian a Claude Code para trabajar con n8n:

- `n8n-code-javascript` — Código JS en nodos Code
- `n8n-expression-syntax` — Sintaxis de expresiones `{{ $json.field }}`
- `n8n-workflow-patterns` — Patrones arquitectónicos de workflows
- `n8n-node-configuration` — Configuración correcta de nodos por operación
- `n8n-mcp-tools-expert` — Uso eficiente de herramientas MCP de n8n

## Flujo de Trabajo con Claude

1. Describir el workflow o el error
2. Claude consulta documentación de n8n en tiempo real via skills y MCP
3. Se genera o depura el JSON del workflow listo para importar
4. Se valida con checklist de debugging antes de activar en producción

## Checklist de Debugging

1. Leer el error completo del nodo que falló
2. Revisar datos de entrada con "View output of previous node"
3. Verificar que las credenciales estén activas
4. Comprobar sintaxis de expresiones (`$json`, nombre de nodo correcto)
5. Probar nodos HTTP Request con trigger manual primero
6. Usar un nodo Set para loggear datos intermedios si es necesario
