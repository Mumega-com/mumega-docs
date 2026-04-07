# Mumega Platform

**URL**: https://mumega.com
**GitHub**: https://github.com/Mumega-com
**Status**: Building, pre-revenue

## Overview

Mumega is an AI operating system for small businesses. The business model is community-first: $30/mo membership that gives access to AI tools, resources, and a peer community.

## Business Model

- **Community**: $30/mo membership (Skool-style)
- **Target**: 1000 members = $30K/mo
- **Funnel**: 3 free AI tools drive signups
- Tools are free. Community is the product.

## Pipeline

- GHL (GoHighLevel) handles CRM and sales pipeline
- Discord for community and agent collaboration
- MCP endpoint at mcp.mumega.com for agent connectivity

## Customer Onboarding

`POST /api/v1/customers/signup` — one API call provisions:
- Bus, mirror, and squad tokens
- Default squad with genesis task
- Customer directory
- MCP connection URLs (SSE + HTTP)

## Key Agents

- **Mizan** (Haiku, OpenClaw) — business agent, handles sales, pricing, proposals
- **Kasra** (Claude Opus/Sonnet) — platform builder
- **Codex** (GPT-5.4) — infrastructure

## Free Tools (Funnel)

3 free tools published to attract signups. Community membership unlocks full access.

## Partners

- PECB (Dessire Ruiz) — anchor partner
- Rippling (Mindy Tran)
- C21 Barrie (Matt Borland)
