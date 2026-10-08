This is a personal fork of the repo created by Stachugit. See the [original here](https://github.com/Stachugit/MeshCore-Cardputer-ADV).

## Changes in this fork

### Fixes
- **Crash loop with more than 64 contacts** - the contact list used a 64-slot array, so once more contacts were heard the device crashed on the contacts screen and kept crashing on every reboot
- **Backspace and FN+ESC not working when built from source** - the M5Cardputer library is now pinned to 1.1.1 (1.2.0 changed how these keys are reported). RadioLib, M5Unified and M5GFX are pinned too, so rebuilds stay reproducible
- **Contact/channel search** reading uninitialised memory for empty names and overflowing on 32-character names
- **GPS on/off from the app** used a hand-copied settings layout that only worked by chance; it now uses the real one

### Contacts and messages
- **Up to 500 contacts** (was 200). When the list is full, the least recently heard contact that isn't a favourite is replaced, instead of new contacts being silently ignored
- **Offline message queue stored in flash** - messages waiting for the phone app are kept in internal flash (up to 1024) instead of RAM, and now survive reboots and power loss
- **Favourites** - star contacts on the device; favourites are never auto-replaced and sync with the phone app's favourite flag on its next contact refresh

### Interface
- **Tab bar with icons** - Contacts, Favourites and Channels, in the theme colours
- **Battery icon and percentage** in the top-right of the home screen, using a LiPo discharge curve for a more realistic reading
- **Favourite star button** in the chat header
- **Long chat names scroll** across the header instead of being cut off
- **Device Info** is larger and scrollable, and adds the Bluetooth PIN, contact usage (e.g. 186/500) and free RAM

### Keyboard controls (new or changed)
- **Tab** - Cycle tabs: Contacts → Favourites → Channels
- **🟠 ←** / **🟠 →** - Move between the three tabs
- **🟠 FN+F** - Favourite / unfavourite the selected contact, or the contact you're chatting with
- **🟠 FN+ESC** on the home screen - Clear the search, or open Settings if not searching
- **🟠 ↑** / **🟠 ↓** in Device Info - Scroll

### Notes
- **The Bluetooth pairing PIN** is now under **Settings → Device Info** (the top-right corner shows the battery). The original setup steps below still refer to the top-right corner
- **The web flasher, M5Burner and release binaries below install the original firmware, not this fork.** To use this fork, build and flash it from source:
  ```bash
  pio run -e M5stack_cardputer_cap_lora1262_companion -t upload
  ```
  A normal upload keeps your settings, contacts and channels. Don't use `-t erase` or `-t uploadfs`, which wipe them
- Verbose logging is off by default; uncomment `MESH_DEBUG=1` in `variants/m5stack_cardputer/platformio.ini` to turn it back on

---

The original README follows as so:

# 🔥 MeshCore-Cardputer-ADV 🔥

[![Buy Me a Coffee](https://img.buymeacoffee.com/button-api/?text=Buy%20me%20a%20coffee&emoji=☕&slug=Stachu&button_colour=ff8800&font_colour=000000&font_family=Lato&outline_colour=000000&coffee_colour=FFDD00)](https://buymeacoffee.com/Stachu)

## 🌐 Quick Flash via Web Flasher (Recommended)

### **[⚡ Flash Firmware Online →](https://meshcorecardputeradv.vercel.app/)**

✅ **No installation needed!** Flash directly from your browser  
✅ **Preserves your settings** - keeps all your data intact  
✅ **Fast and easy** - just connect and click

---

Enhanced TFT user interface for MeshCore mesh networking firmware, optimized for M5Stack Cardputer-Adv with Cap LoRa-1262.

![MeshCore-Cardputer-ADV](docs/images/Imagecardp.png)

## 📸 Screenshots

<details>
<summary>Click to view screenshots</summary>

### Main Interface
| Chat | Contacts | Channels |
|------|----------|----------|
| ![Chat](docs/images/Chat.bmp) | ![Contact](docs/images/Contact.bmp) | ![Channel](docs/images/Channel.bmp) |

### Settings Menu
| Main Settings | Public Info | Radio Setup |
|---------------|-------------|-------------|
| ![Settings](docs/images/Settings.bmp) | ![Public Info](docs/images/Publicinfo.bmp) | ![Radio Setup](docs/images/RadioSetup.bmp) |

### Radio Configuration
| Choose Preset | Manual Setup | Device Info |
|---------------|--------------|-------------|
| ![Choose Preset](docs/images/ChoosePreset.bmp) | ![Manual Setup](docs/images/ManualSetup.bmp) | ![Device Info](docs/images/DeviceInfo.bmp) |

### Customization
| Theme Settings | Other Options |
|----------------|---------------|
| ![Theme](docs/images/Theme.bmp) | ![Other](docs/images/Other.bmp) |

</details>

## 📦 Installation Options

### Option 1: Web Flasher (⭐ Recommended)
Visit **[https://meshcorecardputeradv.vercel.app/](https://meshcorecardputeradv.vercel.app/)** and flash directly from your browser!

**Why use the Web Flasher?**
- ✅ No software installation required
- ✅ Preserves all your settings and data
- ✅ Fastest and easiest method
- ✅ Works on any modern browser

### Option 2: M5Burner
Search in M5Burner for:
- `MeshCore-Cardputer-ADV M5Stack Cap LoRa1262 version!!!!` - **Plug-and-play**

⚠️ **WARNING**: Flashing with M5Burner will erase all data from your device, including settings, contacts, and channels. Use the Web Flasher to preserve your data.

### Option 3: Pre-compiled Binary
Download `firmware_Cap_LoRa-1262.bin` from [Releases](https://github.com/Stachugit/MeshCore-Cardputer-ADV/releases) and flash using esptool.py or ESP Flash Download Tool.

## 🔧 Hardware Requirements

### M5Stack Cap LoRa-1262 (Required)
Simply attach the Cap LoRa-1262 to your Cardputer-Adv - no wiring needed!
- **Module**: RA-01SH (SX1262)
- **Frequency**: 863-870 MHz
- **Documentation**: [Cap LoRa-1262](https://docs.m5stack.com/en/cap/Cap_LoRa-1262)

## ✨ Features

### Chat Interface
- **Chat bubbles** with sender names
- **150-character limit** with real-time counter
- **Notification popups** for new messages
- **Message scrolling** with FN+UP/DOWN
- **18 color themes** with brightness control
- **Real-time search** in contacts and channels

### Keyboard Controls
- **🟠 ↑** - Up
- **🟠 ↓** - Down
- **🟠 ←** - Contacts
- **🟠 →** - Channels
- **Enter** - Send/Select
- **Backspace** - Delete | **Hold Backspace** - Clear all
- **🟠 FN+ESC** - Go back
- **Opt** - Go back
- **🟠 FN+↑** / **🟠 FN+↓** - Scroll messages (in writing mode)
- **🟠 FN+DEL** - Delete contacts/channels
- **G0(Top right button)** - Send an advert

### Settings Menu (☰)

Access the settings menu via the **☰** icon in the top-left corner. All settings persist across restarts.

#### 📱 Public Info
- **Change Name** - Modify device name
- **Share Key** - Display QR code with public key for easy pairing
- **Share Position** - Enable/disable position sharing in advertisements

#### 📡 Radio Setup
- **GPS On/Off** - Enable or disable GPS (position checked every 3 minutes)
- **Choose Preset** - Select from predefined radio configurations
- **Manual Setup** - Configure individual parameters:
  - Frequency
  - Bandwidth
  - Spreading Factor (SF)
  - Coding Rate (CR)
  - TX Power

#### 🎨 Theme
- **Brightness Control** - Adjust screen brightness
- **Color Schemes** - Choose from 18 available themes

#### ⚙️ Other
- **Sleep Timeout** - Screen auto-sleep options: 10s, 30s, 1m, 2m, 5m, Never
- **Factory Reset** - Restore device to factory settings (generates new key)
- **Spark the Project** - Support development via QR code (links to Buy Me a Coffee)

#### 📊 Device Info
View real-time device information:
- Device name
- Battery status
- GPS coordinates
- Radio frequency
- Spreading Factor (SF)
- TX Power
- System uptime

## 🚀 Initial Setup

**Important**: First-time configuration requires the MeshCore mobile app:

1. Flash firmware to Cardputer-Adv (via web flasher or M5Burner)
2. Download MeshCore app on your smartphone
3. Connect via Bluetooth using the pairing code displayed in the top-right corner of the screen
4. Configure node name, region, network keys, and channels

## 🆕 What's New in This Version

### Major Features
- **Delete contacts and channels** from device using FN+DEL
- **Comprehensive settings menu** organized into tabs: Public Info, Radio Setup, Theme, Other, and Device Info
- **GPS integration** with 3-minute position update intervals
- **Manual radio configuration** for advanced users
- **QR code sharing** for easy device pairing
- **Position sharing toggle** for privacy control
- **Multiple sleep timeout options** for battery optimization
- **Factory reset option** for easy device reconfiguration

### Improvements
- Enhanced Cap LoRa-1262 compatibility and stability
- UI refinements for better usability
- Power consumption optimizations for extended battery life
- Improved Bluetooth pairing experience

## 🛠️ Building from Source

```bash
git clone https://github.com/Stachugit/MeshCore-Cardputer-ADV.git
cd MeshCore-Cardputer-ADV

# For Cap LoRa-1262:
pio run -e M5stack_cardputer_cap_lora1262_companion --target upload
```

## 🙏 Credits

Based on [MeshCore](https://github.com/meshcore-dev/MeshCore) mesh networking firmware. This project adds custom TFT UI, chat bubbles, comprehensive settings system, theme customization, and enhanced keyboard navigation.

Cap LoRa-1262 compatibility fixes based on work by [sosprz](https://github.com/sosprz/meshcore-cardputer-adv).

## 📜 License

Same license as original MeshCore firmware. See [license.txt](license.txt).

## 🤝 Contributing

Contributions welcome! Report bugs, suggest features, submit pull requests, or improve documentation.

## 🔗 Links

- **Web Flasher**: https://meshcorecardputeradv.vercel.app/
- **Original MeshCore**: https://github.com/meshcore-dev/MeshCore
- **M5Stack Cardputer-ADV**: https://shop.m5stack.com/products/m5stack-cardputer-adv-version-esp32-s3
- **Cap LoRa-1262**: https://docs.m5stack.com/en/cap/Cap_LoRa-1262
- **Support Development**: https://buymeacoffee.com/Stachu

## ⚠️ Disclaimer

Independent UI modification of MeshCore. For core networking questions, refer to the original project.

---

**Version**: 1.1.0 | **Last Updated**: January 27, 2026
