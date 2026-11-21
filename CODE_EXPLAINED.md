# MachineGuard code explained simply

## The big picture

The HTML file contains three parts:
- **HTML** makes the dashboard cards, buttons, graph area, sensor values and logs.
- **CSS** controls the colours, spacing and responsive layout.
- **JavaScript** reads sensors, connects to MQTT, applies rules and updates the screen.

## Important code ideas

### 1. Project topics
`PROJECT_KEY` is the shared project name. The three topics are the message addresses:
- `telemetry`: phone sends sensor values to Mac.
- `command`: Mac sends a command to phone.
- `ack`: phone confirms it received the command.

Both devices must use the same project key or they will not meet in the same message topics.

### 2. MQTT connection
`connectMQTT()` connects the browser to the broker using secure WebSockets. When connected, the client subscribes to the topics it needs. The Mac subscribes to telemetry and acknowledgements. The phone subscribes to commands.

MQTT is publish/subscribe messaging. A publisher sends a message to a topic. A subscriber listening to that topic receives it. The broker is the middle server that routes messages.

### 3. Reading the accelerometer
`startPhoneSensors()` asks for motion permission after the user taps the Start button. The `devicemotion` event provides acceleration. The code calculates the magnitude of the three axes:

`magnitude = sqrt(x² + y² + z²)`

If the browser provides acceleration without gravity, the magnitude is used. If it only provides acceleration including gravity, the code subtracts approximately 9.81 m/s² to estimate movement. This is a simplified demonstration estimate.

### 4. Reading the microphone
The browser asks for microphone permission using `getUserMedia()`. An `AnalyserNode` reads audio samples in the browser. The code calculates RMS (root mean square), then converts it to dBFS:

`dBFS = 20 × log10(RMS)`

RMS measures the average size of the waveform. The audio itself is not published; only the calculated number is sent.

### 5. Sending sensor data
Every second, the phone sends a JSON message containing vibration, sound and units to the telemetry topic. The message also receives a timestamp.

### 6. Applying rules
`handleTelemetry()` runs on the Mac when a telemetry message arrives. It compares vibration and sound against the slider values. If a value is over its threshold, it creates a timestamped alert and sends an alarm command. A five-second cooldown prevents the same alert from firing on every incoming sample.

### 7. Sending a command and confirming it
The Mac's buttons call `publishCommand()`. The phone receives the command in `handleCommand()`, performs the requested action and publishes an acknowledgement to the ack topic. The Mac displays the confirmation.

### 8. The actuator
`activateAlarm()` lights the phone's warning lamp and plays a short tone. This is the prototype's on-screen/audio actuator. It is not a physical industrial machine stop.

### 9. The graph
Chart.js draws the sensor trend. The dashboard keeps the latest 30 samples so the graph stays readable.

### 10. Offline queue
If the phone cannot publish telemetry because the broker is disconnected, the message is placed in `pending`. When MQTT reconnects, `flushQueue()` sends the queued messages. The real behaviour must be demonstrated and recorded; mobile browser suspension or broker/network restrictions may affect it.

## Key terms

- **Sensor:** a component that measures something in the real world.
- **Actuator:** an output that performs an action, such as a lamp or buzzer.
- **Telemetry:** measurement data sent by a device.
- **MQTT broker:** the server that routes messages between publishers and subscribers.
- **Topic:** the message address used by MQTT.
- **Threshold:** a limit used by a rule to decide when to raise an alert.
- **RMS:** root mean square; a way to measure the effective size of a changing signal.
- **dBFS:** decibels relative to digital full scale; a relative digital audio level, not calibrated sound pressure in dB SPL.
- **Acknowledgement (ack):** a message confirming that a command was received.
