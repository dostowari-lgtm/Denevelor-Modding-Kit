# Denevelor-Modding-Kit
What this supports

Mods can be packaged as .pck files and mounted directly into the game at startup. A .pck mod can add or override anything — scenes, scripts, textures, audio, whole enemies/bosses, you name it — by matching the file path of whatever it's replacing.

This is separate from the JSON/script mod system (ModRegistry) — that one's for quick item/recipe/boss/enemy definitions via JSON + a script or orchestration file. PCK mods are for full content packs: new scenes, new assets, deeper overrides.

Supported scripting for mods

Any mod content can use:

GDScript (.gd)
Orchestrator visual scripts (.torch)

Both work identically once packaged — a scene inside a mounted .pck with either script type attached just runs, no special handling needed on our end. Orchestrator's plugin is baked into the base game itself, so any mod using it will work out of the box, no extra setup required by the modder.

Important limit: mods can only use plugins the base game already ships with (currently: Orchestrator). A mod can't bring its own brand-new native plugin/GDExtension inside a .pck — GDExtensions only load from the base game at boot, not from mounted packs.

Where mods go
Denevelor/ (next to the .exe)
└─ mods/
   └─ pcks/
      └─ YourMod.pck

Drop .pck files in mods/pcks/. They're mounted automatically on launch, in alphabetical order — later-loaded mods override earlier ones and the base game on any matching file path.

Making a mod
You need a Godot project with the Orchestrator plugin installed if you want to use it — use the stub kit (included in this repo) as your starting point. It contains the game's scene structures (node names/hierarchy) with no scripts or assets attached, so you can build content that matches our layout without needing our source.
Build your content — new scenes, overrides, whatever. To override an existing game file, your mod's file needs to live at the exact same res:// path as the one you're replacing.
Project → Export → Export PCK/ZIP (not the normal project export). Choose .pck as the output type.
Before exporting: make sure none of the stub kit's placeholder scenes are included in your export. They're structure-only references for building — if one gets bundled into your mod and mounted into the real game, it'll silently overwrite the real version and break things for anyone using your mod. Exclude the stub folder in your export preset's Resources filter.
Drop the resulting .pck into mods/pcks/.
Version matching

Your mod's .pck has to be exported from the same Godot engine version the base game uses. A mismatched version can fail to load, or worse, partially load and cause weird crashes. Current base game version: (fill in your Godot version here).
