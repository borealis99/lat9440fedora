## GRUB out i915 PSR
  _**This is specific to my Dell 9440, but if you're experiencing your screen update in sparse vertical lines this may help you too.**_ 
   ```bash
   sudo grubby --update-kernel=ALL --args="i915.enable_psr=0"
   sudo reboot now
   ```

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
  After installing gTiles, configure these resize presets in the extension settings:

  | Preset | Keyboard Shortcut | Grid Layout | Description |
  |--------|------------------|-------------|-------------|
  | Resize preset 11 | Ctrl+Super+d | `3x2 1:1 1:2 , 3x2 1:1 1:1 , 3x2 1:2 1:2` | Left third layouts |
  | Resize preset 12 | Ctrl+Super+f | `3x2 2:1 2:2 , 3x2 2:1 2:1 , 3x2 2:2 2:2` | Middle third layouts |
  | Resize preset 13 | Ctrl+Super+g | `3x2 3:1 3:2 , 3x2 3:1 3:1 , 3x2 3:2 3:2` | Right third layouts |
  | Resize preset 14 | Ctrl+Super+e | `3x2 1:1 2:2` | Left two-thirds , full height |
  | Resize preset 15 | Ctrl+Super+t | `3x2 2:1 3:2` | Right two-thirds , full height |
  | Resize preset 15 | Ctrl+Super+r | `6x1 2:1 5:1` | Center two-thirds , full height |

### Then Reboot
  ```bash
  sudo reboot now
  ```
