## GRUB out i915 PSR
  _**This is specific to my Dell 9440, but if you're experiencing your screen update in sparse vertical lines this may help you too.**_ 
   ```bash
   sudo grubby --update-kernel=ALL --args="i915.enable_psr=0"
   sudo reboot now
   ```
  _**And for non-Fedora:**_
  ```bash
  sudo nano /etc/default/grub
  ```
  Then, at the end of the line containing `linux`, add `i915.enable_psr=0`. You should also do this within the grub menu of the live CD for a smoother installation experience.

## Get my CTRL+ALT+T terminal back:
   Settings --> Keyboard --> Keyboard Shortcuts --> View and Customize Shortcuts \
   `ptyxis -s`

## Change the hostname
   _**Is this the Krusty Krab?**_
   ```bash
   sudo hostnamectl set-hostname $CHANGE_ME_HOSTNAME_UWU_CHANGE_ME
   ```

## Reboot to make shortcut and hostname settings stick
  ```bash
  sudo reboot now
  ```

## Firefox a la Marci

Create a policy file to auto-install extensions and disable unwanted features (passwd mgr, sidebar, AI):

F1. **Create the policy directory and policies.json file:**
   ```bash
   sudo mkdir -p /etc/firefox/policies
   sudo nano /etc/firefox/policies/policies.json
   ```

F2. **Add policies:**
  ```json
  {
    "policies": {
      "Extensions": {
        "Install": [
          "https://addons.mozilla.org/firefox/downloads/latest/ublock-origin/latest.xpi",
          "https://addons.mozilla.org/firefox/downloads/latest/bitwarden-password-manager/latest.xpi",
          "https://addons.mozilla.org/firefox/downloads/latest/privacy-com/latest.xpi",
          "https://addons.mozilla.org/firefox/downloads/latest/darkreader/latest.xpi",
          "https://addons.mozilla.org/firefox/downloads/file/4066280/lush_bold-2.1.xpi"
        ]
      },
      "PasswordManagerEnabled": false,
      "OfferToSaveLogins": false,
      "OfferToSaveLoginsDefault": false,
      "DisableFirefoxStudies": true,
      "UserMessaging": {
        "ExtensionRecommendations": false,
        "FeatureRecommendations": false,
        "UrlbarInterventions": false,
        "SkipOnboarding": true,
        "MoreFromMozilla": false,
        "WhatsNew": false
      },
      "FirefoxSuggest": {
        "WebSuggestions": false,
        "SponsoredSuggestions": false,
        "ImproveSuggest": false
      },
      "Preferences": {
        "browser.ml.enable": {
          "Value": false,
          "Status": "locked"
        },
        "browser.ml.chat.enabled": {
          "Value": false,
          "Status": "locked"
        }
      }
    }
  }
  ```

Extensions will be installed when Firefox next starts.

## Moar Software

  ```bash
  flatpak install flathub com.github.flxzt.rnote        # RNote: Have Stylus, Will Draw
  flatpak install flathub com.visualstudio.code         # VS Code: For Reasons
  flatpak install flathub org.signal.Signal             # Signal: Texting a la Hegseth
  flatpak install flathub com.discordapp.Discord        # Discord: For Nerds (Like Me)
  flatpak install flathub org.kde.krita                 # Krita: Exercise the Stylus
  flatpak install flathub io.github.pwr_solaar.solaar   # Solaar: For Logitech Unifying & Bolt
  flatpak install flathub com.prusa3d.PrusaSlicer       # PrusaSlicer: he must slice
  flatpak install flathub md.obsidian.Obsidian          # Obsidian: Note-taking
  flatpak install flathub com.github.marktext.marktext  # MarkText: Markdown Editor
  ```
## A GNOME to Call Home
### Disable GNOME Hot Corners and Automatic Screen Brightness
  ```bash
  gsettings set org.gnome.desktop.interface enable-hot-corners false
  gsettings set org.gnome.settings-daemon.plugins.power ambient-enabled false
  ```
