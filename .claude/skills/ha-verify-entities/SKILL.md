---
name: ha-verify-entities
description: Verify that entity_ids, person./light./sensor./etc. references, and notify/service targets used in Home Assistant blueprints, automations, or scripts actually exist, using the live HA MCP connection. Use before finishing any edit to a blueprint/automation YAML file that references an entity_id or a notify/service target.
---

Voordat je een wijziging aan een HA blueprint/automation/script als klaar rapporteert, controleer de gebruikte entities:

1. **Verzamel referenties** uit het bestand: entity_ids (bv. `person.vincent`, `light.hal`), `!input` defaults die naar entity-selectors verwijzen, en service/action targets (bv. `notify.mobile_app_iphone`, `action: light.turn_on`).

2. **Check entities** via `mcp__HA__homeassistant__GetLiveContext`, gefilterd op `domain` en/of `name`. Vergelijk de teruggegeven namen/domains met wat het bestand gebruikt.

3. **Ken de beperking van deze tool**: `GetLiveContext` toont alleen entities die **exposed zijn aan Assist**. Een "No exposed entities matched" resultaat betekent dus NIET automatisch dat de entity niet bestaat — het kan ook gewoon niet aan Assist zijn blootgesteld. Rapporteer dit onderscheid expliciet, claim nooit hardhandig "bestaat niet" op basis van alleen dit resultaat.

4. **Services/notify targets kunnen niet via deze tool worden geverifieerd** (het zijn geen entities met state). Vermeld dit als "niet te verifiëren via MCP" in plaats van het te negeren of te laten doorgaan voor een check. Verwijs de gebruiker naar Instellingen → Apparaten & services, of Ontwikkelaarstools → Acties, om dit zelf te bevestigen.

5. **Rapporteer per referentie** een van drie statussen: bevestigd aanwezig / niet te verifiëren (buiten scope van deze tool) / niet gevonden (en dus vermoedelijk fout of hernoemd).

Doe dit proactief zodra je entity_ids of notify/service-namen in HA YAML-bestanden toevoegt of wijzigt — wacht niet tot de gebruiker er expliciet om vraagt.
