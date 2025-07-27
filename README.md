# <h1 align="center"> 🚀 ESP32 MQTT Control Dashboard</h1>
<p align="center"><em>A modern, responsive web interface for controlling ESP32 devices via MQTT protocol. This project provides real-time LED control through a beautiful dashboard with comprehensive documentation and simulation support.</em></p>

<p align="center"> <img src="https://img.shields.io/badge/C++-ESP32-blue?style=for-the-badge&logo=arduino" /> <img src="https://img.shields.io/badge/HTML-Web%20UI-orange?style=for-the-badge&logo=html5" /> <img src="https://img.shields.io/badge/JavaScript-Control-green?style=for-the-badge&logo=javascript" /> <img src="https://img.shields.io/badge/MQTT-Protocol-purple?style=for-the-badge&logo=mqtt" /> </p>

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Demo](#demo)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [File Structure](#file-structure)
- [Configuration](#configuration)
- [API Reference](#api-reference)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

This project consists of two main components:
1. **ESP32 Arduino Code** - Handles WiFi connection, MQTT communication, and LED control
2. **Web Dashboard** - Modern interface for remote control with real-time feedback

The system uses MQTT protocol for reliable communication between the web interface and ESP32 device, allowing real-time control of connected LEDs.

## ✨ Features

### 🎨 Web Interface
- **Modern Design** - Glassmorphism UI with gradient backgrounds
- **Real-time Control** - Instant LED on/off commands
- **Connection Monitoring** - Live MQTT connection status
- **Message Logging** - Real-time command and response tracking
- **Responsive Design** - Works on desktop, tablet, and mobile
- **Keyboard Shortcuts** - Quick control with Ctrl+1/Ctrl+2
- **Auto-reconnect** - Automatic connection recovery
- **Visual Feedback** - Animated buttons and status indicators

### 🔧 ESP32 Features
- **WiFi Connectivity** - Automatic connection to specified network
- **MQTT Communication** - Reliable message handling
- **LED Control** - GPIO pin control for external LEDs
- **Auto-reconnect** - Automatic MQTT broker reconnection
- **Serial Monitoring** - Debug output for troubleshooting

### 📚 Documentation
- **Comprehensive Manual** - Built-in user guide
- **Troubleshooting Guide** - Common issues and solutions
- **Technical Specifications** - Complete system details
- **Code Reference** - Function documentation

## 🎮 Demo

### Live Simulation
Test the system without physical hardware:
```Wokwi Simulation
https://wokwi.com/projects/418425453311975425
```

### How to Test:
1. Click the simulation link above
2. Press the green "Start Simulation" button in Wokwi
3. Open the web interface
4. Wait for "Connected" status
5. Use the control buttons to test LED functionality

## 📋 Requirements

### Hardware
- ESP32 development board
- LED (connected to GPIO pin 5)
- Resistor (220Ω recommended for LED)
- Breadboard and jumper wires
- USB cable for programming

### Software
- Arduino IDE (1.8.x or 2.x)
- ESP32 board package for Arduino
- Required Arduino libraries:
  - `WiFi.h` (built-in)
  - `PubSubClient.h`

### Web Browser
- Modern browser with WebSocket support
- Chrome, Firefox, Safari, or Edge (latest versions)
- Internet connection for MQTT broker access

## 🚀 Installation

### 1. ESP32 Setup

#### Install Required Libraries
```bash
# In Arduino IDE, go to Tools > Manage Libraries
# Search and install:
- PubSubClient by Nick O'Leary
```

#### Upload Arduino Code
1. Open Arduino IDE
2. Copy the ESP32 code from the project
3. Select your ESP32 board: `Tools > Board > ESP32 Dev Module`
4. Select the correct port: `Tools > Port`
5. Upload the code to your ESP32

#### Hardware Connections
```
ESP32 Pin    Component
---------    ---------
GPIO 5   →   LED Anode (long leg)
GND      →   LED Cathode (via 220Ω resistor)
```

### 2. Web Interface Setup

#### Option 1: Direct File Access
1. Download all project files
2. Open `index.html` in your web browser
3. The interface will automatically connect to the MQTT broker

#### Option 2: Local Web Server
```bash
# Using Python
python -m http.server 8000 
```
```
# Using Node.js
npx http-server
```
Then open: http://localhost:8000

#### Option 3: GitHub Pages
1. Fork this repository
2. Enable GitHub Pages in repository settings
3. Access via: `https://ficrammanifur/Esp32-mqtt-project`

## 🎯 Usage

### Basic Operation

1. **Power on ESP32** - Connect to power source
2. **Check Serial Monitor** - Verify WiFi and MQTT connection
3. **Open Web Interface** - Load the dashboard in your browser
4. **Wait for Connection** - Green "Connected" status should appear
5. **Control LED** - Use ON/OFF buttons to control the LED

### Keyboard Shortcuts
- `Ctrl + 1` - Turn LED ON
- `Ctrl + 2` - Turn LED OFF

### Status Indicators
- 🟢 **Connected** - Ready to send commands
- 🟡 **Connecting** - Establishing connection
- 🔴 **Error** - Connection failed
- ⚪ **Disconnected** - No connection

## 📁 File Structure

```
esp32-mqtt-control/
├── README.md                # Project documentation
├── esp32_code.ino           # Arduino code for ESP32
├── index.html               # Main web interface
├── main.js                  # JavaScript MQTT client
├── style.css                # Styling and animations
├── docs/                    # Additional documentation
│   ├── hardware-setup.md    # Hardware connection guide
│   ├── troubleshooting.md   # Detailed troubleshooting
│   └── api-reference.md     # MQTT API documentation
└── assets/                  # Images and resources
    ├── screenshots/         # Interface screenshots
    └── diagrams/            # Circuit diagrams
```

## ⚙️ Configuration

### ESP32 Configuration
```cpp
// WiFi Settings
const char* ssid = "Your_WiFi_Name";
const char* password = "Your_WiFi_Password";

// MQTT Settings
const char* mqttServer = "broker.emqx.io";
int port = 1883;
char clientId[50] = "PACEE112233";

// Pin Configuration
const int LED = 4;      // Main LED pin
const int pinGreen = 5; // Controlled LED pin
```

### Web Interface Configuration
```javascript
// MQTT Configuration
const MQTT_BROKER = "wss://broker.emqx.io:8084/mqtt"
const MQTT_TOPIC = "OpenCV-IoT6601"
```

### Custom MQTT Broker
To use your own MQTT broker:

1. **ESP32 Code**: Change `mqttServer` variable
2. **Web Interface**: Update `MQTT_BROKER` in `main.js`
3. **Ensure WebSocket support** on your broker

## 📡 API Reference

### MQTT Topics
| Topic | Direction | Payload | Description |
|-------|-----------|---------|-------------|
| `OpenCV-IoT6601` | Web → ESP32 | `"ON"` | Turn LED on |
| `OpenCV-IoT6601` | Web → ESP32 | `"OFF"` | Turn LED off |
| `OpenCV-IoT6601` | ESP32 → Web | `"ON"` | LED status confirmation |
| `OpenCV-IoT6601` | ESP32 → Web | `"OFF"` | LED status confirmation |

### JavaScript Functions
```javascript
// Send command to ESP32
sendCommand("ON")   // Turn LED on
sendCommand("OFF")  // Turn LED off

// Connection management
connectToMQTT()     // Establish MQTT connection
retryConnection()   // Retry failed connection
```

### Arduino Functions
```cpp
void wifiConnect()     // Connect to WiFi
void mqttReconnect()   // Connect to MQTT broker
void callback()        // Handle incoming messages
```

## 🔧 Troubleshooting

### Common Issues

#### 1. ESP32 Not Connecting to WiFi
**Symptoms**: Serial monitor shows connection dots indefinitely
**Solutions**:
- Verify WiFi credentials in code
- Check WiFi network availability
- Ensure ESP32 is within WiFi range
- Try different WiFi network (2.4GHz only)

#### 2. MQTT Connection Failed
**Symptoms**: "Connection Error" status in web interface
**Solutions**:
- Check internet connection
- Verify MQTT broker URL
- Disable VPN or proxy
- Try different browser
- Check firewall settings

#### 3. LED Not Responding
**Symptoms**: Commands sent but LED doesn't change
**Solutions**:
- Verify LED wiring (GPIO 5)
- Check LED polarity
- Test with multimeter
- Verify resistor value (220Ω)
- Check ESP32 power supply

#### 4. Web Interface Not Loading
**Symptoms**: Blank page or connection errors
**Solutions**:
- Enable JavaScript in browser
- Clear browser cache
- Try incognito/private mode
- Check browser console for errors
- Use different browser

### Debug Mode

#### ESP32 Serial Monitor
```cpp
// Add to setup() for verbose debugging
Serial.setDebugOutput(true);
```

#### Web Console Debugging
```javascript
// Open browser developer tools (F12)
// Check Console tab for error messages
console.log("Debug information here");
```

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork the repository**
2. **Create feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open Pull Request**

### Development Guidelines
- Follow existing code style
- Add comments for complex logic
- Test on multiple browsers
- Update documentation as needed
- Include screenshots for UI changes

### Reporting Issues
Please include:
- Operating system and browser version
- ESP32 board model
- Complete error messages
- Steps to reproduce
- Screenshots if applicable

## 🪪 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
<p align="center">
  <a href="https://github.com/ficrammanifur/Control-Motor-With-DABBLE-APP/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue" alt="License: MIT" />
  </a>
</p>

## 🙏 Acknowledgments

- **EMQX** for providing free MQTT broker service
- **Wokwi** for online ESP32 simulation platform
- **Arduino Community** for extensive libraries and support
- **MQTT.js** for reliable WebSocket MQTT client
- **Font Awesome** for beautiful icons
- **Google Fonts** for typography

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/ficrammanifur/esp32-mqtt-control/issues)
- **Discussions**: [GitHub Discussions](https://github.com/ficrammanifur/esp32-mqtt-control/discussions)
- **Email**: ficramm@gmail.com

## 🔗 Links

- [🎮 Live Demo (Wokwi)](https://wokwi.com/projects/418425453311975425)
- [📚 Documentation](https://github.com/ficrammanifur/esp32-mqtt-control/wiki)
- [🐛 Report Bug](https://github.com/ficrammanifur/esp32-mqtt-control/issues/new?template=bug_report.md)
- [💡 Request Feature](https://github.com/ficrammanifur/esp32-mqtt-control/issues/new?template=feature_request.md)

---

<div align="center">

**⭐ Star this repository if you found it helpful!**

Made with ❤️ for the IoT community

[⬆ Back to Top](#-esp32-mqtt-control-dashboard)
</div>
