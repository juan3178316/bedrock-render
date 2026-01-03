# entity.h
the properties created in the files [entity.fragment](entity.fragment.h) and [entity.vertex](entity.vertex.h) are used for [entity.material](../materials/entity.material.json)

> [!IMPORTANT]
> idk if the `entity.fragment` and `entity.vertex` are programmed in C


get the property values defined in [entity.material](../materials/entity.material.json) like:

[`entity.fragment.h`](entity.fragment.h)
```C
#include "c/fragmentVersionCentroidUV.h"
#include "c/uniformEntityConstants.h"
#include "c/uniformShaderConstants.h"
#include "c/util.h"

#ifdef USE_OVERLAY
	varying highp vec4 overlayColor;
#endif

#ifdef GLINT
	varying vec2 layer1UV;
	varying vec2 layer2UV;
	varying vec4 tileLightColor;
	varying vec4 glintColor;
#endif

#ifdef USE_EMISSIVE
#ifdef USE_ONLY_EMISSIVE
#define NEEDS_DISCARD(C) (C.a == 0.0 || C.a == 1.0 )
#else
#define NEEDS_DISCARD(C)	(C.a + C.r + C.g + C.b == 0.0)
#endif
#else
#ifndef USE_COLOR_MASK
#define NEEDS_DISCARD(C)	(C.a < 0.5)
#else
#define NEEDS_DISCARD(C)	(C.a == 0.0)
#endif
#endif
// ...
```

[`entity.material.json`](../materials/entity.material.json)
```json
{
	"materials": {
		"version": "1.0.0",

		"entity_static": {
			"vertexShader": "shaders/entity.vertex.vsh",
			"vrGeometryShader": "shaders/entity.geometry",
			"fragmentShader": "shaders/entity.fragment.fsh",
			"vertexFields": [
				{ "field": "Position" },
				{ "field": "Normal" },
				{ "field": "UV0" }
			],
			"variants": [
				{
					"skinning": {
						"+defines": [ "USE_SKINNING" ],
						"vertexFields": [
							{ "field": "Position" },
							{ "field": "BoneId0" },
							{ "field": "Normal" },
							{ "field": "UV0" }
						]
					}
				},
				{
					"skinning_color": {
						"+defines": [ "USE_SKINNING", USE_OVERLAY ],
						"+states": [ "Blending" ],
						"vertexFields": [
							{ "field": "Position" },
							{ "field": "BoneId0" },
							{ "field": "Color" },
							{ "field": "Normal" },
							{ "field": "UV0" }
						]
					}
				},
				{
					"skinning_alphatest": {
						"+defines": [ "USE_SKINNING", "ALPHA_TEST" ],
						"+states": [ "DisableCulling" ],
						"vertexFields": [
							{ "field": "Position" },
							{ "field": "BoneId0" },
							{ "field": "Normal" },
							{ "field": "UV0" }
						]
					}
				}
			],
			"msaaSupport": "Both",
			"+samplerStates": [
				{
					"samplerIndex": 0,
					"textureFilter": "Point"
				}
			]
		},
// ...

		// The texture must be a tga and it uses the alpha channel for determining emissiveness
		"entity_emissive:entity": {
			"+defines": [ USE_EMISSIVE ]
		},
// ...
```
