# BvLauncher UI Reference (from APK analysis)

Source APK: DKLauncher.apk / BvLauncher  
Package: `com.blackview.launcher`  
Version: V3.0.0_20220226 (versionCode 300220226)  
compileSdk / platform: 31 (Android 12), targetSdk 29, minSdk 31

Base is AOSP Launcher3 + Quickstep with significant OEM extensions (left-screen cards, blur controller, hide/frozen apps, hybrid hotseat, spring widgets, etc.).

## Colors (priority for matching)

### Must-change / distinctive
| Name | Value | Notes |
|------|-------|-------|
| notification_dot_color | #FFFE4621 | Strong orange-red (AOSP is usually system/gray) |
| color3478F6 / dialog_button_text_color | #FF3478F6 | Brand blue accent |
| page_indicator_active_color | #FFFFFFFF | |
| page_indicator_dark_active_color | #FF1E1E1E | |
| page_indicator_dark_inactive_color | #661E1E1E | |
| page_indicator_inactive_color | #66FFFFFF | |

### Matches classic AOSP (keep or verify)
| Name | Value |
|------|-------|
| folder_background_dark | #FF464746 |
| icon_background | #FFE0E0E0 |
| popup_shade_first_light | #FFF9F9F9 |

Many other colors reference system attrs or have night variants (`color-night`, `values-night` / v31). `folder_background_light` and several popup/scrim colors use resource references or night XML.

Also present: `bv_weather_bg_*` gradients, `card_bg_color`, `recent_*` task colors, `apps_blur_cover_color`, `edit_mode_blur_cover_color`.

## Dimens (icons, grid, folder, indicator)

### Icon / dynamic grid
- `default_icon_bitmap_size`: **56dp**
- `dynamic_grid_icon_drawable_padding`: **8dp** (land: 7dp)
- `dynamic_grid_cell_padding_x`: **8dp**
- `dynamic_grid_cell_layout_padding`: **5.5dp**
- `dynamic_grid_cell_border_spacing`: **16dp**
- `dynamic_grid_edge_margin`: **8dp**
- `dynamic_grid_left_right_margin`: **8dp**
- `dynamic_grid_hotseat_bottom_padding`: **2dp**
- `dynamic_grid_hotseat_top_padding`: **8dp**
- `dynamic_grid_hotseat_side_padding`: **0dp** (land: 16dp)
- `dynamic_grid_hotseat_extra_vertical_size`: **10dp**
- `dynamic_grid_drop_target_size`: 54dp
- `dynamic_grid_min_spring_loaded_space`: 8dp

### Folder
- `folder_cell_x_padding`: 9dp
- `folder_cell_y_padding`: 6dp
- `folder_content_bg_corner`: **30dp** (noticeably round)
- `folder_content_padding_left_right`: 6dp
- `folder_content_padding_top`: 26dp
- `folder_name_text_size`: 20sp
- `folder_label_text_scale`: 1.14

### Page indicator
- `page_indicator_dot_size`: **9dp**
- `page_indicator_dot_gap`: **17dp**
- `workspace_page_indicator_height`: 24dp
- `workspace_page_indicator_line_height`: 1dp
- `workspace_page_indicator_overlap_workspace`: 0dp

### Blur
- `blur_size_click_shadow`: 4dp
- `blur_size_medium_outline`: 2dp
- `blur_size_thin_outline`: 1dp

## Theme / window behavior

`BaseLauncherTheme` (parent DeviceDefault.DayNight style):
- windowShowWallpaper = true
- windowBackground transparent / null
- status / navigation bar transparent, draws system bar backgrounds
- Standard LauncherTheme / Dark / DarkText / DarkMainColor variants exist and map workspace text, folder fill, etc.

## Code-level OEM pieces (beyond pure resources)

- `com.blackview.launcher.blur.BlurController` / BlurUtil
- Left screen: `com.blackview.leftscreen.*` (cards for weather, note, calendar, usetime; EditApp / CardStyle / CardManager activities)
- HideAppController, FrozenUtil, HotSeatController, hybridhotseat, LauncherMonitor
- Spring edge-effect widgets (`BvSpring*`)

Matching appearance for the home grid / folders / indicators / colors can start with resources + theme attrs. Full visual parity (especially left panel and blur) needs code ports.

## Suggested next steps on this branch

1. Overlay the priority colors into `res/values/colors.xml` (+ night).
2. Override the dynamic_grid_* / folder_* / page_indicator_* dimens.
3. Align `LauncherTheme` attributes (`workspaceTextColor`, `folderBackgroundColor`, `notificationDotColor`, `pageIndicatorDotColor`, etc.).
4. Verify wallpaper + system bar transparency.
5. Build and compare side-by-side with the original APK on a device/emulator.
6. Incrementally add blur / left-screen if desired.
