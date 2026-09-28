# Firmware for DuinoCoinMiner

## 1. ATmega328P Nodes (`DuinoCoin_Arduino_Slave`)

### Required Arduino Libraries:

Install these libraries in your Arduino IDE via Library Manager or GitHub:

- [DuinoCoin](https://github.com/ricaun/arduino-DuinoCoin) (DUCO-S1A hashing engine)
- [ArduinoUniqueID](https://github.com/ricaun/ArduinoUniqueID) (Chip identifier)
- [StreamJoin](https://github.com/ricaun/StreamJoin) (StreamString for AVR)

### Flashing via ICSP (Connector J1):

1. Use an ISP programmer (e.g. **USBasp** or an **Arduino as ISP**).
2. Install the **[MiniCore](https://github.com/MCUdude/MiniCore)** board package in Arduino IDE:
   - Add `https://mcudude.github.io/MiniCore/package_MCUdude_MiniCore_index.json` to Additional Boards Manager URLs.
3. In **Tools** menu select:
   - **Board:** ATmega328P
   - **Clock:** External 20 MHz
   - **BOD:** 2.7V (or 4.3V)
   - **Compiler LTO:** Enabled
4. Click **Tools -> Burn Bootloader** to set the correct fuses for the 20MHz crystal.
5. Open `firmware/DuinoCoin_Arduino_Slave/DuinoCoin_Arduino_Slave.ino` and click **Sketch -> Upload Using Programmer**.

---

## 2. Master (`DuinoCoin_Esp_Async_Master`)

### Configuration:

Open `firmware/DuinoCoin_Esp_Async_Master/DuinoCoin_Esp_Async_Master.ino` and set:

```cpp
const char* ssid          = "Your_WiFi_SSID";      // Your Wi-Fi network name
const char* password      = "Your_WiFi_Password";  // Your Wi-Fi network password
const char* ducouser      = "Your_Username";       // Your Duino-Coin wallet username
const char* rigIdentifier = "DuinoMiner-6x";       // Custom name shown in web dashboard
```

### Required Arduino Libraries:

- [ArduinoJson](https://github.com/bblanchon/ArduinoJson) (v6.x)
- [AsyncTCP](https://github.com/me-no-dev/AsyncTCP)
- [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)

### Flashing via USB-C:

1. Connect the Seeed Studio XIAO ESP32-C3 directly via USB-C to your computer.
2. In Arduino IDE:
   - Board: **XIAO_ESP32C3** (from Seeed Studio ESP32 boards package or official ESP32 by Espressif)
   - Port: Select the corresponding COM port
3. Click **Upload**.

---

## Upstream Sources & Credits

- **I2C Rig Architecture & Firmware:** [ricaun/DuinoCoinI2C](https://github.com/ricaun/DuinoCoinI2C) (Luiz H. Cassettari)
- **Official Duino-Coin Project:** [revoxhere/duino-coin](https://github.com/revoxhere/duino-coin)
- **Hashing Engine:** [ricaun/arduino-DuinoCoin](https://github.com/ricaun/arduino-DuinoCoin)
- **AVR 20MHz Core:** [MCUdude/MiniCore](https://github.com/MCUdude/MiniCore)
