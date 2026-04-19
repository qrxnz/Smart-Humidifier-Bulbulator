# Bulbulator – Smart Humidifier Controller 💧

This project is a simple DIY smart humidifier controller that keeps your room humidity at a desired level.  
It uses a DHT11 sensor to monitor humidity, a 16x2 LCD to display current and target values, and two buttons for setting the target humidity.  
The humidifier is switched on and off automatically via a relay or NPN transistor.

---

## ❔ How It Works

- Press **Button UP** to increase the target humidity value (displayed on LCD).
- Press **Button SET** to confirm the target humidity.
- The DHT11 sensor continuously reads the room humidity.
- If the current humidity falls below the target, the humidifier is turned on.
- Once the target humidity is reached, the humidifier turns off automatically.
- The LCD shows the live humidity and the set target.

---

## ⭐ Features

- Simple two-button interface to set humidity target
- Real-time display of current and target humidity on 16x2 LCD
- Automatic humidifier control NPN transistor
- Easy to build and customize
- Low power consumption — humidifier runs only when needed

---

## 🧰 Components

- **Wemos D1 Mini (ESP8266)** – Microcontroller (can also be adapted for Arduino Uno)
- **DHT11** – Humidity and temperature sensor
- **16x2 or 20x4 LCD I2C** – Humidity display
- **NPN Transistor** – Controls humidifier power
- **Humidifier (DIY1 v2.0)** – Ultrasonic module
- **2x Push Buttons** – For setting and confirming humidity
- **LEDs (optional)** – Status indicators
- **Power source** – USB or 5V–12V
- **Capacitor 470μF** – Power supply stabilizer
- **Resistors, wires** – Basic electronic components

---

## 🔌 Wiring Diagram

![Diagram](./.github/assets/CircuitDiagram.png)

---

## 🖥️ Usage

### ⚙️ Hardware Setup

1. Connect all components according to the wiring diagram.
2. Power the system via USB or an external 5V source.
3. Use **Button UP** to set your desired humidity target.
4. Press **Button SET** to confirm.
5. The Bulbulator will monitor the humidity and control the humidifier accordingly.
6. Check current and target humidity on the LCD.

### 🚀 Building and Uploading

#### Option A: Using Arduino IDE

1. Open `bulbulator/bulbulator.ino`.
2. Install required libraries: `LiquidCrystal_I2C`, `DHT11`.
3. Select your board (e.g., **LOLIN(WEMOS) D1 R2 & mini**).
4. Click **Upload**.

#### Option B: Using CLI (Recommended for Linux/macOS)

This project uses a `flake.nix` to provide a reproducible development environment.

1. **Enter the development shell:**

   ```bash
   nix develop
   ```

   _This will automatically install `arduino-cli`, `make`, and all required dependencies._

2. **Compile the project:**

   ```bash
   cd bulbulator
   make compile
   ```

3. **Upload to your board:**

   ```bash
   # Find your serial port first:
   arduino-cli board list

   # Then upload (adjusting SERIAL port if needed)
   make upload SERIAL=/dev/ttyUSB0
   ```

   _Note: If it's your first time, you might need to install the platforms and libraries specified in `sketch.yaml` by running `arduino-cli core update-index` and then `arduino-cli compile --install --profile bulbulator`._

4. **Monitor serial output:**
   ```bash
   make monitor
   ```

---

## ⚖ Pros and Cons

### ✅ Pros

- Simple and easy-to-build design.
- Clear real-time feedback on LCD (current and target humidity).
- Easy to customize (different sensors, displays, or control modules can be used).

### ❌ Cons

- **Sensor placement:** The DHT11 was mounted too close to the humidifier outlet, causing it to saturate with steam and give unreliable readings.
- **No hysteresis:** The control logic switches the humidifier on/off immediately at the threshold, leading to frequent toggling.
- **Power supply instability:** With a long USB power cable, the LCD sometimes lost power or flickered when the humidifier module turned on due to voltage drops.
- **No water level monitoring:** There’s no way to check the humidifier’s water level, which can lead to running dry.

---

## 📚 Libraries

- **Wire.h**  
  Handles I2C communication – required for the LCD display (and any other I2C devices).

- **LiquidCrystal_I2C.h**  
  Library for controlling the 16x2 LCD via the I2C interface – makes it easy to print text and numbers.

- **DHT.h** (or **Dht11.h**, depending on the version you use)  
  Used to read humidity and temperature values from the DHT11 sensor.

---

### Made with 💙 by [Oliwier Gramala]
