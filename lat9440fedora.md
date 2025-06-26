## GRUB out i915 PSR
  _**This is specific to my Dell 9440, but if you're experiencing heavy graphics glitches this may help you too.**_ 
   ```bash
   sudo grubby --update-kernel=ALL --args="i915.enable_psr=0"
   sudo reboot now
   ```

## Get my CTRL+ALT+T terminal back:
   Settings --> Keyboard --> Keyboard Shortcuts --> View and Customize Shortcuts \
   `ptyxis --new-tab`

## Change the hostname
   _**Is this the Krusty Krab?**_
   ```bash
   sudo hostnamectl set-hostname $CHANGE_ME_HOSTNAME_UWU_CHANGE_ME
   ```

## Reboot to make shortcut and hostname settings stick
  ```bash
  sudo reboot now
  ```

## Firefox: Install Extensions and Theme

Create a policy file to auto-install extensions:

F1. **Create the policy directory and policies.json file:**
   ```bash
   sudo mkdir -p /etc/firefox/policies
   sudo nano /etc/firefox/policies/policies.json
   ```

F2. **Add extension installation policy:**
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
      }
   }
}
```

Extensions will be installed when Firefox next starts.

## Moar Software

   ```bash
   flatpak install flathub com.github.flxzt.rnote  # RNote: Have Stylus, Will Draw
   flatpak install flathub com.visualstudio.code   # VS Code: For Reasons
   flatpak install flathub org.signal.Signal       # Signal: Texting a la Hegseth
   flatpak install flathub com.discordapp.Discord  # Discord: For Nerds (Like Me)
   flatpak install flathub org.kde.krita           # Krita: Exercise the Stylus
   ```
