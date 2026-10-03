# OmniRoute Agent Skills

Este repositorio contiene habilidades de desarrollo adaptadas para OmniRoute Agent Skills. Cada skill es un archivo `SKILL.md` que enseña a los agentes cómo trabajar con tecnologías específicas.

## Skills Disponibles

| Skill | Categoría | Descripción |
|-------|-----------|-------------|
| **security-reviewer** | Seguridad | Revisión de vulnerabilidades, SAST, secrets scanning |
| **code-reviewer** | Calidad | Reviews de código estructuradas y accionables |
| **debugging-wizard** | Calidad | Debugging sistemático, root cause analysis |
| **playwright-expert** | Testing | E2E testing, automatización de navegador |
| **typescript-pro** | Lenguaje | Type safety avanzada, generics, branded types |
| **kubernetes-specialist** | Infraestructura | Deployments, RBAC, networking, security |
| **nextjs-developer** | Framework | Next.js 14+, App Router, Server Components |
| **react-expert** | Framework | React 18+, hooks, Server Components, patterns |
| **python-pro** | Lenguaje | Python 3.11+, type hints, async, pytest |
| **devops-engineer** | DevOps | CI/CD, Docker, Kubernetes, IaC |
| **terraform-engineer** | Infraestructura | Terraform, módulos, state management |
| **mcp-developer** | API | MCP servers, tool handlers, JSON-RPC 2.0 |

## Estructura

```
skills/
├── security-reviewer/
│   └── SKILL.md
├── code-reviewer/
│   └── SKILL.md
├── debugging-wizard/
│   └── SKILL.md
├── playwright-expert/
│   └── SKILL.md
├── typescript-pro/
│   └── SKILL.md
├── kubernetes-specialist/
│   └── SKILL.md
├── nextjs-developer/
│   └── SKILL.md
├── react-expert/
│   └── SKILL.md
├── python-pro/
│   └── SKILL.md
├── devops-engineer/
│   └── SKILL.md
├── terraform-engineer/
│   └── SKILL.md
└── mcp-developer/
    └── SKILL.md
```

## Formato del Skill

Cada SKILL.md sigue el formato estándar de OmniRoute Agent Skills:

```yaml
---
id: skill-name
name: Skill Name
description: Descripción detallada...
category: security|quality|language|infrastructure|frontend|devops|api-architecture
area: specific-area
icon: material-icon-name
license: MIT
version: "1.0.0"
author: GitHub URL
domain: domain
triggers:
  - trigger1
  - trigger2
role: specialist|engineer|architect|expert
scope: implementation|review|analysis|testing
output-format: code|report|analysis|manifests|architecture|specification
related-skills:
  - related-skill-1
  - related-skill-2
---

# Skill Title

Contenido markdown...
```

## Uso con OmniRoute

Estos skills están diseñados para ser usados con OmniRoute Agent Skills. Para agregar este catálogo a tu instalación de OmniRoute:

1. Configura la URL del repositorio en los settings de Agent Skills
2. OmniRoute cargará automáticamente los skills disponibles
3. Los agentes podrán usar estos skills cuando detecten los triggers correspondientes

**Repositorio:** https://github.com/Cleomig/omni-route-skills

## Licencia

Todos los skills están licenciados bajo MIT License.

## Contribuir

Para agregar un nuevo skill:

1. Crea una carpeta con el nombre del skill en `skills/`
2. Agrega el archivo `SKILL.md` con el formato adecuado
3. Actualiza este README con el nuevo skill
4. Envía un pull request
