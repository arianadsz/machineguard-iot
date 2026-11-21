# Likely professor questions and simple answers

**1. What problem does your project solve?**  
It demonstrates how unusual machine vibration or sound can trigger a maintenance alert so a technician can inspect the machine.

**2. Why did you choose these two sensors?**  
Vibration can indicate mechanical movement that is different from normal operation. Sound can provide another warning signal. Both are available in a smartphone, so no external hardware is needed for this prototype.

**3. What are the four layers?**  
Device reads sensors and operates the actuator; Network transfers messages; Service applies rules; Content displays the data and lets the user control the device.

**4. What is MQTT?**  
MQTT is a lightweight publish/subscribe messaging protocol often used in IoT. Devices publish messages to topics, and other devices subscribe to those topics.

**5. What is the broker's job?**  
The broker receives MQTT messages from publishers and forwards them to clients subscribed to the matching topic.

**6. Why use three topics?**  
Telemetry carries readings from phone to Mac, command carries control instructions from Mac to phone, and ack carries the phone's confirmation back to the Mac.

**7. What does RMS mean?**  
RMS means root mean square. It calculates an effective size of a changing signal, which is useful for summarising vibration or audio samples.

**8. What is dBFS?**  
It is a digital audio level relative to the maximum digital signal. It is not the same as a calibrated sound-pressure measurement in dB SPL.

**9. Why are thresholds adjustable?**  
Different machines and test conditions have different normal readings. A slider lets the operator set a limit and demonstrate how the rule changes.

**10. What happens when a threshold is exceeded?**  
The Mac dashboard creates a timestamped alert and sends an alarm command to the phone. The phone lights its warning indicator, plays a short tone and sends an acknowledgement.

**11. What is the actuator?**  
The phone's on-screen warning lamp and browser-generated tone act as the prototype actuator. It is a demonstration output, not a real machine shutoff.

**12. What happens if the internet connection is lost?**  
The MQTT client tries to reconnect. Sensor messages generated while disconnected are held in a small in-memory queue and are sent after reconnection. If the page is closed or suspended, this temporary queue may be lost.

**13. Are these industrially accurate measurements?**  
No. They are readings from consumer phone sensors. The microphone value is dBFS, not calibrated dB SPL, and the accelerometer estimate depends on the phone and how it is held. Industrial deployment needs calibrated sensors.

**14. Why did you use a public broker?**  
It avoids buying or configuring a server for a classroom prototype. It is shared and not private, so the app sends only non-sensitive demo sensor values. A real factory would use a private authenticated broker.

**15. What would you improve?**  
Use calibrated vibration and sound sensors, collect normal operating data, build a more reliable anomaly-detection model, store historical readings, and use a private MQTT broker with authentication.

**16. Did AI write the code?**  
ChatGPT helped generate and explain the initial code. I disclosed that use in the prompt log. I am responsible for testing it, understanding it and explaining how each part works.
