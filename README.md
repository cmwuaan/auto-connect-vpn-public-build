<div align="center">

<img src="https://img.shields.io/badge/%F0%9F%94%92-AutoVPN-1f6feb?style=for-the-badge&labelColor=0d1117" alt="AutoVPN" height="42">

### One-click OpenVPN from the macOS menu bar — automatic OTP, automatic reconnect, nothing left behind

[![Release](https://img.shields.io/github/v/release/cmwuaan/auto-connect-vpn-public-build?display_name=tag&sort=semver&color=2ea043)](https://github.com/cmwuaan/auto-connect-vpn-public-build/releases/latest)
![macOS](https://img.shields.io/badge/macOS-12%2B-000000?logo=apple&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

</div>

---

This repository only hosts **release builds** of AutoVPN: the `.dmg` / `.zip` downloads and the signed update
information the app checks for new versions. Releases are published automatically; there is no source code here.

## What AutoVPN does

AutoVPN is a small menu bar app around Homebrew's `openvpn`. It uses **your** `.ovpn` profile as is and never changes
the profile or the options the server pushes.

- **One click** — lock icon in the menu bar, <kbd>⌘</kbd><kbd>K</kbd> to connect or disconnect.
- **Automatic sign-in** — password/PIN and TOTP secret live in the macOS **Keychain**; a fresh OTP is generated for
  every connection.
- **Automatic reconnect** — after network drops, Wi-Fi changes or server-side disconnects.
- **Sleep aware** — waits until the Mac is fully awake before reconnecting.
- **Nothing left behind** — restores DNS to match System Settings when the VPN is off.
- **Automatic updates** — the app offers new versions from the menu and installs them itself.
- **English / Vietnamese** interface.

## Install

1. Download **`AutoVPN-<version>.dmg`** from the [latest release](https://github.com/cmwuaan/auto-connect-vpn-public-build/releases/latest).
2. Open it and drag **AutoVPN.app** to **Applications**.
3. Install OpenVPN with [Homebrew](https://brew.sh):

   ```bash
   brew install openvpn
   ```

4. The app is not signed or notarized by Apple, so allow it once:

   ```bash
   xattr -dr com.apple.quarantine "/Applications/AutoVPN.app"
   ```

   or right-click the app → **Open**.

Verify a download (optional): put `SHA256SUMS` next to the files and run `shasum -a 256 -c SHA256SUMS`.

## First run

The **Settings** window opens on the **Account** tab:

1. **Choose .ovpn file…** — pick your OpenVPN profile.
2. Pick the **sign-in method** and fill in username, password/PIN and TOTP secret as needed.
3. **Save**, then accept **Install sudo permissions** (your Mac password, once).
4. Press <kbd>⌘</kbd><kbd>K</kbd> in the menu to connect.

> [!IMPORTANT]
> The **TOTP secret** is the Base32 string you got when enrolling your authenticator (often inside the QR code),
> **not** the 6-digit code.

## Updates

The app checks for a new version once a day. When one is available, the menu shows **Update to AutoVPN X.Y.Z…**:
the app downloads it, verifies its signature, then closes and reopens on the new version. A running VPN stays
connected; your settings, Keychain items and sudo permissions are kept.

- Check now: **Help → Check for Updates…**
- Turn the daily check off: **Settings → General**

Versions released before automatic updates existed must be replaced once by hand (steps above); settings are kept.

## Troubleshooting

Run the built-in check and follow its advice:

```bash
/Applications/AutoVPN.app/Contents/MacOS/vpn doctor
```

or **Help → Check Setup…** in the menu. When asking for help, copy its report.

## License

MIT. OpenVPN is a trademark of OpenVPN Inc.; AutoVPN is an independent project that uses the `openvpn` installed on
your Mac.
