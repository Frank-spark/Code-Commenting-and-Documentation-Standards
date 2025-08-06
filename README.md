
# Code Commenting and Documentation Standards

## Purpose

This document defines a comprehensive and language-agnostic standard for commenting and documenting code across all environments used within the company.

Whether your team is building real-time APIs, hardware-integrated firmware, mobile applications, internal data tooling, or analytics dashboards, the expectation is the same:

- **All code must be documented**
- **All logic must be explained**
- **All repositories must include clear and complete README files**

This document serves multiple purposes:

- To guide developers in best practices that improve clarity and maintainability
- To set expectations for technical leadership and review processes
- To help executives understand how code quality translates to risk reduction and organizational strength
- To ensure codebases can be confidently evaluated by investors, acquirers, and audit teams

---

## Why Documentation Matters

Code is a strategic asset. When that asset is undocumented or inconsistently documented, it becomes a liability.

Lack of code documentation leads to:

- Lost knowledge when engineers leave
- Slowed onboarding and team velocity
- Fragile systems that only one person understands
- Technical debt that cannot be tracked or prioritized
- Failed audits or delayed funding rounds
- Higher long-term cost of ownership

Well-documented code, by contrast, enables:

- Seamless transitions between engineers
- Faster diagnosis of production issues
- Cross-functional collaboration between dev, QA, ops, and business teams
- Trust and transparency in external reviews
- Sustainable velocity for fast-scaling companies

---

## Company-Wide Policy

| Area | Requirement |
|------|-------------|
| Code Comments | All non-trivial logic must be explained via inline or block comments |
| Function Documentation | All public methods, classes, APIs, or components must include formal documentation |
| README.md | All repositories must include a properly structured `README.md` that communicates the business and technical purpose |
| Test Clarity | Tests must clearly describe what they are verifying and why |
| Tooling | Linting, formatting, or CI rules should enforce as many of these standards as possible |

---

## General Commenting Guidelines

| Principle | Description |
|----------|-------------|
| Explain the “Why” | Comments should explain intent and context, not just what the code does |
| Use Natural Language | Write full sentences. Don’t rely on shorthand or cryptic notes |
| Keep Comments Up to Date | Update or delete comments when the code changes |
| Avoid Redundant Comments | Don’t restate the code — add value by explaining purpose, edge cases, trade-offs |
| Standardize Formats | Use docstring conventions or structured headers in supported languages |

---

## README Expectations

Every repository should contain a `README.md` file with the following sections:

- **Overview** – One paragraph explaining what the system does
- **Architecture** – Components, data flow, integrations
- **Business Purpose** – Why this system exists and who it serves
- **Setup Instructions** – Local install/run/test commands
- **Environments** – Expected runtime, OS, infrastructure
- **Contact** – Who owns or supports the codebase

