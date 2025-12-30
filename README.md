# Bedrock Render

this repository was created for investing about types of entities render in Minecraft bedrock.

when i refer to "types of entities render", i refer to this one:
```mermaid
---
title: My entity render
---
flowchart TB;
A[br:my_entity_render] -->|Creating my custom entity properties, like materials and render_controllers| B & C;
```

```json
{
	"format_version": "1.10.0",
	"minecraft:client_entity": {
		"description": {
			"identifier": "br:my_entity_render",
			"materials": {
				"default": "entity_alphatest"
			},
// ...
		}
	}
}
```

> [!NOTE]
> Comming soon add further information.
