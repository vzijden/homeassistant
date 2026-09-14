---
name: create-home-assistant-automations
description: Creates and updates Home Assistant automations. When the users asks to generate, update or fix home assistant automations, blueprints or scripts.
---

# Create Home Assistant automations

## Instructions

### Home Assistant automation best practices
Automations should be easy to read and to debug. Try to apply the following best practices to ensure this:
* Automations should have seperate triggers per entity.
* Deep nesting of conditions should be avoided. 
* Geef condities een duidelijke omschrijving via een alias.  
* Gebruik logbook.log voor het omschrijven wat en waarom er iets gedaan is.
