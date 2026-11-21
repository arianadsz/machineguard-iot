# MachineGuard: Smartphone-Based Machine Health Monitoring

**Course:** IDM 401 — Smart Manufacturing Systems  
**Student:** [Your full name]  
**Student ID:** [Your student ID]  
**Working arrangement:** Individual project — subject to instructor approval  

## 1. Use case and industrial decision

**Decision sentence:** When vibration or sound around a machine becomes unusually high, the maintenance team receives an alert and inspects the machine before a possible failure.

MachineGuard is an educational predictive-maintenance prototype. An iPhone is used as a portable sensor node. Its accelerometer provides motion measurements and its microphone provides a relative sound-level measurement. A Mac receives the measurements and displays the machine condition, trends, alerts and device controls.

The system is intended to demonstrate how sensor data can support a maintenance decision. It does not diagnose a bearing fault and must not be used as a real industrial safety device.

## 2. Four-layer architecture

| Layer | Implementation |
|---|---|
| **Layer 4 — Device** | iPhone Safari reads accelerometer motion in m/s² and microphone amplitude as dBFS. The phone displays a warning lamp and plays a short browser tone as an on-screen/audio actuator. |
| **Layer 3 — Network** | The phone publishes JSON telemetry to an MQTT topic using secure WebSockets. The Mac subscribes to telemetry and acknowledgements. The Mac publishes commands; the phone subscribes to the command topic. Messages are timestamped and logged. |
| **Layer 2 — Service** | Two user-adjustable threshold rules compare vibration RMS and sound level against selected limits. A threshold violation creates a timestamped alert and sends an alarm command to the phone. |
| **Layer 1 — Content** | The Mac dashboard shows live readings, a trend chart, message history, alerts, threshold sliders and command buttons. The phone acknowledges commands. |

**Message topics**
- `idm401/machineguard-demo-7f3c91/telemetry` — phone sensor readings
- `idm401/machineguard-demo-7f3c91/command` — dashboard-to-phone commands
- `idm401/machineguard-demo-7f3c91/ack` — phone acknowledgements

**Data example:** `{"vibration":0.84,"sound":-31.2,"units":{"vibration":"m/s²","sound":"dBFS"},"source":"iPhone Safari","time":"ISO timestamp"}`

## 3. Sensors and rules

| Input | Source | Displayed unit | Rule / purpose |
|---|---|---|---|
| Vibration | iPhone motion sensor | m/s² | Alert when the reading exceeds the adjustable vibration threshold (initially 1.2 m/s²). |
| Sound | iPhone microphone | dBFS | Alert when the reading exceeds the adjustable sound threshold (initially −25 dBFS). |

The vibration value is calculated from the phone's motion acceleration. When only acceleration including gravity is available, the code estimates dynamic movement by subtracting the approximate gravity magnitude (9.81 m/s²). This is a demonstration estimate, not a calibrated vibration instrument. The microphone's waveform RMS is converted to dBFS using `20 × log10(RMS)`. The raw audio stays in the browser; only the calculated level is transmitted.

The thresholds are initial demonstration settings and must be tuned after observing the actual phone's readings. The rules include a five-second alert cooldown to prevent repeated alerts from firing continuously.

## 4. Tests and results

**Important:** Complete this table after testing on the actual iPhone and Mac. Do not enter a pass result unless you personally observed it.

| Test | Procedure | Actual result |
|---|---|---|
| HTTPS and permissions | Open the published HTTPS page in iPhone Safari; tap Start; allow Motion and Microphone. | [Record result] |
| Live vibration | Gently move the phone and observe vibration values on the Mac. | [Record result] |
| Live sound | Speak or clap near the phone and observe sound-level changes. | [Record result] |
| Vibration rule | Lower the threshold and move the phone until an alert fires. | [Record result] |
| Sound rule | Lower the sound threshold and make a sound until an alert fires. | [Record result] |
| Actuator and command | Use Test alarm and Start/Stop sensing on the Mac; check the phone lamp/tone and acknowledgement. | [Record result] |
| Message log | Confirm topic names, message content and timestamps appear. | [Record result] |
| Offline behaviour | Disconnect the phone's network, observe the queue/disconnected state, reconnect and inspect delivery. | [Record result] |

## 5. Limitations and future improvements

- Smartphone accelerometers are not calibrated industrial vibration sensors. Phone placement, orientation and device model affect readings.
- dBFS is a relative digital signal level, not calibrated dB SPL. Microphone sensitivity and automatic gain control vary between phones.
- The public MQTT broker is shared and is suitable only for a classroom prototype. Messages are not private; no personal information is sent.
- Mobile browsers may suspend background activity. The sensor page should remain open during the demonstration.
- Internet or broker outages may interrupt live delivery. The prototype attempts to queue sensor messages while disconnected and flush them after reconnection; this behaviour must be tested and documented.
- A production version would use calibrated industrial sensors, a private authenticated broker, persistent storage, secure access control, and validated fault-detection logic.

## 6. AI and external resources disclosure

ChatGPT (OpenAI) was used to help plan the architecture, generate an initial HTML/CSS/JavaScript implementation, and prepare explanatory documentation. The student must review, test, understand and adapt the generated work, and retain this prompt log. The project uses the MQTT.js browser library, Chart.js, and the EMQX public MQTT broker. Add the actual library and broker URLs used in the final submitted version.

**Sources:**
- Course project brief, IDM 401 IoT App Project, especially slides 2, 5–8, 12–14 and 16–20.
- EMQX public MQTT broker connection details: https://www.emqx.com/en/mqtt/public-mqtt5-broker
- MQTT.js browser library: https://github.com/mqttjs/MQTT.js
- Chart.js: https://www.chartjs.org/
- GitHub Pages HTTPS documentation: https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https
