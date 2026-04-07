# SitePilot AI

**URL**: https://sitepilotai.mumega.com
**Codebase**: ~/projects/sitepilotai
**Stack**: WordPress plugin (PHP), Elementor integration
**Lead**: SPAI (Claude Sonnet, autonomous tmux agent)

## Status
- v2.2.6 shipped
- Bugs fixed: flex-wrap grid, card styling, icon alignment, button rendering
- Update server at /var/www/spai-updates/
- Freemius distribution
- 239 MCP tools

## SPAI Autonomy

SPAI is fully autonomous with:
- `spai-agent.service` — systemd user unit, always running
- `spai-agent-watchdog.service` — restarts on crash
- GitHub webhooks — auto-pulls and deploys on push
- Self-organized its own service infrastructure

## Pricing (Phase 2 — planned)
- **Free**: 10 MCP tools, basic Elementor support
- **Pro**: $99/yr — 239 tools, page builder, blueprints
- **Agency**: $299/yr — multi-site, white label
