# General Import Extensions

A collection of ThunderKit import extensions intended to be broadly useful to multiple games.

This is a stripped-down version of the excellent [RoR2ImportExtensions](https://github.com/risk-of-thunder/RoR2ImportExtensions) package with minor changes to support additional games.  If you are writing RoR2 mods, use `RoR2ImportExtensions` instead.

For using ThunderKit to mod Unity games without game-specific ThunderKit importers, this one provides generally useful assembly patching and data access tools.

| Extension Name | Priority | Effect | Recommended When |
|--|--|--|--|
|Assembly Publicizer|3.125M|Publicizes the listed assemblies with N-Strip, converting all `private`/`protected`/`internal` members to `public`.| High-performance private member access is needed, and potential increased breakage after game version updates is acceptable. |
|MMHook Generator|3.12M|Creates MMHook assemblies for the listed assemblies, allowing access to MonoMod.RuntimeDetour.HookGen API. | When using MonoMod.RuntimeDetour for patching |

## Using the publicizer

All assemblies accessing publicized members must have the `Allow 'unsafe' Code` option enabled in the `asmdef`, even if unsafe code blocks are not used. The runtime will throw exceptions such as `FieldAccessException` without it.

An option to disable NStrip's option to remove `readonly` keywords is added to this version.  This is added because Burst code can only access `static readonly` members, breaking compilation of [mods using Burst](https://docs.unity3d.com/Packages/com.unity.burst@1.8/manual/modding-support.html).
