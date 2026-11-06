# Unity UI Five

A Codex skill for building and maintaining Unity uGUI screens and prefabs. **Five** refers to Team Five.

The skill preserves each project's visual design while separating image-based content into editable UI controls. It provides layout, prefab reuse, and Editor workflow guidelines rather than a fixed theme or a ready-made UI package.

## Installation

Clone this repository into your Codex skills directory:

```sh
git clone https://github.com/Song-Sungyoub/unity-ui-five.git ~/.codex/skills/unity-ui-five
```

On Windows, the default directory is `%USERPROFILE%/.codex/skills`. If you use a custom Codex skills location, clone there instead. Preserve an existing installation before replacing it.

## Usage

Invoke the skill in a Codex request:

```text
Use $unity-ui-five to rebuild this mockup as editable Unity uGUI.
Preserve the project's fonts and design. Keep this task limited to UI.
```

The main instructions are in [SKILL.md](SKILL.md), currently written in Korean. The skill can also be selected automatically for matching UI tasks.

## UI guidelines

- Preserve project-specific fonts, colors, icons, spacing, and Canvas settings.
- Separate backgrounds, TMP text, and interactive controls instead of baking them into a single image.
- Prefer existing shared sprites and 9-slice images for scalable backgrounds.
- Use LayoutGroups and LayoutElements where they clarify layout ownership.
- Preserve serialized references and script-dependent hierarchy paths when modifying existing screens.
- Keep API, authentication, and business logic outside a UI-only task.

A typical panel uses this structure:

```text
Panel
├── Background
├── Title
│   └── Text
└── Content
```

Omit unnecessary containers for simple controls. This structure should help maintain the screen, not force a project-wide hierarchy rewrite.

## Prefab reuse

Reuse project-specific Button, InputField, Checkbox, and Toggle prefabs. Keep their backgrounds, labels, and icons as internal children.

For new composite elements such as cards and rows:

1. Lay out the UI using existing controls.
2. Show the screen and hierarchy.
3. Propose which elements should become prefabs, with their reuse and nesting implications.
4. Obtain approval or adjustments before extracting them.
5. Verify layout, references, overrides, and saved instances after extraction.

Avoid turning every object into a prefab or adding nesting without a maintenance benefit. Existing approval covers repeated use within the approved scope.

## Unity CLI and Pipeline

The preferred editing route is:

```text
Unity CLI → Unity Pipeline (com.unity.pipeline) → Editor API
```

Use the separate `unity-cli` skill when it is available. Check the connected Editor with `unity status`, specify the target using `--project-path`, and discover supported commands with `unity command` or `unity list`.

When an Editor is reachable, edit scenes, prefabs, and assets through Editor APIs rather than modifying their YAML directly. Diagnose connection failures, compile errors, and Safe Mode before considering a fallback. Installing tools or changing project configuration requires its own authorization when outside the approved scope.

Preserve unsaved work and the user's Play mode state. Save and reload affected assets, then distinguish visual inspection, Play mode checks, and actual input testing in the report.

## Included sprites

[assets/sprites](assets/sprites/) contains six PNG background shapes and their Unity `.meta` files:

- Rounded rectangle
- Refined rounded rectangle
- Refined horizontal rounded bar
- Refined upper-left corner shape
- Refined upper-right corner shape
- Refined bottom corner shape

Prefer the target project's existing assets. When importing these sprites, keep each PNG with its `.meta` file to preserve import settings. Check for existing GUIDs first to avoid duplicate assets.

These are background shapes, not a font collection or functional control library.

## Scope

This repository contains reusable UI guidance and supporting sprite assets. It does not include a Unity project, install Unity CLI or Pipeline automatically, or implement backend integration. Project-specific instructions and approval requirements still apply.
