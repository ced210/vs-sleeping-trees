# Bare Branchy Winter

A Vintage Story content mod that makes the foliage on **Branchy** leaf blocks completely invisible during Winter, leaving only the bare branch mesh and bark texture visible.

---

## How to Test In-Game

### 1. Install the mod

1. Build or zip the mod folder so it contains:
   ```
   modinfo.json
   assets/
   patches/
   ```
2. Copy the resulting `.zip` (or the raw folder) into your Vintage Story **Mods** directory:
   - **Windows:** `%APPDATA%\VintagestoryData\Mods\`
   - **Linux / macOS:** `~/.config/VintagestoryData/Mods/`
3. Launch Vintage Story. On the main menu go to **Mods** and confirm `Bare Branchy Winter (barebranchy)` appears in the list and is enabled.

---

### 2. Create or open a world with Branchy trees

1. Start a new **Creative** world (or use an existing survival world).
2. Travel to a forest biome that contains **Branchy** tree variants — look for oak, maple, pine, or birch trees whose leaf blocks display the characteristic 3-D branch mesh.
3. Alternatively, use the creative inventory or the command `/give @p game:leaves-branchy-oak-free` to place some branchy leaf blocks directly.

---

### 3. Force the season to Winter

Because waiting for the in-game calendar to reach Winter can take a long time, use the server console to jump straight to it:

1. Open the **chat / command bar** (default: `T`).
2. Run:
   ```
   /time set calendar 0.9
   ```
   A value of `0.9` places the calendar deep in Winter (the year runs 0 → 1, and Winter spans roughly `0.85 – 1.0 / 0.0 – 0.15`).
3. Confirm the season with:
   ```
   /time
   ```
   The output should show the current season as **Winter**.

---

### 4. Observe the result

- **Expected:** The foliage (leaf) part of every Branchy leaf block is invisible — you can see the bare branch/bark mesh and look through the block.
- **Branches stay visible:** The 3-D branch geometry and its bark texture must still render. If the branches are also invisible, check that the patch's `foliage` texture slot is targeted correctly (not `wood` or `all`).
- **No black boxes:** If you see black or solid-coloured blocks instead of transparency, verify that `renderpass` is set to `"Transparent"` in the patch.
- **No X-ray holes:** If the branch mesh of neighbouring blocks disappears, verify that `faceCull` is set to `"Never"` in the patch.

---

### 5. Verify other seasons look normal

Set the calendar back to Spring or Summer and confirm the foliage re-appears with its normal colour:

```
/time set calendar 0.3
```

---

### Troubleshooting quick-reference

| Symptom | Likely cause | Fix |
|---|---|---|
| Leaves turn into black boxes | `renderpass` is not `Transparent` | Check the patch sets `"renderpass": "Transparent"` |
| Neighbouring branch mesh disappears | Face-culling is active | Check the patch sets `"faceCull": "Never"` |
| Branches also vanish in winter | Wrong texture slot patched | Ensure only the `foliage` slot maps to `survival:block/transparent`, not `wood` or `all` |
| Mod doesn't appear in the list | File structure incorrect | Confirm `modinfo.json` is at the root of the zip/folder |
| No visual change at all | Wrong season value or patch not applied | Run `/time` to confirm season; check game logs for patch errors |