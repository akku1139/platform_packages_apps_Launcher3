# Launcher3 (BvLauncher UI Port)

Fork of [aosp-mirror-neo/platform_packages_apps_Launcher3](https://github.com/aosp-mirror-neo/platform_packages_apps_Launcher3) aimed at matching **Blackview BvLauncher** (`com.blackview.launcher`, V3.0.0_20220226) appearance on an **Android 12 (S)** Launcher3 + Quickstep base.

## Branch

- **`bv-launcher-ui`** — primary development branch (Android 12–era tree + Bv UI changes)

## Implemented UI matching (resources + code)

### Colors (`res/values/colors.xml`)
| Resource | Value | Role |
|----------|-------|------|
| `notification_dot_color` / `notification_icon_default_color` | `#FFFE4621` | Fixed notification badge (Bv) |
| `bv_accent` / `dialog_button_text_color` | `#FF3478F6` | Brand blue |
| `folder_dot_color` | `@color/bv_accent` | Folder badge uses accent |
| `folder_background_dark` | `#464746` | Unchanged AOSP match |
| `page_indicator_*` | white / `#1E1E1E` variants | Page dots |

### Dimens (`res/values/dimens.xml`, `values-land`)
- Icon drawable padding **8dp** (land **7dp**)
- Hotseat extra vertical **10dp** (was 34dp)
- Page indicator dot **9dp**, gap **17dp**
- Folder content padding L/R **6dp**, top **26dp**, corner **30dp**
- `default_icon_bitmap_size` **56dp**

### Code
- `BubbleTextView`: notification dots use `R.color.notification_dot_color` instead of muted icon color (Bv fixed-color badges).

### Theme
- Existing `BaseLauncherTheme` / `LauncherTheme` already use wallpaper + transparent system bars (aligned with Bv).

See `docs/BV_LAUNCHER_UI_REFERENCE.md` for the full extraction notes from the original APK.

## Build

This is an **AOSP platform package**, not a fully standalone app.

```bash
# Inside an Android 12 AOSP tree, with this tree at packages/apps/Launcher3:
source build/envsetup.sh
lunch <your_target>
mma Launcher3QuickStep
```

Gradle files exist for partial IDE use but require `ANDROID_TOP` prebuilts (`iconloaderlib`, framework intermediates, optional `sysui_shared`).

## CI

GitHub Actions (`.github/workflows/build.yml`):
- Validates XML resources
- Asserts BvLauncher marker colors/dimens/code are present
- Documents the AOSP `mma` path for producing the APK

## Not yet ported (OEM extras beyond pure look)

- Left-screen cards (weather / note / calendar / usetime)
- `BlurController` and related blur cover colors
- Hide-app / frozen-app / hybrid hotseat controllers

Those need additional Java packages beyond resource theming.