See [Sample README Template](#sample-readme-template) below.

---

## Language-Specific Commenting Examples

### Python

```python
def read_temperature(sensor_id: int) -> float:
    """
    Reads the temperature in Celsius from a sensor over Modbus.

    Args:
        sensor_id (int): Sensor register ID

    Returns:
        float: Temperature in degrees Celsius
    """
    raw = client.read_holding_registers(sensor_id, 1).registers[0]
    return raw / 10.0
````

---

### JavaScript

```javascript
// Fetch temperature from API and update the DOM
async function updateTemperatureDisplay() {
    const res = await fetch('/api/temp');
    const { temp } = await res.json();
    document.getElementById('temp').textContent = `${temp} °C`;
}
```

---

### HTML

```html
<!-- UI block to display live sensor temperature -->
<section id="temp-block">
    <h2>Temperature</h2>
    <p id="temp">-- °C</p>
</section>
```

---

### TypeScript

```typescript
/**
 * Converts Celsius to Fahrenheit
 * @param celsius - temperature in Celsius
 * @returns temperature in Fahrenheit
 */
function toFahrenheit(celsius: number): number {
    return (celsius * 9) / 5 + 32;
}
```

---

### Rust

```rust
/// Converts raw sensor data to degrees Celsius
/// Sensor values are in tenths of a degree
fn convert(raw: i16) -> f32 {
    raw as f32 / 10.0
}
```

---

### C

```c
// Converts ADC value to temperature in Celsius
float convert_to_celsius(int adc_value) {
    return (adc_value * 5.0 / 1024.0) * 100.0;
}
```

---

### C++

```cpp
/**
 * Converts raw temperature from sensor
 * @param raw - raw sensor value
 * @return float - temperature in Celsius
 */
float convertTemperature(int raw) {
    return (raw * 5.0f / 1024.0f) * 100.0f;
}
```

---

### Java

```java
/**
 * Converts Celsius to Fahrenheit
 * @param celsius Temperature in Celsius
 * @return Temperature in Fahrenheit
 */
public double toFahrenheit(double celsius) {
    return (celsius * 9/5) + 32;
}
```

---

### Go

```go
// Convert Celsius to Fahrenheit
func ToFahrenheit(celsius float64) float64 {
    return (celsius * 9 / 5) + 32
}
```

---

### Perl

```perl
# Converts Celsius to Fahrenheit
sub to_fahrenheit {
    my $c = shift;
    return ($c * 9 / 5) + 32;
}
```

---

### Pascal

```pascal
// Convert Celsius to Kelvin
function CelsiusToKelvin(Celsius: Real): Real;
begin
  CelsiusToKelvin := Celsius + 273.15;
end;
```

---

### Bash / Shell Script

```bash
# Restart sensor service and log the result
sudo systemctl restart sensor.service
echo "$(date) Sensor service restarted" >> /var/log/sensors.log
```

---

### SQL

```sql
-- Select active sensors updated in the last 24 hours
SELECT * FROM sensors
WHERE status = 'active'
AND updated_at >= NOW() - INTERVAL '1 day';
```

---

### Ruby

```ruby
# Convert Celsius to Fahrenheit
def to_fahrenheit(celsius)
  (celsius * 9 / 5) + 32
end
```

---

### Swift

```swift
/// Converts Celsius temperature to Fahrenheit
func toFahrenheit(_ celsius: Double) -> Double {
    return (celsius * 9/5) + 32
}
```

---

### Kotlin

```kotlin
/**
 * Converts Celsius to Fahrenheit.
 */
fun toFahrenheit(celsius: Double): Double {
    return (celsius * 9 / 5) + 32
}
```

---

### MATLAB

```matlab
% Convert Celsius to Fahrenheit
function F = toFahrenheit(C)
    F = (C * 9/5) + 32;
end
```

---

### Assembly (x86 NASM)

```asm
; Multiply value in AX by 2 (simulate doubling temperature)
MOV AX, [temp_value]
ADD AX, AX
```

---

## Sample README Template

<details>
<summary>Click to expand</summary>

```
# Device Telemetry Service

## Overview
Service that collects and forwards telemetry from industrial sensors to a central dashboard.

## Architecture
- `collector.py`: connects to devices via Modbus
- `forwarder.js`: sends JSON data to real-time frontend via WebSocket
- `dashboard.html`: live interface

## Business Value
Allows operators to monitor temperature, vibration, and pressure across facilities remotely.

## Setup
- Clone repository
- Run `pip install -r requirements.txt`
- Execute `python collector.py`

## Environment
- Python 3.11+
- Linux-based sensor hosts
- Node.js for frontend service

## Contact
Owner: Engineering Operations  
Email: engops@company.com
```

</details>

---

## Tooling Recommendations

| Language      | Formatters           | Linters            | Doc Tools            |
| ------------- | -------------------- | ------------------ | -------------------- |
| Python        | `black`              | `pylint`, `flake8` | `pydocstyle`, Sphinx |
| JavaScript/TS | `prettier`           | `eslint`           | JSDoc                |
| Rust          | `rustfmt`            | `clippy`           | Rustdoc              |
| C/C++         | `clang-format`       | `cppcheck`         | Doxygen              |
| Java          | `google-java-format` | `checkstyle`       | Javadoc              |
| Go            | `gofmt`              | `golint`           | GoDoc                |
| Shell         | `shfmt`              | `shellcheck`       | Inline comments      |
| SQL           | Manual               | `sqlfluff`         | Inline comments      |
| Perl          | `perltidy`           | `Perl::Critic`     | POD                  |
| Pascal        | Manual               | Manual             | Inline               |

---

## Test Documentation

Tests must describe what they cover and why:

```go
// Ensures overflow condition is handled when input exceeds sensor max range
func TestSensorOverflow(t *testing.T) {
    ...
}
```

```typescript
/**
 * Ensures API returns 400 for invalid temperature format
 */
test('rejects bad input', () => {
  ...
});
```

---

## Audit, Transfer, and Continuity Expectations

Code is not complete until it is documented. This applies to internal handoffs and external evaluations.

Every repository must be ready for:

* **Engineer hand-off**: another dev can take over with no downtime
* **Team transition**: documentation doesn’t rely on tribal knowledge
* **Executive review**: purpose and risks are clearly stated
* **Investor diligence**: systems are demonstrably scalable and maintainable

If documentation fails to communicate clearly, the system is not ready for scale or evaluation.

---

## Contact

**Engineering Standards Committee**
**[engineering.standards@company.com](mailto:engineering.standards@company.com)**

---

## License

This standard is internal IP of \[Your Company Name]. Do not distribute outside the organization without written authorization.

```
```
