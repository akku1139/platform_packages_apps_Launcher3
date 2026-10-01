# Launcher3 (BvLauncher UI Port)

Fork of [aosp-mirror-neo/platform_packages_apps_Launcher3](https://github.com/aosp-mirror-neo/platform_packages_apps_Launcher3) for developing a Launcher that matches the UI/appearance of **Blackview BvLauncher** (`com.blackview.launcher`, V3.0.0_20220226).

## Goal

Port / replicate the visual design of BvLauncher (an OEM-customized AOSP Launcher3 + Quickstep from the Android 12 era) onto this codebase:

- Colors (notification dots, accents, folder backgrounds, page indicators, dark/light variants)
- Background transparency / wallpaper show
- Blur effects
- Icon size, padding, spacing, dynamic grid metrics
- Folder corner radius / paddings
- Hotseat / page indicator layout
- Related theme attributes

## Recommended base

- Working branch: **`bv-launcher-ui`** (created from `main` of the upstream mirror)
- BvLauncher itself targets ~Android 12 (compileSdk 31, version dated 2022-02). The upstream `main` is significantly newer (contains Compose paths, etc.).
- For closer structural match to the original APK, consider resetting or cherry-picking from an Android 12 tag (e.g. `android-12.0.0_r*` / `android-platform-12.0.0_r*` equivalents) if available in history, or starting from a dedicated A12 Launcher3 snapshot. Current work proceeds on this branch and adapts resources/styles first.

## Key extracted values from BvLauncher APK (for reference)

### Critical colors
- `notification_dot_color`: `#FFFE4621`
- Brand accent / `color3478F6` / dialog button text: `#FF3478F6`
- `folder_background_dark`: `#FF464746` (matches classic AOSP)
- `page_indicator_active_color`: `#FFFFFFFF`
- `page_indicator_dark_active_color`: `#FF1E1E1E`
- `page_indicator_dark_inactive_color`: `#661E1E1E`
- `icon_background`: `#FFE0E0E0`

### Key dimens (dynamic grid / icons / folder)
- `default_icon_bitmap_size`: 56dp
- `dynamic_grid_icon_drawable_padding`: 8dp (land 7dp)
- `dynamic_grid_cell_padding_x`: 8dp
- `dynamic_grid_cell_layout_padding`: 5.5dp
- `dynamic_grid_cell_border_spacing`: 16dp
- `dynamic_grid_edge_margin` / left-right: 8dp
- `dynamic_grid_hotseat_bottom_padding`: 2dp
- `dynamic_grid_hotseat_top_padding`: 8dp
- `folder_cell_x_padding`: 9dp / `folder_cell_y_padding`: 6dp
- `folder_content_bg_corner`: 30dp
- `page_indicator_dot_size`: 9dp / gap: 17dp

Blur sizes: click shadow 4dp, medium outline 2dp, thin 1dp.

See conversation / analysis notes for full list (styles, night variants, left-screen cards, etc.).

## Development notes

1. Start by overriding `res/values/colors.xml`, `dimens.xml`, and relevant styles/themes (`LauncherTheme`, `BaseLauncherTheme`, etc.).
2. Keep wallpaper / translucent system bars behavior.
3. Blur, left-screen cards, hide-app, frozen-app are OEM additions and require additional code beyond pure resource matching.
4. Build as part of AOSP or adapt for standalone if needed (this tree is the platform package layout).

## Upstream

- Original mirror: https://github.com/aosp-mirror-neo/platform_packages_apps_Launcher3
- Official AOSP: https://android.googlesource.com/platform/packages/apps/Launcher3
