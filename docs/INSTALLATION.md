# Installation guide

[← Back to overview](../README.md)

This guide describes the intended **ESX Legacy** installation of KR4SH Backfire. The repository currently contains a `k_backfire.zip` distribution archive; its extracted contents and any additional licensed asset packages must be checked before use. Do not assume the main archive includes every companion resource.

## 1. Server requirements

- ESX Legacy (`es_extended`), `ox_lib`, `ox_inventory` and `oxmysql` installed and started.
- A configured MySQL database and OneSync enabled.
- A compatible `kr_backfire_fx` resource for the particle effects.
- A compatible `Audio_Pack` resource if using the engine sound catalog.

This build is **not** a QBCore/Qbox/standalone integration. Verify the redistribution rights and required notices for third-party audio and particle assets before sharing a repack.

## 2. Extract the resources

[Download the archive](../k_backfire.zip), then verify the installation folders:

```text
resources/
├── k_backfire/       # main script and tuning tablet
├── kr_backfire_fx/   # compatible backfire particles
└── Audio_Pack/       # compatible engine audio
```

**Important:** these are three separate FiveM resources, not three directories to merge into `k_backfire`. The repository listing alone does not establish whether the ZIP contains both companion resources. Obtain them separately if they are absent and you have distribution/use rights. Preserve these folder names if you use the configuration and item example below.

Remove old, conflicting particle resources before switching to `kr_backfire_fx`, but keep your database data.

## 3. Import SQL

Import `k_backfire/sql/install.sql` from the extracted main resource into the database used by ESX. Back up existing tables before upgrading. An optional migration from an older `bbv_antilag` setup is not needed for a fresh installation.

## 4. Register the tablet item

Add this entry **inside the existing items table** in `ox_inventory/data/items.lua`:

```lua
['backfire_tablet'] = {
    label = 'Backfire Tablet',
    weight = 650,
    stack = false,
    close = true,
    consume = 0,
    description = 'Configure your vehicle backfire system.',
    client = {
        export = 'k_backfire.openTablet'
    }
},
```

Do not paste an additional top-level `return`. The item export must match the actual resource folder (`k_backfire`); the older string `kr_backfire.openTablet` is incorrect for this layout. `consume = 0` ensures that using the tablet does not remove it. Reload/restart `ox_inventory` after changing its item registration.

## 5. Start resources in order

Place the following after any mandatory framework initialization in `server.cfg`:

```cfg
ensure oxmysql
ensure ox_lib
ensure es_extended
ensure ox_inventory
ensure Audio_Pack
ensure kr_backfire_fx
ensure k_backfire
```

All three Backfire resources must exist and start successfully for the full configured experience. Consult your FiveM console for missing dependency errors.

## 6. Configure your server

Open `k_backfire/config.lua` and review at least:

| Setting | What to configure |
| --- | --- |
| `Config.ItemName` | Inventory item, normally `backfire_tablet`. |
| `Config.RequireTabletItem` | Require item possession for access/purchases. |
| `Config.PaymentAccount` | ESX bank or cash account. |
| `Config.InstallPrice` | First-time price in **in-game currency**. |
| `Config.OwnedVehicles` | Correct vehicle ownership table and column names for your garage. |
| `Config.RequireVehicleOwnerForPurchase` | Whether modifications require registered ownership. |
| `Config.BlockedVehicleClasses` / `Config.BlockedModels` | Vehicle eligibility. |
| `Config.EngineAudio` / `Config.ParticleFx` | Companion-resource names and behavior. |

Resource download price and in-game tuning prices are different things. Configuration changes may require restarting `k_backfire`.

## 7. Verify before opening to players

- [ ] Both companion resources start and required audio banks are present.
- [ ] The tablet item opens the interface and is **not consumed**.
- [ ] SQL installs without errors; purchased settings persist across a restart.
- [ ] The default ownership, driver, vehicle and payment checks work.
- [ ] Backfire profiles, flame color and size are visible to a nearby observer.
- [ ] The system's ON/OFF setting persists after a new purchase and a reconnect.
- [ ] Launch control works with your configured keybinds (default W + Space while nearly stationary).
- [ ] Vehicle radio stays on the selected station or OFF after repeated effects and engine-sound changes.
- [ ] Tablet layout works at 1920×1080 and 1280×720.
- [ ] You have confirmed redistribution rights/attribution before distributing third-party assets.

The above is a **test checklist**, not a claim that tests have been run on your server. Refer to [troubleshooting](TROUBLESHOOTING.md) if any check fails.

## Updating an existing installation

1. Back up the database and your existing resources, especially custom `config.lua` values.
2. Compare updated configuration options rather than overwriting local settings blindly.
3. Replace the main resource with a matching build, ensure companion assets are compatible and remove obsolete conflicting particle files.
4. Restart in the order above and repeat the verification checklist. **Do not delete the persistent vehicle table as an update step.**

[← Back to overview](../README.md)
