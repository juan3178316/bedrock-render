# Bedrock Render
<details>
<summary>Table of contents (Click to show)</summary>

+ [Bedrock Render](#bedrock-render)
+ [Entity render Diagram](#entity-render-diagram)
+ [1. Entity Client Components](#1-entity-client-components)
</details>
this repository was created for investing about types of entities render in Minecraft bedrock.

when i refer to "types of entities render", i refer to this one:

> [!warning]
> Diagram only show on GitHub web :(
## Entity render Diagram
```mermaid
---
title: My entity render
---
flowchart TB;
A[br:my_entity_render] -->|Creating my custom entity properties, like materials and render_controllers| B[minecraft:entity_client];
B --> C(materials) & D(render_controllers);
D -->|You define what part of your GEO set the render type| E[e_render.render_controllers.json];
E ==> B;
C -->|You chose what type of render uses for your entity| F[Types of entity render];
G(entity.material);
F ==>|entity_custom| G;
F ==>|entity_alphatest| G;
F ==>|entity_emissive| G;
F ==>|entity_alphablend| G;
G -->|In entity.material exists more of entity render...| H(The material properties exists in shaders/entity.fragment and shaders/entity.vertex);

```

an example about the diagram:

## 1. Entity Client Components
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
			"render_controllers": [ "controller.render.my_entity_render" ],
		}
	}
}
```
in this JSON file define the entity client components like texturing, geometry, etc, but the important now is `materials` and `render_controllers`.

> [!NOTE]
> Comming soon add further information.
