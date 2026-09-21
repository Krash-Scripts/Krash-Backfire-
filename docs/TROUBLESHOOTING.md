# Troubleshooting

[← Back to overview](../README.md) · [Installation guide](INSTALLATION.md)

| Problem | Check |
| :--- | :--- |
| Tablet item disappears after use | The `backfire_tablet` definition must have `consume = 0`. Restart `ox_inventory` after editing the item definition. |
| Tablet item does nothing / export not found | Ensure the folder is named `k_backfire` and the inventory item uses `export = 'k_backfire.openTablet'`, not `kr_backfire.openTablet`. |
| Tablet will not open in a vehicle | Enter an eligible vehicle as the driver and stop. Review blocked vehicle classes and models. |
| Vehicle owner is rejected | Check `Config.OwnedVehicles`, registration plate matching and the ESX owner identifier. |
| Purchase fails or charges incorrectly | Check ESX account selection, configured prices and whether the player has enough money. Inspect console errors. |
| SQL errors / missing columns | Import `sql/install.sql` and check the MySQL connection. Back up the database before manual changes. |
| No flames or unexpected flame colors | Confirm `kr_backfire_fx` is running, its compatible particle assets are present and older particle packs do not conflict. |
| Missing engine sound or silent vehicle | Check that `Audio_Pack` is started and actually contains the selected engine sound bank. Catalog entries alone do not supply audio files. |
| No backfire audio | Check `k_backfire/web/sounds/`, audio settings, player distance and vehicle volume. |
| Backfire is not firing | Confirm that the vehicle has an installation, its power switch is ON, the engine is running and RPM/profile conditions are met. |
| Vehicle radio changes during effects | Confirm your build includes the radio fix, test with radio OFF and ON, and check for other scripts changing the radio or engine audio. |
| Tablet layout is cut off | Test NUI at 1280×720 and 1920×1080, and confirm the installed UI matches the script version. |

## Report a reproducible bug

[Open a GitHub issue](https://github.com/Krash-Scripts/Krash-Backfire-/issues/new/choose) with your FiveM artifact version, resource versions, client/server console output, reproduction steps, vehicle model and the result you expected. Add screenshots or a short recording when they help.

**Security:** redact private identifiers, tokens, server license keys, database connection strings and passwords from public logs.

[← Back to overview](../README.md)
