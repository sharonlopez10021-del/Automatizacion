# AI Agency — n8n Workflow Automation

## Project Overview

This workspace contains n8n workflows for an AI agency. The goal is to build, debug, and optimize automation workflows that deliver AI-powered services to clients.

## What We Build Here

- n8n workflow JSON files (exported from n8n)
- Supporting scripts and utilities for workflow logic
- Documentation for each automation
- API integration configs (OpenAI, Claude, Google, Airtable, etc.)

## Workflow File Conventions

- Store exported workflows as `.json` files, one per workflow
- Name files descriptively: `lead-qualification-ai.json`, `email-responder-gpt.json`
- Group related workflows in subdirectories: `workflows/lead-gen/`, `workflows/content/`, `workflows/client-ops/`

## Available Resources

Claude has access to live n8n documentation via built-in skills and MCP tools. When building or debugging workflows, relevant n8n docs, node configurations, and templates can be looked up directly — no need to paste documentation manually.

## How to Help Me

When I ask for help with an n8n workflow:

1. **Building**: Describe the node sequence clearly. If generating JSON, output valid n8n workflow JSON that can be imported directly.
2. **Debugging**: Ask for the error message and the relevant node config. Identify whether the issue is in the node settings, expressions, or data mapping.
3. **Optimizing**: Look for redundant HTTP calls, improve error handling with Try/Catch branches, suggest batching where applicable.

## n8n Key Concepts (Context for Claude)

- Workflows are made of **nodes** connected by edges
- Data flows as **JSON arrays of items**: `[{ "json": { ... } }]`
- **Expressions** use `{{ $json.fieldName }}` or `{{ $node["NodeName"].json.field }}`
- **Credentials** are referenced by name, never hardcoded
- Common node types: Webhook, HTTP Request, Code, IF, Switch, Set, Merge, Loop Over Items, AI Agent, OpenAI, Anthropic
- The **Code node** runs JavaScript (Node.js); use it for data transformation
- **Error workflows** can be set globally in n8n settings

## Integrations Used

- OpenAI / Anthropic (Claude) — AI text generation, classification, extraction
- Google Sheets / Airtable — data storage
- Gmail / SMTP — email automation
- Slack / Telegram — notifications
- Webhooks — trigger workflows from external tools (Make, Zapier handoffs, web forms)

## Coding Style (Code Nodes)

- Use modern JavaScript (ES2020+)
- Return data as: `return items.map(item => ({ json: { ...item.json, newField: value } }))`
- Never mutate `item.json` directly without spreading
- Add try/catch inside Code nodes for graceful error handling

## Debugging Checklist

When a workflow fails:
1. Check the node that threw the error — read the full error message
2. Inspect the input data with "View output of previous node"
3. Verify credentials are active and not expired
4. Check expression syntax — missing `$json` or wrong node name reference
5. Test HTTP Request nodes with a manual trigger first
6. Use a Set node to log intermediate data if needed

## Project Goals

- Automate client onboarding, lead gen, content production, and reporting
- Build reusable workflow templates the agency can sell or replicate
- Keep workflows maintainable: one workflow = one clear responsibility
