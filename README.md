<p align="right">
  <a href="README-zh-CN.md">简体中文</a> | <b>English</b>
</p>

# foo_nowbar

<p align="center">
  <!-- 徽章组：版本 | 下载 | 支持 -->
  <a href="https://github.com/jame25/foo_nowbar/releases"><img src="https://img.shields.io/github/v/release/jame25/foo_nowbar?style=flat-square&label=Release&color=blue" alt="Latest Version"></a>
  <a href="https://github.com/jame25/foo_nowbar/releases"><img src="https://img.shields.io/github/downloads/jame25/foo_nowbar/total?style=flat-square&label=Downloads&color=success" alt="Total Downloads"></a>
  <a href="https://ko-fi.com/Jame25"><img src="https://img.shields.io/badge/Support%20me%20on-Ko--fi-FF5E5B?style=flat-square&logo=kofi&logoColor=white" alt="Support me on Ko-fi"></a>
</p>

A foobar2000 component that provides a "Now Playing" control panel for both Default UI and Columns UI.

<img width="1434" height="108" alt="nowbar" src="https://github.com/user-attachments/assets/bd1a04b9-9a9b-49ca-85c6-7e6bd7f722ee" />

### Core Features
- **Dual UI Support**: Works seamlessly with both Default UI (DUI) and Columns UI (CUI)
- **Album Artwork Display**: Shows album art with square/rounded corners and optional margin
- **Online Artwork**: Fetches artwork from online sources via [foo_artwork](https://github.com/jame25/foo_artwork) when local/embedded artwork is unavailable
- **Track Information**: Displays track info across up to 3 configurable display lines with customizable Title Formatting (default: Line 1 title, Line 2 artist, Line 3 optional format or rating stars); supports real-time dynamic updates for `%playback_time%`, `%bitrate%` (VBR), and external stream metadata
- **Selection Mode**: Switch between Prioritize Now Playing Mode (shows active playback, falls back to selected track when stopped) and Follow Selection (always follows the selected playlist item)
- **DPI Aware**: Properly scales on high-DPI displays with adaptive sizing and space compression

### Playback Controls
- **Play/Pause**: Central play button to toggle playback
- **Stop**: Optional stop button (hidden by default) - stops playback
- **Stop After Current**: Optional toggle button (hidden by default) - stops playback after the current track finishes; accent color when active
- **Previous/Next**: Navigate between tracks
- **Shuffle**: Toggle shuffle mode with visual indicator (accent color when active; bi-directionally synchronized with MiniPlayer)
- **Repeat**: Cycle through repeat modes: Off -> All -> Track (accent color when active; bi-directionally synchronized with MiniPlayer)
- **Seek Bar**: Interactive progress bar for seeking within tracks
  - Pill-shaped or rectangular style (configurable)
  - Elapsed and remaining time display
  - Hover tooltip showing timestamp at cursor position
  - In Spectrum mode, a thin progress bar at the top edge replaces the seekbar with hover enlargement and timestamp tooltip

### Volume Control
- **Volume Slider**: Click or drag to adjust volume (perceptual loudness mapping matching foobar2000's default curve)
- **Volume Number**: Optional inline numeric volume readout (0 when muted, 1-100) displayed directly next to the volume slider or icon; matches secondary font/color and replaces hover tooltip
- **Mute Toggle & Memory**: Click volume icon to mute/unmute; unmuting restores the exact previous volume level
- **Independent Visibility**: Volume icon and volume bar can be toggled independently (hiding the bar docks the icon to the right edge and reclaims panel width)
- **Mouse Wheel Support**: Scroll over panel to adjust volume

### Special Buttons
- **Heart/Mood Button**: Toggle to "like" a track
  - Configurable tag: `%FEEDBACK%`, `%2003_LOVED%`, `%LFM_LOVED%`, `%SMP_LOVED%`, or `%MOOD%`
  - Red when mood is set, gray when empty
  - Can be hidden via preferences
- **Track Rating Stars**: Interactive 5-star rating element
  - Click any star (1-5) to set rating; click the currently active star to clear rating (sets to unrated / `<not set>`)
  - Integrates with `foo_playcount` via context menu commands
  - Flexible placement: panel center (playback controls row) or Line 3 (track info area)
  - Can be hidden via preferences
- **MiniPlayer Launch**: Quick access button to launch or reveal the MiniPlayer
  - Requires [foo_traycontrols](https://github.com/jame25/foo_traycontrols)
  - Hidden by default
- **Super Button**: Quick access menu with autoplaylist queries and playback options
  - Autoplaylist queries: Never played, Recently played (last 5 days), Unrated, Rated 3-5/4/5, Loved tracks, Recently added, Same artist/title as selected
  - **Infinite Playback**: Toggle to automatically add similar tracks when the playlist ends (genre-based matching from media library)
  - **Playback Preview**: Submenu to auto-skip after a portion of each track (Off / 35% / 50% / 60 seconds)
  - **Skip Low Rating**: Submenu to toggle and set rating threshold (Off / 1 / <= 2 / <= 3) directly from menu
  - **Selection Mode**: Submenu to switch between Prioritize Now Playing Mode and Follow Selection
  - **Settings**: Quick link to open Now Bar preferences
- **Up to 12 Custom Buttons**: Fully configurable action buttons
  - **Buttons 1-6**: Visible on panel, configurable via Preferences
  - **Buttons 7-12**: Hidden, keyboard shortcuts only, configurable via config file
  - Actions: Open URL, [Run executable](#highlight-word1), [Foobar2k Action](#highlight-word2) (main menu or context menu), Open folder, or **Output Device** (opens popup menu listing all audio output devices to switch active output on click)
  - **3D Button Style**: Adds a raised, pad-like appearance with gradient and shadow; buttons animate when pressed for tactile feedback (enabled by default)
  - **State feedback**: Foobar2k Action buttons show accent color when the command is checked/active (e.g., toggle commands)
  - Custom icon glyph: Unicode symbol support ([enter character directly or use U+XXXX notation](#highlight-word3)), custom font family selection, and adjustable glyph size percentage (50%-120%, default 80%)
  - Custom tooltip label per button
  - Adaptive layout: 2-row (buttons 1-3, 4-6) at larger heights, single row at smaller heights
  - Auto-hide during playback (optional, with smooth 300ms fade animation)
  - URL/Executable actions use selected track for title formatting (not playing track)
  - Configuration profiles for saving/loading button sets (New / Rename / Delete / Export / Import)
  - Config file location: `<foobar2000_profile>\foo_nowbar_data\custom_buttons.conf` (supports `action = output_device`)

### Visualization Modes
- **Spectrum Visualizer**: Full-width spectrum analyzer behind playback buttons
  - Configurable bar width (Thin / Normal / Wide), height (Low: 20% / Normal: 33% / High: 50% of panel height), and style (Bars / Curve / Dominoes)
  - **Color Modes**: Adaptive (samples dominant album art color with HSL contrast normalization; falls back to theme accent), Solid (custom color), Gradient (custom two-color vertical gradient), Frequency (built-in frequency spectrum colors)
  - **Opacity Slider**: Adjustable opacity from 0% to 100% (default: 75%)
  - **Smooth Hover Dimming**: Bars smoothly dim via exponential easing when hovering over playback controls for button clarity
  - **Playback Time Display**: Toggleable top-right elapsed/total time readout (Show / Hidden)
  - Thin progress bar at top edge replaces the seekbar; enlarges on hover with top-layer timestamp tooltip for seeking
  - 30 FPS default, optional 60 FPS mode
- **Waveform Progress Bar**: SoundCloud-style pre-computed waveform replaces the seekbar
  - **Waveform Styles**: Style 1 (discrete vertical bars) and Style 2 (continuous two-tone centered envelope with primary accent outer peaks, lighter core tint, and baseline across silence)
  - **Waveform Widths**: Thin (1px), Wide (2px), and Wide (4K) (3px) density options (Style 1)
  - **Sweep Reveal Animation**: Left-to-right sweep reveal on track change (~250ms for cached tracks, progressive real-time reveal as audio decodes)
  - RMS-based computation with played/unplayed color distinction
  - Waveform data cached to disk across sessions (`wavecache.db`) with CUE and subsong support
  - Full seeking support with time tooltip on hover

### Theming & Appearance
- **Theme Modes**:
  - **Auto**: Follows foobar2000's theme automatically
  - **Dark**: Forces dark mode
  - **Light**: Forces light mode
  - **Custom**: Syncs with DUI color scheme (DUI) or CUI colour manager (CUI)
- **Background Style**:
  - **Solid**: Standard solid color background
  - **Artwork Colors**: Dynamic gradient extracted from album art's dominant colors
  - **Blurred Artwork**: Album art blurred as ambient background
- **Seek/Volume Bar Style**: Pill-shaped or rectangular
- **Seekbar Visibility**: Show or completely hide the seekbar/waveform/spectrum
- **Seekbar Length Mode**:
  - **Fixed** (default): Seekbar spans from heart/shuffle button to super/repeat button, length remains constant
  - **Scaling**: Dynamically extends the seekbar as panel width increases, filling 70% of the available gap on each side
- **Seekbar Horizontal Position**: Fine-tuning slider (-100 to +100 px offset) for seekbar horizontal alignment
- **Volume Control Visibility**: Show or completely hide the volume icon and volume slider independently
- **Volume Number**: Toggle numeric volume readout (Disabled / Enabled)
- **Play Icon Style**: Style 1 (Normal: accent circle with dark icon / Inverted: accent circle with white icon) / Style 2 (Rectangular outline, no accent circle) / Style 3 (Solid rectangle, no accent circle)
- **Hover Circles**: Optional hover effect on buttons
- **Hover Enlarge Effect**: Playback controls enlarge 15% on hover
- **Custom Fonts**: Select custom fonts for the three info lines on the left and time display, with full formatting support (colors, underline, etc.)
- **10 Custom Colors**: Button accent, play/pause accent, progress accent, volume accent, hover color, spectrum color (with primary and secondary gradient swatches), waveform played/unplayed colors, progress track color, volume track color (each independently toggleable between custom and theme-derived)
- **Smooth Animations**: Toggle for animated transitions (disabled by default for performance)
  - When enabled: custom button auto-hide fade, background crossfade
  - When disabled: instant transitions for better performance
- **Cover Artwork**: Toggle artwork visibility; optional margin around artwork
- **Online Artwork**: Fetch artwork from online sources when local art is unavailable (requires [foo_artwork](https://github.com/jame25/foo_artwork))

### Playback Features
- **Selection Mode**: Switch between Prioritize Now Playing Mode (displays active playback; falls back to selection when stopped) and Follow Selection (track info, artwork, rating stars, and mood icon always track selected item in active playlist or library)
- **Skip Low Rating**: Automatically skip tracks with low ratings during playback (configurable threshold 1-3 stars; requires foo_playcount). After 10 consecutive skips, the feature temporarily pauses to allow the next track to play, preventing infinite loops; toggleable from Preferences or Super Button menu
- **Infinite Playback**: Automatically add genre-matched tracks from the media library when the playlist ends (15 tracks at a time)
- **Playback Preview**: Auto-skip after a portion of each track for quick browsing (Off / 35% / 50% / 60 seconds)

## Installation

1. For **installed version of foobar2000 with file associations**: Double-click the `foo_nowbar*.fb2k-component` file to install.<br>
   For **portable version**: Open foobar2000, go to Preferences → Components, click Install..., select the `foo_nowbar*.fb2k-component` file, and click OK.
2. Restart foobar2000
3. Add the panel:
   - **Default UI**: View → Layout → Add panel → "Now Bar Control Panel"
   - **Columns UI**: Add "Now Bar Control Panel" panel to your layout

## Preferences

Access preferences via: File → Preferences → Tools → Now Bar OR Super Icon → Settings

### General Tab

| Setting | Options | Description |
|---------|---------|-------------|
| Line 1 Format | Title Formatting | Default: `%title%` |
| Line 2 Format | Title Formatting | Default: `%artist%` |
| Line 3 Format | Title Formatting | Default: blank; can display title format or rating stars |
| Rating Stars | Show (panel center) / Hidden / Line 3 (replaces third line title format) | Toggle rating stars visibility and position |
| Mood Tag | FEEDBACK / 2003_LOVED / LFM_LOVED / SMP_LOVED / MOOD | Which tag the heart button reads/writes |
| Skip Low Rating | Disabled / Enabled | Auto-skip low-rated tracks during playback |
| Rating Threshold | 1 / 2 / 3 | Skip tracks rated at or below this threshold |
| Visualization | Disabled / Spectrum / Waveform | Visualization mode selector |
| 60 FPS | Checkbox | Run spectrum at 60fps instead of 30fps |
| Playback Time | Show / Hidden | Toggle top-right time readout in Spectrum mode (default: Show) |
| Spectrum Style | Bars / Curve / Dominoes | Spectrum visual style |
| Spectrum Width | Thin / Normal / Wide | Spectrum bar width (grayed out in Curve style) |
| Spectrum Height | Low / Normal / High | Spectrum display height |
| Waveform Style | 1 / 2 | Waveform style: 1 (Bottom bars) or 2 (Centered envelope) |
| Waveform Width | Thin / Wide / Wide (4K) | Waveform bar density (Style 1 only; grayed out in Style 2) |

### Appearance Tab

| Setting | Options | Description |
|---------|---------|-------------|
| Theme Mode | Auto / Dark / Light / Custom | Controls panel color scheme |
| Cover Artwork | Yes / No | Show or hide album artwork |
| Cover Margin | Yes / No | Add margin around artwork |
| Cover Style | Square / Rounded | Toggle album cover corner style |
| Background Style | Solid / Artwork Colors / Blurred Artwork | Panel background appearance |
| Bar Style | Pill-shaped / Rectangular | Seek and volume bar shape |
| Seekbar | On / Off | Show or hide the seekbar |
| Seekbar Length | Fixed / Scaling | Toggle seekbar length mode |
| Seekbar Position | Slider (-100 to +100) | Adjust seekbar horizontal offset in pixels |
| Smooth Animations | Enabled / Disabled | Smooth animated transitions |
| 3D Buttons | Enabled / Disabled | Toggle 3D style for custom buttons |
| Volume Number | Disabled / Enabled | Display inline volume number (0-100) next to volume bar or icon |
| Online Artwork | Checkbox | Fetch online artwork (requires foo_artwork) |

### Icons Tab

| Setting | Options | Description |
|---------|---------|-------------|
| Mood Icon | Show / Hidden | Toggle heart button visibility |
| Shuffle Icon | Show / Hidden | Toggle shuffle button visibility |
| Repeat Icon | Show / Hidden | Toggle repeat button visibility |
| Stop Button | Show / Hidden | Toggle stop button visibility |
| Stop After Current | Show / Hidden | Toggle stop-after-current button visibility |
| Super Button | Show / Hidden | Toggle Super menu button visibility |
| MiniPlayer Icon | Show / Hidden | Toggle MiniPlayer button visibility |
| Hover Circles | Show / Hide | Show circular hover effect on buttons |
| Alternate Icons | Style 1 / 2 / 3 | Toggle play/pause icon style |
| Play Icon Style | Normal / Inverted | Normal: accent bg + dark icon; Inverted: accent bg + white icon |
| Auto-hide C-buttons | Yes / No | Custom buttons fade out during active playback |
| Volume Icon | Show / Hide | Toggle volume icon visibility |
| Volume Bar | Show / Hide | Toggle volume bar visibility |

### Custom Button Tab

#### Configuration Profile
- **Configuration name**: Select between saved button configurations
- **[...] menu**: New, Rename, Delete, Export, Import options for profiles

#### Button Configuration
Configure up to 6 visible custom buttons (7-12 via config file only):
- **None**: Button disabled
- **Open URL**: Opens a URL in the default browser (supports Title Formatting, uses selected track)
- <a name="highlight-word1"></a>**Run Executable**: Launches an external program (supports Title Formatting, uses selected track)
- <a name="highlight-word2"></a>**Foobar2k Action**: Executes a foobar2000 menu command (e.g., `Playback/Stop` or context menu `File Operations/Move to/MP3`); shows accent color when the command is active
- **Open Folder**: Opens the directory containing the currently selected track
- **Output Device**: Opens a popup menu listing all available audio output devices (ASIO, WASAPI, DirectSound, Null Output, etc.) to switch foobar2000's output device directly on click (no path required)

Each button also supports:
- **Font**: Select font family from presets (`Segoe UI`, `Segoe MDL2 Assets`, `Segoe Fluent Icons`, `Segoe UI Symbol`, `Material Icons Outlined`, `Material Icons`, `Wingdings`, `Webdings`) or enter any installed font name
- <a name="highlight-word3"></a>**Custom Icon**: Unicode symbol support - enter characters directly or use U+XXXX notation. For example, select `Segoe UI` font and paste `🎶` directly, or select `Segoe Fluent Icons` font and enter `U+E8D6`
- **Glyph Size**: Adjust icon glyph size percentage (presets: 50%, 60%, 70%, 80%, 90%, 100%, 120%; default: 80%)
- **Tooltip Label**: Custom text shown on hover (defaults to "Button #N")
- Automatic fallback to numbered square icons when custom icon is missing

### Fonts & Colors Tab

#### Fonts
- **Left Line 1-3**: Font for the left info area (supports colors, underline, etc.)
- **Time Display**: Font for elapsed/remaining time

#### Colors
Each color has a checkbox: unchecked uses theme colors from DUI/CUI, checked uses a custom color.

| Color | Default (theme) | Description |
|-------|----------------|-------------|
| Button Accent | DUI Highlight / CUI highlight | Active state for Shuffle, Repeat, etc. |
| Play/Pause Accent | DUI Highlight / CUI highlight | Play button background circle |
| Progress Accent | DUI Highlight / CUI highlight | Progress bar fill |
| Progress Track | Theme-derived | Progress bar unfilled portion |
| Hover Color | DUI Selection / CUI selection | Button hover circle |
| Spectrum Color | Adaptive / Solid / Gradient / Frequency | Visualizer bars; includes color mode dropdown, opacity slider (0-100%), and dual swatches for gradient mode |
| Waveform Color | DUI Highlight / CUI highlight | Waveform played portion |
| Waveform Unplayed | DUI Text / CUI text | Waveform unplayed portion |
| Volume Accent | DUI Highlight / CUI highlight | Volume bar fill |
| Volume Track | Theme-derived | Volume bar unfilled portion |

### Keyboard Shortcuts
All 12 custom button actions can be triggered via keyboard shortcuts:

1. Go to **Preferences → Keyboard Shortcuts**
2. Find commands under **File → Now Bar**:
   - `Custom Button 1` through `Custom Button 12`
3. Assign any keyboard shortcut to trigger the corresponding button's action

## Building from Source

### Prerequisites

- Visual Studio 2022 (v143 toolset)
- foobar2000 SDK
- Columns UI SDK
- Windows 10 SDK

### Build Commands

**64-bit Release:**
```bash
msbuild foo_nowbar.vcxproj /p:Configuration=Release /p:Platform=x64 /p:PlatformToolset=v143 /v:minimal
```

**32-bit Release:**
```bash
msbuild foo_nowbar.vcxproj /p:Configuration=Release /p:Platform=Win32 /p:PlatformToolset=v143 /v:minimal
```

> **Note**: Ensure all SDK libraries (foobar2000_SDK, pfc, columns_ui_sdk) are built with matching runtime library settings (`/MT` for static).

## Project Structure

```
foo_nowbar/
├── core/
│   ├── control_panel_core.cpp   # Core rendering and interaction logic
│   ├── control_panel_core.h     # Core class, layout metrics, and hit regions
│   ├── playback_state.cpp       # Playback state tracking and callbacks
│   └── playback_state.h         # Playback state structures
├── ui/
│   ├── control_panel_cui.cpp    # Columns UI wrapper
│   ├── control_panel_cui.h
│   ├── control_panel_dui.cpp    # Default UI wrapper
│   └── control_panel_dui.h
├── artwork_bridge.cpp           # Runtime bridge to foo_artwork for online artwork
├── artwork_bridge.h
├── preferences.cpp              # Preferences page implementation
├── preferences.h                # Preferences declarations
├── preferences.rc               # Preferences dialog resources
├── resource.h                   # Resource IDs
├── component.cpp                # Component initialization
├── component_client.cpp         # foobar2000 component client
├── mainmenu_commands.cpp        # Main menu commands for keyboard shortcuts
├── guids.h                      # Component GUIDs
├── pch.h / pch.cpp              # Precompiled headers
└── version.h                    # Version information
```

## Controls Reference

| Element | Action |
|---------|--------|
| **Play/Pause** | Click to toggle playback |
| **Stop** | Stop playback (optional, hidden by default) |
| **Stop After Current** | Toggle stop-after-current (optional, hidden by default; accent color when active) |
| **Previous/Next** | Navigate tracks |
| **Shuffle** | Toggle shuffle mode (accent color when active; synced with MiniPlayer) |
| **Repeat** | Cycle repeat modes: Off -> All -> Track (accent color when active; synced with MiniPlayer) |
| **Rating Stars** | Click star (1-5) to set rating; click active star to clear rating (sets to unrated) |
| **Super Button** | Open menu: autoplaylists, infinite playback, preview, skip low rating, selection mode, settings |
| **Seek Bar** | Click or drag to seek within track (tooltip shows timestamp) |
| **Thin Progress Bar** | Hover and click or drag along top edge to seek in Spectrum mode (tooltip shows timestamp) |
| **Volume Icon** | Click to mute/unmute (restores previous volume on unmute) |
| **Volume Bar** | Click or drag to adjust volume |
| **Volume Number** | Displays numeric volume level (0-100) next to volume bar or icon (optional) |
| **Mouse Wheel** | Scroll over panel to adjust volume (tooltip shows dB when volume number is disabled) |
| **Heart Icon** | Toggle mood tag for current track (red when set) |
| **MiniPlayer Icon** | Launch or reveal MiniPlayer |
| **Custom Buttons** | Execute configured action (URL, program, foobar2k command, folder, or output device menu); accent color when active |
| **Artwork** | Double-click to view in album art viewer |
| **Track Info** | Double-click to highlight playing track in playlist |

## Dependencies

- [foobar2000 SDK](https://www.foobar2000.org/SDK)
- [Columns UI SDK](https://github.com/reupen/columns_ui-sdk)
- [foo_playcount](https://www.foobar2000.org/components/view/foo_playcount) (optional, for rating stars and skip low rating)
- [foo_traycontrols](https://github.com/jame25/foo_traycontrols) (optional, for MiniPlayer functionality)
- [foo_artwork](https://github.com/jame25/foo_artwork) (optional, for online artwork)

## License

This component is provided as-is for personal use with foobar2000.

## Support Development

If you find these components useful, consider supporting development:

| Platform | Payment Methods |
|----------|----------------|
| **[Ko-fi](https://ko-fi.com/Jame25)** | Cards, PayPal |

Your support helps cover development time and enables new features. Thank you! 🙏

---

## 支持开发

如果您觉得这些组件有用，请考虑支持开发：

| 平台 | 支付方式 |
|------|----------|
| **[Ko-fi](https://ko-fi.com/Jame25)** | 银行卡、PayPal |

您的支持有助于支付开发时间并实现新功能。谢谢！🙏

---

**Feature Requests:** Paid feature requests are available for supporters. [Contact me on Discord](https://discord.gg/jSajdJ3nMz) to discuss.

**功能请求：** 为支持者提供付费功能请求。[请在 Discord 上联系我](https://discord.gg/jSajdJ3nMz) 进行讨论。