### Enable Gnome Extensions and the gTiles Window Manager
  ```bash
  flatpak install flathub org.gnome.Extensions
  ```
  Then install gTiles: https://extensions.gnome.org/extension/28/gtile/

  #### gTiles Resize Presets Configuration
  After installing gTiles, configure these resize presets in the extension settings.
  
  _Preset numbers 11+ were selected as they are existing Ctrl + Super combos._

  | Preset | Keyboard Shortcut | Grid Layout | Description |
  |--------|------------------|-------------|-------------|
  | Resize preset 11 | Ctrl+Super+d | `3x2 1:1 1:2 , 3x2 1:1 1:1 , 3x2 1:2 1:2` | Left third layouts |
  | Resize preset 12 | Ctrl+Super+f | `3x2 2:1 2:2 , 3x2 2:1 2:1 , 3x2 2:2 2:2` | Middle third layouts |
  | Resize preset 13 | Ctrl+Super+g | `3x2 3:1 3:2 , 3x2 3:1 3:1 , 3x2 3:2 3:2` | Right third layouts |
  | Resize preset 14 | Ctrl+Super+e | `3x2 1:1 2:2` | Left two-thirds , full height |
  | Resize preset 15 | Ctrl+Super+t | `3x2 2:1 3:2` | Right two-thirds , full height |
  | Resize preset 16 | Ctrl+Super+r | `6x1 2:1 5:1` | Center two-thirds , full height |
  | Resize preset 17 | Ctrl+Super+Return | `1x1 1:1 1:1` | Full Screen |

  # gTile Configuration via Terminal

gTile stores its settings in dconf, so you can configure it entirely from the command line without using the GUI.

## Finding the Settings

gTile settings live at `/org/gnome/shell/extensions/gtile/` in dconf. However, this path won't show anything until you've changed at least one setting from the default.

To verify gTile is installed and find its schema:

```bash
find /usr/share/gnome-shell/extensions ~/.local/share/gnome-shell/extensions \
  -name "*.xml" 2>/dev/null | xargs grep -l -i gtile
```

## Exporting and Importing Settings

Export current settings to a file:

```bash
dconf dump /org/gnome/shell/extensions/gtile/ > gtile-settings.conf
```

Import settings from a file:

```bash
dconf load /org/gnome/shell/extensions/gtile/ < gtile-settings.conf
```

## Setting Individual Values

```bash
dconf write /org/gnome/shell/extensions/gtile/resize1 "'6x4 1:1 3:4'"
```

Note the nested quotes: outer double quotes for the shell, inner single quotes for dconf.

## Resize Preset Format

Resize presets use the format:

```
WxH X1:Y1 X2:Y2
```

Where:
- `WxH` is the grid size (columns × rows)
- `X1:Y1` is the top-left cell of the window placement
- `X2:Y2` is the bottom-right cell of the window placement

For example, `3x2 1:1 2:2` on a 3-column, 2-row grid places the window in the left two-thirds at full height.

### Cycling Presets

Separate multiple positions with commas to cycle through them when pressing the same shortcut repeatedly:

```
3x2 1:1 1:2, 3x2 1:1 1:1, 3x2 1:2 1:2
```

This cycles through: full left third → top-left third → bottom-left third.

## Example Configuration

This configuration sets up thirds-based window management:

```bash
cat > gtile-presets.conf << 'EOF'
[/]
resize11='3x2 1:1 1:2, 3x2 1:1 1:1, 3x2 1:2 1:2'
resize12='3x2 2:1 2:2, 3x2 2:1 2:1, 3x2 2:2 2:2'
resize13='3x2 3:1 3:2, 3x2 3:1 3:1, 3x2 3:2 3:2'
resize14='3x2 1:1 2:2'
resize15='3x2 2:1 3:2'
resize16='6x1 2:1 5:1'
resize17='1x1 1:1 1:1'
preset-resize-11=['<Super><Control>d']
preset-resize-12=['<Super><Control>f']
preset-resize-13=['<Super><Control>g']
preset-resize-14=['<Super><Control>e']
preset-resize-15=['<Super><Control>t']
preset-resize-16=['<Super><Control>r']
preset-resize-17=['<Super><Control>Return']
EOF

dconf load /org/gnome/shell/extensions/gtile/ < gtile-presets.conf
```

| Preset | Shortcut | Layout | Description |
|--------|----------|--------|-------------|
| 11 | Ctrl+Super+D | `3x2 1:1 1:2, ...` | Left third (cycles full/top/bottom) |
| 12 | Ctrl+Super+F | `3x2 2:1 2:2, ...` | Middle third (cycles full/top/bottom) |
| 13 | Ctrl+Super+G | `3x2 3:1 3:2, ...` | Right third (cycles full/top/bottom) |
| 14 | Ctrl+Super+E | `3x2 1:1 2:2` | Left two-thirds, full height |
| 15 | Ctrl+Super+T | `3x2 2:1 3:2` | Right two-thirds, full height |
| 16 | Ctrl+Super+R | `6x1 2:1 5:1` | Center two-thirds, full height |
| 17 | Ctrl+Super+Return | `1x1 1:1 1:1` | Fullscreen |

## Applying Changes

After loading settings, you may need to restart GNOME Shell:

- **X11:** Press Alt+F2, type `r`, press Enter
- **Wayland:** Log out and back in

## Verifying Configuration

```bash
dconf dump /org/gnome/shell/extensions/gtile/
```

### Then Reboot
  ```bash
  sudo reboot now
  ```
