# AI prompt log — MachineGuard

**AI tool:** ChatGPT by OpenAI (GPT-6)  
**Disclosure:** AI assistance was used for planning, code generation and explanatory writing. The student must personally test the application, understand the code, and make any corrections before submission.

## Main prompts / assistance sequence

1. **Initial request from student:** “This is my project. I have no idea what to do. I haven’t attended any classes at all. I don’t have a group so I’m doing the project solo. I don’t want to buy any material for the project so whatever online is best. Make it easy so I can even explain the code well or whatever the project is well. Please do the entire thing for me in the best way possible.”
   - AI action: reviewed the uploaded course brief and proposed a smartphone-based machine health monitoring project using the iPhone's built-in sensors, a Mac dashboard and MQTT.

2. **Student clarified available devices:** “I have a Mac and my iPhone yup.”
   - AI action: selected a two-device architecture, with iPhone as sensor node and Mac as dashboard, and generated an initial single-file HTML/CSS/JavaScript application.

3. **Implementation requirements used in code generation:** build a beginner-friendly two-mode browser app; use iPhone motion and microphone sensors; publish sensor readings over MQTT secure WebSockets; display live values, chart, logs and timestamped threshold alerts on the Mac; provide adjustable thresholds; send dashboard commands to the phone and receive acknowledgements; show a warning lamp/tone and basic offline queue behaviour.
   - AI action: generated `index.html` and checked JavaScript syntax. This syntax check does not replace real-device testing.

## Manual changes made by student

Complete this section honestly after you inspect and test the code. Examples: changed thresholds after measuring the phone, changed topic key, fixed a permission issue, changed dashboard labels, or adjusted styling.

- [Write each change you personally made, or state “No manual code changes yet” if accurate.]

## Testing performed by student

- [Date, device/browser, test, and actual result.]
- [Do not claim a test passed unless you performed it.]
