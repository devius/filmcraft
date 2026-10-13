# Georgian interface

> **Last reviewed:** 2026-10-13 · **Last updated:** 2026-10-13 · **Change:** minor (Georgian catalog in sync with 0.7.2, 3,574 entries; terminology and scope written down) · **Target:** FilmCraft 0.7.2

Choose **Edit › Language › ქართული** (also Settings › General › Interface Language), or leave the
setting on System Language and use a Georgian system display language (`ka`, `ka-GE`,
`ka_GE.UTF-8`). The preference is `general.interfaceLanguage` with the value `ka`
(`prefs.set` over the control channel, or the `app.language.georgian` command); it is saved
with the other preferences and restored at startup. Project content (track and bin names, the demo
project), command ids, timecode, engine errors and CLI/MCP/control responses stay as they are.

`crates/ui-egui/src/i18n/ka.tsv` has every entry of the Spanish catalog plus the native macOS
Settings item (3,574 entries): menus, panels, tools, dialogs, settings, effect and transition
names and their parameters, presets, export formats and status messages. It is written from the
meaning of the English labels; no proprietary translation resources were consulted.

## Georgian script

- Mkhedruli, the script of the interface, has no letter case. Capitalising for chrome uses
  `i18n::ui_caps`, which leaves Georgian letters alone: Unicode uppercasing would turn them into
  Mtavruli, which is not used for interface text. The header's workspace name goes through it;
  the catalog contains no Mtavruli (a test checks this).
- The catalog has no plural forms, so counts are count-neutral: the noun comes first, then the
  number (`ელემენტი: {n}` for `{n} items`, `ფერის მართვა · ელემენტი: {n}`).
- The bundled Inter and JetBrains Mono have no Georgian letters, and craft-fonts has no Georgian
  face yet. `crates/ui-egui/src/georgian.rs` adds an installed system face as a fallback
  (SF Georgian, Sylfaen, Noto Sans Georgian, DejaVu Sans, Arial Unicode MS). Without one, which
  includes the web build, switching to Georgian is refused with a message and the interface stays in
  English, as for Chinese. A Georgian face in craft-fonts would make the web build work too.
- Numbers, timecode, frame rates and units keep their usual form (`48 kHz`, `24-bit`, `29.97`).

## Terminology

| Source | Georgian |
|---|---|
| File / Edit / Window | ფაილი / რედაქტირება / ფანჯარა |
| Save As… / Undo / Redo | შენახვა როგორც… / დაბრუნება / ხელახლა შესრულება |
| Cut / Paste | ამოჭრა / ჩასმა |
| Project / Bin | პროექტი / ბინი |
| Sequence / Nest… | სეკვენცია / ჩადგმა… |
| Timeline / Playhead | ტაიმლაინი / დაკვრის კურსორი |
| Clip / Marker | კლიპი / მარკერი |
| Mark In / Mark Out | შესვლის დასმა / გამოსვლის დასმა |
| Insert / Overwrite | ჩასმა / გადაწერა |
| Lift / Extract | აწევა / ამოღება |
| Add Edit | გაჭრა |
| Ripple Delete / Ripple Edit Tool | ძვრადი წაშლა / ძვრადი მონტაჟის ხელსაწყო |
| Rolling Edit Tool / Razor Tool | მცოცავი მონტაჟის ხელსაწყო / სამართებლის ხელსაწყო |
| Snap in Timeline | მიბმა ტაიმლაინზე |
| Speed/Duration… | სიჩქარე/ხანგრძლივობა… |
| Effects / Effect Controls | ეფექტები / ეფექტის მართვა |
| Video Transitions / Cross Dissolve / Fade | ვიდეოგადასვლები / ჯვარედინი გადადნობა / მიქრობა |
| Preset | პრესეტი |
| Audio Track Mixer / Mute / Volume | აუდიოტრეკების მიქშერი / დადუმება / ხმის დონე |
| Captions | სუბტიტრები |
| Workspaces / Appearance | სამუშაო სივრცეები / იერსახე |
| Render In to Out | რენდერი შესვლიდან გამოსვლამდე |
| Import / Export | იმპორტი / ექსპორტი |

Please follow this table (and the existing catalog) when adding strings. Commands use the verbal
noun (`შენახვა`, `ექსპორტი`), not the imperative; product and format names (FilmCraft, Lumetri,
ProRes, FLAC) stay as they are.

## Maintenance

Add a line `<TAB>English source<TAB>Georgian` to `ka.tsv` for every new `tl!` literal, menu label
or registry name (the Spanish entry is required anyway). Keep `{placeholders}`, a trailing `…`,
`\n` and shortcut text exactly. `cargo test -p filmcraft-ui-egui --lib i18n` checks Georgian with
the other catalogs: valid format and placeholders, every Spanish entry, `tl!` literal and menu label
translated, no entry without a Spanish one, no Mtavruli, locale matching (`ka`, `ka-GE`,
`ka_GE.UTF-8`), switching, saving and restoring `ka`, the refusal without a Georgian font, glyph
coverage with the installed fallback, and `ui_caps`. A native-speaker skim of the catalog is
welcome.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-13 | minor | Catalog in sync with 0.7.2 (3,574 entries); terminology, script notes and maintenance written down |
