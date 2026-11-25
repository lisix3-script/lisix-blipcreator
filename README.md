# lisix-blips

In-game blip manager for FiveM with a clean dark/orange UI.
Create, edit, hide and delete map blips without touching a single config file or restarting the server.


**[English](#english) · [Hrvatski](#hrvatski)**

---

## English

### Features
- Full in-game UI: search, filter (all / visible / hidden), sort (name / ID / last updated)
- Icon picker with all **883 GTA V blip sprites** (live previews) and searchable by name or number
- 86 blip colours, scale slider, short-range and hidden toggles
- "My position" button, set waypoint, teleport to blip
- Live sync: every change is pushed to all players instantly, no restart needed
- Storage: **oxmysql** (auto-creates the table) or a plain **JSON file** when no database is available
- Framework-free: works standalone, with **ESX** or **QBCore** groups, or via **ACE** permissions
- Locales: **Croatian** and **English** (add your own in `locales/`)
- Server exports for other resources

### Requirements
- FiveM server (any recent artifact)
- Optional: `oxmysql` for database storage
- Optional: `es_extended` or `qb-core` for group permissions

### Installation
1. Put the `lisix-blips` folder into your `resources` directory.
2. Add `ensure lisix-blips` to `server.cfg` (after `oxmysql` / your framework if you use them).
3. Give yourself permission, either:
   - ACE: `add_ace group.admin lisixblips.admin allow`
   - or be in one of the groups from `Config.Permission.Groups` (ESX / QBCore).
4. In game: `/blips`

### Configuration (`config.lua`)
| Option | Default | Description |
|---|---|---|
| `Config.Locale` | `'hr'` | `'hr'` or `'en'` |
| `Config.Command` | `'blips'` | Command that opens the manager |
| `Config.Permission.Ace` | `'lisixblips.admin'` | ACE permission name |
| `Config.Permission.Groups` | `admin, superadmin, god` | ESX / QBCore groups |
| `Config.Storage` | `'auto'` | `'auto'`, `'mysql'` or `'json'` |
| `Config.MaxBlips` | `500` | Maximum number of blips |
| `Config.Teleport` | `true` | Show the teleport button |
| `Config.Defaults` | | Sprite, colour, scale and short-range for new blips |
| `Config.SpriteUrl` | FiveM docs CDN | Where icon previews are loaded from |

### Exports (server)
```lua
local id = exports['lisix-blips']:AddBlip({ name = 'Shop', sprite = 52, color = 2, scale = 0.8, shortRange = true, x = 25.7, y = -1347.3, z = 29.5 })
exports['lisix-blips']:UpdateBlip(id, { color = 5, hidden = false })
exports['lisix-blips']:RemoveBlip(id)
local all = exports['lisix-blips']:GetBlips()
```

### Notes
- Icon previews are loaded from the FiveM documentation CDN. If an image cannot load, the sprite number is shown instead; the in-game blip is not affected.
- Colour swatches are a close preview of the in-game HUD colours.
- JSON storage writes to `data/blips.json` (ignored by git).

---<img width="221" height="526" alt="image" src="https://github.com/user-attachments/assets/4d8405da-fbec-4e0f-90eb-95a22db4e99f" />
<img width="843" height="526" alt="image" src="https://github.com/user-attachments/assets/4d893256-b4a9-4502-9a87-9ab03a2ad4a9" />
