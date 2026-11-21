# Seven-minute presentation script — MachineGuard

Use this as a guide, not as a script to read without demonstrating. The brief says the live demo is the most important part. Practise with the actual two devices and keep the demo under seven minutes.

## Minute 1 — Use case and decision

“Good morning. My project is MachineGuard, a smartphone-based machine health monitoring prototype. The industrial decision is: when vibration or sound around a machine becomes unusually high, the maintenance team receives an alert and inspects the machine before a possible failure. I use an iPhone as the sensor node and a Mac as the dashboard. The system follows the four IoT layers: device, network, service and content.”

Show the four-layer diagram in the report.

## Minutes 2–5 — Live demonstration

1. **Device layer:** Show the iPhone sensor page. Explain that the accelerometer measures movement in m/s² and the microphone calculates a relative sound level in dBFS. Tap Start and show the live readings.
2. **Network layer:** Show the Mac's MQTT-connected indicator and message log. Move the phone gently; point to the new telemetry messages and timestamps. Explain that MQTT topics act like message addresses and the broker passes messages between the two devices.
3. **Service layer:** On the Mac, lower the vibration threshold using the slider. Gently move the phone until the rule fires. Show the timestamped alert and the warning lamp/tone on the phone. Repeat with the sound threshold by making a short sound near the phone.
4. **Content and control:** Show the live trend chart. Press Test alarm or Stop sensing on the Mac. Show the command arriving on the phone and the acknowledgement appearing on the Mac.
5. **Offline behaviour:** Briefly disconnect the phone's network. Point out the disconnected state and queue counter. Reconnect and show whether queued messages are delivered. Describe only what actually happens during your test.

## Minutes 6–7 — Questions

Finish with: “This prototype demonstrates how phone sensors, MQTT messaging, adjustable rules and a dashboard can support a maintenance decision. Its readings are not industrially calibrated, so a real deployment would require industrial sensors and a private broker.”

**Important:** The project brief says the demo should be live and under seven minutes. It also asks for a 60–90 second backup video. Record the backup only after the real tests work.
