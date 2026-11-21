# MachineGuard — start here

This is a first working-code draft for the IDM 401 IoT App Project. It is designed for two devices and does not require purchased hardware:

- iPhone Safari = sensor node (accelerometer + microphone)
- Mac browser = monitoring dashboard
- MQTT over secure WebSockets = network connection

## Before anything else

1. Ask your professor for approval to work individually. The brief says solo work requires approval (page 19).
2. The brief's deadline is Thursday 19 November 2026. The current date is 21 November 2026, so contact the professor and check Moodle about late submission/extension.
3. This code has passed a JavaScript syntax check, but it has NOT yet been tested on your actual iPhone, Mac, browser, or campus network. You must complete the real-device tests and record the actual outcomes. Do not claim tests passed until you have run them.

## Publish the app for iPhone sensor permissions (HTTPS)

The easiest route is GitHub Pages:

1. On the Mac, go to https://github.com and sign in or create a free account.
2. Create a new **public** repository named `machineguard-iot`.
3. Upload this folder's `index.html` to the repository root. (The file must be named exactly `index.html`.)
4. Open the repository's **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**; select `main` and `/ (root)`, then Save.
6. Wait for GitHub Pages to publish. Open the HTTPS website link shown in Settings → Pages.
7. Open that same HTTPS link on the Mac and on iPhone Safari.

GitHub Pages supports HTTPS. iPhone motion and microphone access require a secure page and permission granted by the user.

## Run the two devices

1. On the Mac, open the published link. Leave **Mac · Dashboard** selected.
2. On the iPhone, open the same link in Safari.
3. Tap **iPhone · Sensor node**.
4. Tap **Allow & start sensors**. Allow Motion and Microphone when iOS asks.
5. Keep the phone on a safe desk or hold it securely. Gently move the phone to change vibration; clap or speak near the microphone to change sound. Do not attach it to machinery.
6. On the Mac, watch the live values, chart, alerts and MQTT message log.
7. On the Mac, click **Test alarm** or send **Start sensing / Stop sensing**. On the iPhone, observe the on-screen actuator and command acknowledgement.
8. For an offline test, temporarily disconnect the iPhone from Wi-Fi/mobile data, observe the disconnected state and queue counter, then reconnect. Check whether queued telemetry is delivered. Record what actually happens.

Both devices must use the same project topic key. It is already set inside the HTML. Do not change it on only one device.

## Troubleshooting

- If the page is not HTTPS, motion/microphone permissions may be blocked.
- Use Safari on iPhone and tap the Start button to request permission.
- If MQTT stays disconnected, try another network or phone hotspot. Campus networks may block broker connections.
- Check that both devices have internet access and that the MQTT.js CDN script loaded.
- Keep the phone page open during the demo; mobile browsers can pause background tabs.
- If motion permission was denied, check iPhone Settings → Safari → Motion & Orientation Access (wording can vary), then reload.
- If microphone permission was denied, check iPhone Settings → Safari → Microphone (wording can vary), then reload.

## Safety and privacy

The EMQX public broker is shared. Messages on it may be visible to other users. This demo sends only sensor numbers and generic commands. Do not publish your name, student ID, location, voice recordings, faces, or other personal information. The microphone audio is analysed locally in the browser; the code sends only the calculated sound level, not the audio stream.

This is an educational prototype, not a certified machine-condition monitor or safety system. dBFS is a relative digital sound level, not calibrated sound-pressure level in dB SPL. Phone accelerometers and microphone readings vary by device and placement.
