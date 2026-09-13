<p align="center">
  <a href="https://typeshade.dev/">
    <img height="112" src="https://raw.githubusercontent.com/typeshade/.github/claude/ai-generated-feeling-ky0y7t/profile/favicon.svg" alt="TypeShade">
  </a>
</p>

<h1 align="center"><a href="https://typeshade.dev/">TypeShade</a></h1>

<p align="center">
  <strong>Write shaders in TypeScript. Start with <code>"use typeshade"</code>.</strong><br>
  TypeShade is a shader language and compiler built around the TypeScript authoring experience.
</p>

<p align="center">
  <a href="https://typeshade.dev/guide/quick-start/">Quick start</a> ·
  <a href="https://typeshade.dev/guide/authoring/">Language guide</a> ·
  <a href="https://typeshade.dev/guide/examples/">Examples</a> ·
  <a href="https://github.com/typeshade/typeshade">Compiler</a>
</p>

## The idea

A TypeShade file looks and feels like TypeScript, but the file-level directive opts it into TypeShade's shader semantics:

```ts
"use typeshade";

export function fragment(uv: vec2): vec4 {
  return vec4(uv, 0.0, 1.0);
}
```

The source is lowered to a shared intermediate representation and emitted as host-consumable shader code:

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

There is no TypeShade runtime. Your host application consumes the generated shader source.

## Learn TypeShade

The documentation is organized around the language first:

- **Why TypeShade** — understand the language boundary and why shader constraints belong in authoring.
- **Quick start** — create your first `"use typeshade"` shader.
- **Language guide** — learn types, functions, expressions, control flow, modules and GPU-specific semantics.
- **Examples** — see complete shader programs and their generated targets.
- **API reference** — look up compiler and public library APIs when you already know what you need.

TypeScript knowledge is a starting point, not a prerequisite to memorizing a second completely unrelated syntax. The guide calls out what stays familiar and where TypeShade deliberately differs because of the GPU execution model.

## Repositories

| Repository | Purpose |
| --- | --- |
| [`typeshade`](https://github.com/typeshade/typeshade) | TypeShade language and compiler implementation |
| [`typeshade.github.io`](https://github.com/typeshade/typeshade.github.io) | Documentation, examples, and site source |
| [`.github`](https://github.com/typeshade/.github) | Organization profile and shared GitHub configuration |

## Status

TypeShade is pre-release. The public authoring model on `main` is file-level `"use typeshade"`; package and compiler details may change while the language surface matures.
