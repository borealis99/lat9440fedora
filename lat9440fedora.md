## GRUB out i915 PSR

## Firefox: Installing Extensions

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
            "https://addons.mozilla.org/firefox/downloads/latest/darkreader/latest.xpi"
         ]
      }
   }
}
```

Extensions will be installed when Firefox next starts.
