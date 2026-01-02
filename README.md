# NerdMiner-M5-StickCPlus
Step-by-step guide to flash NerdMiner on M5StickC Plus 1.1
# NerdMiner Setup Guide for M5StickC Plus 1.1

A step-by-step guide to flash NerdMiner v2 firmware onto the M5StickC Plus 1.1 using PlatformIO on Linux.

## Hardware Required
- M5StickC Plus 1.1 (ESP32-PICO-D4)
- USB-C cable
- Linux computer

## Prerequisites

### Install PlatformIO
```bash
# Install pipx (recommended method)
sudo apt install pipx
pipx install platformio
pipx ensurepath

# Restart terminal after installation
```

### Clone NerdMiner Repository
```bash
git clone https://github.com/BitMaker-hub/NerdMiner_v2.git
cd NerdMiner_v2
```

## Known Issue & Fix

There's a compilation error with the DFRobot_GP8XXX library on newer ESP32 cores. You need to fix this before compiling.

### Fix the Library Error

1. Start the initial build (it will fail):
```bash
platformio run -e M5Stick-C-Plus
```

2. Edit the problematic file:
```bash
nano .pio/libdeps/M5Stick-C-Plus/DFRobot_GP8XXX/DFRobot_GP8XXX.cpp
```

3. Find line 303 and change:
```cpp
// FROM:
analogWriteResolution(_pin0,10);

// TO:
analogWriteResolution(10);
```

4. Save and exit (Ctrl+O, Enter, Ctrl+X)

## Build and Flash

### Clean and Rebuild
```bash
platformio run -t clean
platformio run -e M5Stick-C-Plus -t upload
```

**Note:** Make sure your device is:
- Connected via USB
- Powered on
- Detected at `/dev/ttyUSB0` or `/dev/ttyACM0`

## Configuration

### Initial WiFi Setup
1. After flashing, the device will create a WiFi access point
2. Look for network named "NerdMinerAP" or similar
3. Connect to it (default password: "MineYourCoins" or none)
4. Configure your WiFi credentials and Bitcoin address
5. Device will reboot and connect to your network

### Finding Device IP
- Check your router's connected devices
- Or use nmap: `nmap -sn 192.168.1.0/24`
- Or look on the M5Stick display (cycle screens with buttons)

## Device Controls

**M5StickC Plus buttons:**
- **Button A** (front): Change screen/cycle displays
- **Button B** (side): Secondary functions
- **Power button** (left side): Power on/off, hold to enter config mode

## Mining Pools

Popular pools for NerdMiner:
- **public-pool.io** (default, supports low hashrate miners)
- **solo.ckpool.org** (solo mining)

## Important Notes

⚠️ **This is an educational/lottery mining project**
- Hash rate: ~40-50 kH/s
- Chance of finding a block: astronomically small
- Power consumption > potential earnings
- Purpose: Learn about Bitcoin mining, not profit

## Troubleshooting

### Device won't boot after flashing
- Hold power button for 5-10 seconds
- Try resetting while plugged into USB
- Verify you used the correct environment (M5Stick-C-Plus, not M5Stick-C-Plus2)

### Compilation errors
- Make sure you applied the DFRobot library fix
- Try cleaning: `platformio run -t clean`
- Check that ESP32 platform is installed

### Can't find device IP
- Use `nmap` to scan your network
- Check router admin panel
- Press buttons on M5Stick to cycle through info screens

## Hardware Compatibility

**M5StickC Plus 1.1:**
- Use environment: `M5Stick-C-Plus`
- Chip: ESP32-PICO-D4

**M5StickC Plus 2:**
- Use environment: `M5Stick-C-Plus2`
- Chip: ESP32-PICO-V3-02
- **Different hardware - not interchangeable!**

## Resources

- [NerdMiner GitHub](https://github.com/BitMaker-hub/NerdMiner_v2)
- [PlatformIO Documentation](https://docs.platformio.org/)
- [M5Stack Documentation](https://docs.m5stack.com/)

## License

This guide is provided as-is. NerdMiner v2 is developed by BitMaker-hub and contributors.

---

**Happy mining! 🎰⛏️**
