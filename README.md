
# Code Commenting and Documentation Standards

## Table of Contents

1. [Purpose](#1-purpose)  
2. [Technical and Business Context](#2-technical-and-business-context)  
3. [General Commenting Guidelines](#3-general-commenting-guidelines)  
4. [Language-Specific Standards](#4-language-specific-standards)  
   - [Python](#python)  
   - [JavaScript](#javascript)  
   - [HTML](#html)  
   - [Modbus](#modbus)  
   - [Socket.IO](#socketio)  
5. [Documentation Standards](#5-documentation-standards)  
6. [End-to-End Commenting Example](#6-end-to-end-commenting-example)  
7. [Linting and Style Enforcement](#7-linting-and-style-enforcement)  
8. [Testing and Documentation](#8-testing-and-documentation)  
9. [Summary](#9-summary)  
10. [Contact](#10-contact)  
11. [License](#11-license)

---

## 1. Purpose

This document defines the standards for commenting and documenting code across systems using Python, JavaScript, HTML, Modbus, and Socket.IO. It aims to ensure the codebase is understandable, maintainable, and scalable by any engineer, regardless of original authorship.

---

## 2. Technical and Business Context

Poorly documented code increases long-term risk. This applies not only to developers but also to stakeholders and investors.

**Technical Benefits**:
- Faster onboarding
- Easier debugging and handoffs
- Increased code longevity

**Business and Operational Benefits**:
- Reduces reliance on individual experts
- Avoids critical knowledge silos
- Supports due diligence in funding or acquisition events
- Demonstrates engineering maturity and risk mitigation to shareholders

---

## 3. General Commenting Guidelines

| Principle | Description |
|----------|-------------|
| Clarity over Cleverness | Code and comments should be easy to read |
| Explain “Why” | Comments should explain context or reasoning |
| Keep Comments Updated | Remove outdated or misleading comments |
| Avoid Redundancy | Don’t restate what code obviously does |
| Use Docstrings | Document all public methods and modules with proper docstrings |

---

## 4. Language-Specific Standards

### Python

```python
# Connect to Modbus device
client = ModbusTcpClient('192.168.1.100', port=502)

# Convert from tenths of a degree Celsius
temperature = raw / 10.0
````

```python
def read_temperature():
    """
    Reads temperature from Modbus register.

    Returns:
        float: Temperature in Celsius.
    Raises:
        ConnectionError: If read fails.
    """
```

---

### JavaScript

This standard assumes use of vanilla JavaScript. For frameworks like React or Vue, follow respective documentation conventions (e.g., JSDoc, PropTypes, or TypeScript).

```javascript
// Connect to the Socket.IO server
const socket = io();

// Display the latest temperature
socket.on('temperature_update', (data) => {
    document.getElementById('temp-display').textContent = `${data.temp} °C`;
});
```

---

### HTML

```html
<!-- Container for real-time temperature display -->
<div id="dashboard">
    <h2>Live Temperature</h2>
    <p id="temp-display">Waiting for data...</p>
</div>
```

---

### Modbus

```python
# Read register 40001 (temperature in tenths of degrees)
raw = client.read_holding_registers(0, 1).registers[0]
temperature = raw / 10.0
```

---

### Socket.IO

```javascript
// Request data from backend
socket.emit('request_sensor_data');

// Handle incoming data
socket.on('temperature_update', (data) => {
    updateTemperatureDisplay(data.temp);
});
```

---

## 5. Documentation Standards

Every project should include a properly structured `README.md` with:

* Project overview
* Architecture summary
* Business value
* Technology stack
* Setup instructions
* Contact or ownership details

<details>
<summary>Click to view sample README structure</summary>

```
# Smart Monitoring System

## Overview
A real-time monitoring system using Modbus and Socket.IO.

## Architecture
- Python backend (Flask + pymodbus + Socket.IO)
- JavaScript frontend (vanilla)
- HTML/CSS interface

## Setup
pip install -r requirements.txt  
python server.py

## Contact
Industrial Engineering Team  
iot.support@company.com
```

</details>

---

## 6. End-to-End Commenting Example

### Python + Socket.IO

```python
@socketio.on('request_sensor_data')
def handle_request():
    """
    Handles frontend request for temperature data.

    Emits:
        'temperature_update': Contains the latest temperature reading.
    """
    try:
        raw = client.read_holding_registers(0, 1).registers[0]
        temperature = raw / 10.0
        emit('temperature_update', {'temp': temperature})
    except Exception:
        emit('error', {'message': 'Sensor read failed'})
```

### JavaScript Frontend

```javascript
// Listen for server update and display the temperature
socket.on('temperature_update', (data) => {
    document.getElementById('temp-display').textContent = `${data.temp} °C`;
});
```

### HTML Structure

```html
<!-- Display block for temperature -->
<div class="sensor-widget">
    <h3>Temperature</h3>
    <p id="temp-display">--</p>
</div>
```

---

## 7. Linting and Style Enforcement

Use automated tools to enforce consistency and detect errors before they reach production.

**Python**

* `black` – Code formatting
* `flake8`, `pylint` – Linting and metrics
* `pydocstyle` – Docstring enforcement

**JavaScript**

* `eslint` – Linting
* `prettier` – Auto-formatting

**Markdown/Docs**

* `markdownlint` – Linting for `.md` files
* Recommended: pre-commit hooks and CI checks (e.g., GitHub Actions)

---

## 8. Testing and Documentation

Tests should be written and documented clearly. Use inline comments and docstrings to explain purpose, setup, and edge cases.

```python
def test_temp_within_bounds():
    """Ensure temperature remains within safe operating limits."""
    ...
```

Well-documented tests improve reliability, onboarding, and traceability during debugging or audits.

---

## 9. Summary

* Commenting and documentation reduce risk and improve efficiency
* Standards help avoid knowledge silos and increase transparency
* Tools and CI enforce consistency automatically
* Well-documented tests and APIs support scale and handoffs
* Clarity in code is a long-term investment in product and team success

---

## 10. Contact

For questions about this standard or documentation support, contact:

**Engineering Lead**
**Industrial IoT Team**
**[iot.support@company.com](mailto:iot.support@company.com)**

---

## 11. License

This documentation standard is internal intellectual property of \[Your Company Name]. Redistribution is not permitted without written approval.

```


