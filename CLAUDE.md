# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This repo holds Home Assistant **automation blueprints** — reusable, parameterized automation templates written in HA's YAML blueprint format. There is no build/lint/test tooling; blueprints are validated by loading them into a running Home Assistant instance (via the MCP HA connection available in this environment) rather than by a CLI command.

## Structure

- `blueprints/` — all blueprint YAML files live here (flat, no subfolders per blueprint).
  - `blueprints/CLAUDE.md` — scoped instructions for this directory (see below); it applies automatically when editing files under `blueprints/`.
  - `blueprints/.claude/skills/ha-verify-entities/` — a skill for validating entity/service references against the live HA instance.

## Working with blueprint YAML

- Files start with a `# $schema:` comment line pointing to the community JSON schema (`hass-json-schema`) — keep this line when editing an existing blueprint or adding a new one, so editors get schema validation/autocomplete.
- Blueprint content (names, descriptions, input labels) is written in **Dutch** — match this when adding or editing inputs.
- Inputs are declared under `blueprint.input` and consumed via `!input <name>`; entity-typed inputs use `selector: entity: domain: <domain>` with a sensible `default:`.
- Notify targets are hardcoded service calls (e.g. `notify.mobile_app_iphone`), not `!input`-driven — the same physical recipient (e.g. Christine) is addressed with **different** service names across blueprints (`notify.mobile_app_iphone_van_christine` in `live_activity.yaml` vs `notify.mobile_app_iphone_christine` in `notificatie.yaml`). Don't assume these are interchangeable or "fix" one to match the other without checking the actual registered service in HA first.

## Verifying entities/services before finishing an edit

Any time you add or change an `entity_id`, a `person.*`/`light.*`/etc. reference, or a `notify.*`/service target in a blueprint, run the **`ha-verify-entities`** skill before reporting the change as done. It uses the live HA MCP connection (`GetLiveContext`) to confirm entities exist, but note its real limitations: it only sees entities exposed to Assist, and it cannot verify notify/service targets at all (those require checking Settings → Devices & services / Developer tools → Actions in HA directly). Always report per-reference status as one of: confirmed / not verifiable via MCP / not found — never claim something "doesn't exist" based solely on an unexposed-entity result.
