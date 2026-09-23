<p align="center">
  <a href="https://typeshade.dev/">
    <img height="112" src="https://typeshade.dev/favicon.svg" alt="TypeShade">
  </a>
</p>

<h1 align="center"><a href="https://typeshade.dev/">TypeShade</a></h1>

<p align="center">
  <strong>Write shaders in TypeScript. Start with <code>"use typeshade"</code>.</strong><br>
  A shader language and compiler built around the TypeScript authoring experience.
</p>

<p align="center">
  <a href="https://typeshade.dev/guide/quick-start/">Quick start</a> ·
  <a href="https://typeshade.dev/guide/language/">Language guide</a> ·
  <a href="https://typeshade.dev/guide/examples/">Examples</a> ·
  <a href="https://typeshade.dev/api/">API reference</a>
</p>

## Start with a TypeScript file

TypeShade begins at the file boundary. Add `"use typeshade"`, then write shader code using a TypeScript-shaped authoring model:

```ts
"use typeshade"

class Camera {
  view: mat4
  pos: vec3
}

declare const camera: uniform<Camera>
declare let pixels: storage<array<f32>>

@compute([64, 1, 1])
export function paint(
  @builtin("global_invocation_id") gid: vec3u
) {
  const i = gid.x
  pixels[i] = pixels[i] + camera.pos.x
}
```

Builtins are explicit function inputs. TypeShade does not inject `gid`, `vid`, or `pid` as hidden globals, so a shader entry's interface is visible in its signature.

The language makes the GPU boundary explicit:

```text
TypeScript authoring
        ↓
  "use typeshade"
        ↓
 TypeShade semantics
        ↓
   shared IR
      ↙   ↘
   WGSL   GLSL ES 3.00
  WebGPU     WebGL2
```

There is no TypeShade runtime. The host application owns pipelines, resources and rendering; TypeShade owns the language and shader emission.

## Learn TypeShade

The documentation is organized around authoring first:

1. **Introduction** — understand the relationship between TypeScript and TypeShade.
2. **Quick start** — write your first `"use typeshade"` shader.
3. **Language guide** — learn types, functions, control flow, GPU types, resources and shader stages.
4. **Examples** — study complete shader programs and their generated targets.
5. **API reference** — look up compiler APIs once you know the language surface.

TypeScript is the starting point, not a second unrelated syntax to memorize. The guide explains which TypeScript concepts carry over and where TypeShade deliberately differs because GPU execution is constrained.

## Repositories

| Repository | Purpose |
| --- | --- |
| [`typeshade`](https://github.com/typeshade/typeshade) | TypeShade language and compiler implementation |
| [`typeshade.github.io`](https://github.com/typeshade/typeshade.github.io) | Documentation, examples, and site source |
| [`vscode-typeshade`](https://github.com/typeshade/vscode-typeshade) | Editor support: TypeScript server plugin and VS Code extension |
| [`.github`](https://github.com/typeshade/.github) | Organization profile and shared GitHub configuration |

## Status

TypeShade is pre-release. The public authoring model on `main` is file-level `"use typeshade"`; compiler internals and APIs may continue to evolve while the language surface matures.
