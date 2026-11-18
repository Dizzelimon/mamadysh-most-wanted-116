# Mamadysh Most Wanted — Godot 4.3

Automatic Android ARM64 debug APK builds with GitHub Actions.

## Before building

Upload the **complete Godot 4.3 game project** to the repository root, preserving its original folders and including `project.godot`, scenes, scripts, textures and other source assets. Do not upload Godot executable or generated `.godot/` cache. Do not publish release signing secrets.

If the game already includes `export_presets.cfg` with important project-specific settings, merge these ARM64 options into it instead of blindly replacing it. This sample is for a normal GDScript project without custom Android plugins or C#.

## Build and download APK

Open [Actions](https://github.com/Dizzelimon/mamadysh-most-wanted-116/actions), pick **Android ARM64 APK (Godot 4.3)** and select **Run workflow**, or push a commit to `main`. After a successful build download the `mamadysh-most-wanted-android-arm64` artifact ZIP from the run page, then unzip it to get the debug APK. The debug signing key is generated anew per run and cannot be used for durable release updates.

The workflow intentionally fails until a real `project.godot` has been uploaded. The sample does not create a new empty game.

## Large sources

GitHub browser uploads have per-file size limits. Use GitHub Desktop or git with Git LFS for large binary assets. Standard Git rejects files larger than 100 MiB. Exclude generated caches and downloaded Godot export templates.
