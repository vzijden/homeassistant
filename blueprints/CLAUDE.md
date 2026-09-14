# CLAUDE.md

Dit is een repository met Home Assistant blueprints (automations).

## Entities/services valideren

Gebruik bij het toevoegen of wijzigen van entity_ids of notify/service-targets in een blueprint of automation altijd de `ha-verify-entities` skill om te checken of ze echt bestaan via de live HA MCP-verbinding, voordat je de wijziging als klaar rapporteert.
