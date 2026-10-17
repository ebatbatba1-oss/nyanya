---
name: character-image-prompt
description: Generate copy-ready English keyword-only image prompts with immediate Korean translations, seven ordered sections, consistent character identity across turns, and Danbooru-style tags.
---

# Character Image Prompt Generator

## Role and output contract
- Generate **text-only** image prompt scripts. Never generate an image unless the user explicitly changes this skill's output requirement.
- Output **all requested prompts at once**, each with an English keyword prompt immediately followed by its Korean keyword translation.
- Only output prompts and translations: no introductions, disclaimers, headings explaining omissions, character names, notes, or parenthetical explanations. Use fenced plain-text code blocks for easy copying, with English and Korean in separate blocks for each prompt. If the user wants a single copy block, follow that preference.
- Use **comma-separated keywords**, not prose sentences. Never use `/` as a separator; never use parentheses in the prompt. Do not add filler for unavailable or off-camera features.
- Keep the established character's visual identity **unchanged** until the user explicitly provides a new character or explicitly requests an alteration. New clothing, poses, scenes, or expressions do not reset identity. If the current conversation has no established character, obtain essential identity details from the request, or ask one concise question if absolutely necessary. Do not pretend to remember a character from an inaccessible session.
- Character names must never appear in the prompt. Do not use named-character tags as examples for actual output.

## Character continuity
Maintain the following persistent-in-conversation character profile when known: sex/gender presentation, species and species traits, hair colors and multicolor technique, length/cut/bangs, eye color, eye shape, pupil color and shape when specified, skin tone, build, distinguishing facial marks, tattoos and accessories with exact positions. Preserve each fixed detail across prompts unless the user changes it. Do not confuse eye color with pupil color.

## Mandatory elements and visibility
For every prompt, cover the following when visible and applicable: intended mood and narrative; hair color, style, length and neatness; eye color, eye shape and gaze; build and skin tone; species traits when applicable; situational clothing; lighting; visual effects and accent colors; props and symbolic objects; setting consistent with the world, time of day and weather. **Camera visibility takes priority:** omit legs, shoes, lower-body clothing, or other invisible details in a face or bust crop; do not mention their absence. For a background-only request, use `no humans` rather than character attributes.

## Seven-part order for every SFW prompt
Build one continuous comma-separated tag sequence in the following order. Do not label sections in the final prompt.
1. Basic information and gaze: e.g. `1male, solo, looking at viewer`.
2. Job, species, situation: e.g. `knight, elf, waiting`.
3. Action, posture, emotion: e.g. `standing, holding sword, expressionless`.
4. Physical appearance: face, eye shape and eye color, pupil attributes if specified, hair color/length/cut/bangs, skin, build and condition. **For male characters always include `manly, mature male`**, even if `bishounen` is also used.
5. Clothes: visible layers, material, colors, fit and construction.
6. Accessories, props, symbolic objects, footwear: list from head to toe where visible, shoes last in this section.
7. Setting and finish: **begin this section with exactly one of `indoor`, `outdoor`, `scenery`**, include an explicit time tag such as `morning`, `afternoon`, `evening`, or `night`, then specific setting details, weather when appropriate, lighting, camera framing/angle and accent colors. The spatial tag must be the first tag of section seven, not necessarily the first tag of the entire prompt.

## Tag composition rules
- Prefer short Danbooru-style English tags. Always consult `references/나이태그 정리 조정.txt` first for matching tags, retaining its original category groupings. If the file has no suitable tag, prefer verified Danbooru tags with 100+ posts when lookup is available. Do not invent Danbooru verification results. Never claim a tag's post count was verified without access. If no suitable established tag exists, use a clear short descriptive keyword.
- Use literal colors (`light purple hair`, `dark blue eyes`, etc.), not metaphorical color descriptions. Useful modifiers: `pale`, `ash`, `vivid`, `neon`, `pastel colors`. Avoid changing skin color inadvertently with `pale`.
- For multicolored hair, specify the component colors and **exactly one** relevant method tag from `gradient`, `rainbow`, `split-color hair`, `striped hair`, `colored tips`, `colored inner hair` unless the user explicitly asks for more than one dye technique. Example: `black hair, red hair, colored tips`.
- Optional material/effect tags when appropriate: `iridescent hair`, `liquid hair`, `translucent hair`.
- Specify colored objects as color + noun, e.g. `white glasses`. Give fixed-position tattoos and accessories explicit locations, e.g. `barcode tattoo on upper right buttock` when visible.
- Hair: combine length `short hair` / `medium hair` / `long hair`, cut such as `pixie cut`, `undercut`, `wolf cut`, `hair slicked back`, and bangs such as `crossed bangs`, `hair over one eye`, `parted bangs`, `curtained hair` when appropriate. Optional `heart-shaped ahoge`.
- Eyes: `tareme`, `tsurime`, `sanpaku`, `half-closed eyes`; optional `glowing eyes`, `heterochromia`, `slit pupils`, `symbol-shaped pupils`, `crazy eyes`, `heart-shaped pupils`. For **eye color** use `blue eyes`, not `blue pupils`. Use `blue pupils` only when pupil color is specifically intended.
- Male appearance tags when appropriate: `bishounen`, `muscular`, `toned`, `broad shoulders` alongside mandatory `manly, mature male`.
- Situation-matched clothing and actions may include `business suit`, `loose necktie`, `adjusting necktie`, `black leather jacket`, `cardigan`, `hoodie`, `dog tag`, `shoulder holster`, `adjusting eyewear`.

## Weights
- Use sparingly, only for important fixed attributes or to overcome weak color rendering. Format `N::tag::`, e.g. `3::tsurime::`, `2::red hair::`, where positive N is at most 5 and fractional values such as `0.5` are allowed.
- Negative weights format `-N::tag::`, e.g. `-3::tsurime::`, magnitude at most 5; only use if necessary to suppress confusion.
- For multiple prompts depicting the same character, use **consistent weights for the same fixed tags across all prompts**. Do not add weights gratuitously. Weights count as tag wrappers, not parentheses.

## Internal validation before responding
- Exactly seven logical parts, correct order, with section seven starting with the spatial tag and including time.
- English prompt followed immediately by Korean keyword translation for each prompt.
- All visible mandatory details included; off-camera elements excluded.
- Character identity preserved; no character names.
- No prose, `/` separators, parentheses, or omission notes.
- No unverified claim about tag popularity.
- All requested variations returned together.

## Bundled tag reference
- `references/나이태그 정리 조정.txt` is the user-provided primary tag dictionary, organized into seven major numbered groups covering composition, actions, appearance, hair, body, clothing, and background/props.
- Use the dictionary as a candidate vocabulary, not as instructions to insert every listed tag. Select only relevant, visually consistent tags and preserve user-specified identity.
- Some entries in the reference contain parenthetical clarifications or inconsistent spelling; follow the output contract by omitting parentheses and using clean, meaningful tags.
