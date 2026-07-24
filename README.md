# Modding System (Experimental)

The Modding System lets your players customize your game by loading external mod files — textures, 3D models, and configuration data — that your game can download and apply at runtime. It also allows you to run JavaScript code directly on objects from events.

> ⚠️ **This extension is experimental.** Enable testing/debug mode when working in the editor.

---

## What it provides

| Type | Internal name | Purpose |
|------|--------------|---------|
| **Object** | `ModdingSystem::CodeObject2d` | A 2D object that can execute JavaScript code, create objects with custom textures, and load external assets. |
| **Behavior** | Moddable object (experimental) | Attach this to any sprite/3D model to make it moddable — it can run mod-specific JavaScript and respond to mod file loads. |

---

## Global actions

| Action | What it does |
|--------|-------------|
| **APIKey** | Set your ModAPI key before downloading mods. |
| **ChangeModel3D** | Replace a 3D object's model with an external model resource. |
| **Delete** | Delete all mod files loaded in a group. |
| **Download** | Download a mod file from a given file path / URL. |
| **DownloadInterface** | Opens the mod download interface for the player. Enable testing mode in the editor. |
| **ErrorOrSignal** | Send an error or signal (used internally by the modding workflow). |
| **Load** | Load mod files from a file path into a scene variable and group. |
| **ProgrammingLanguage** | Choose the language the mod is written in: `"Java"`, `"C++"`, `"JavaScript"`, or `"Python"`. |
| **Save** | Save the current modded state into a group. |

## Global conditions

| Condition | What it checks |
|-----------|---------------|
| **IsAPIKey** | Returns true if the API key has been set. |
| **IsCode** | Returns true if the provided JavaScript code string is valid (syntax check). |

## Global expressions

| Expression | What it does |
|-----------|-------------|
| **Quotes(text)** | Wraps a string in quotes, useful when building code strings for Is code correct. |

---

## Object: `CodeObject2d`

### Actions

| Action | What it does |
|--------|-------------|
| **CreateObjectAndTexture** | Creates a new instance at a position with a custom texture image, plus width, height, and angle. |
| **CustomObject** | Mark this object as a custom/modded object (`has_object`: yes/no). |
| **RunCode** | Execute JavaScript on the object. Enable testing mode in the editor. |

### Conditions

| Condition | What it checks |
|-----------|---------------|
| **CheckCustomObject** | Returns true if the object is flagged as a custom/modded object. |

---

## Behavior: Run code (experimental)

### Actions

| Action | What it does |
|--------|-------------|
| **RunCode** | Execute JavaScript code in the context of this moddable object. Enable debug mode in the editor. |

### Properties

| Property | Type | Description |
|----------|------|-------------|
| **Var** | Number | Metadata value for the moddable object. |

---

## Important notes

- **Mod files must follow the naming and format rules** defined in your game's modding guide. See the modding resources site for more details.
- **Many actions require empty placeholder arguments.** Some parameter slots must remain empty, the extension handles them internally.
- **Always enable testing/debug mode** when authoring mod logic in the editor. Disable these flags in production builds.
- Add the Run code (experimental) behavior to sprites or 3D models that players can customize.
- `CodeObject2d` is the runtime bridge object, think of it as a canvas where custom code and textures are applied.
