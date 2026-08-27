# Project Brief — sdd-starter

**Data:** 2026-08-26
**Versão:** 2.1

## 1. Objetivo

Skill pack de Spec-Driven Development: o agente invoca `sdd-mode` (standalone ou **de dentro do pstack** como camada de contrato), casa a intenção em `catalog.md` e gera `SDD/` com o processo do produto. Skill root é a pasta do host (`.cursor/.grok/.kiro/.agents/.agent/skills`).

## 2. Fora do MVP

- ❌ Plugin Cursor como artefato principal
- ❌ “The best spec is code” (spec em `SDD/` continua SSOT)
- ❌ sdd-mode mergear `main` sozinho
- ❌ Stack de referência obrigatória
- ❌ CI/scripts de bootstrap neste repo

Never-block no HOW é o perfil `agentic` (não está fora). Overnight land é playbook do pstack após G3, se o humano pediu (não é regra do sdd-mode).

## 3. Módulos

- **SDD_MODE**: roteador, playbooks, principles, geração de `SDD/`
