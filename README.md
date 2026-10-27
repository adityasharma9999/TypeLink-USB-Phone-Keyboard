# TypeLink-USB-Phone-Keyboard
Send text from an Android phone to Windows over USB

Use your Android phone as a text input device for your Windows PC. Type text on your phone using Gboard or another Android keyboard and send it to the active Windows application over a USB connection.

## Features

- Type text using your phone's keyboard.
- Send text from Android to Windows over USB.
- Automatically configure ADB reverse port forwarding using a batch file.
- Paste received text into the active Windows application.
- Built with Android Studio and Python.

## Project Structure

```text
USB Phone Keyboard/
├── android/                  # Android application
├── windows/
│   ├── receiver.py           # Windows text receiver
│   └── start-usb-keyboard.bat
└── README.md
```

## Requirements

### Android

- Android phone
- USB cable that supports data transfer
- USB debugging enabled
- Android Studio to build or reinstall the app

### Windows

- Windows 10 or Windows 11
- Python 3
- Android Debug Bridge (ADB)
- USB debugging authorization for your phone

## Setup Instructions

### 1. Connect your Android phone

1. Enable Developer options on your phone.
2. Enable USB debugging.
3. Connect your phone to your Windows PC using a USB data cable.
4. Unlock your phone and approve the USB debugging authorization prompt.

### 2. Configure ADB

The Windows startup script uses ADB to establish a connection to the phone.

The current configuration expects ADB at:

```text
D:\Projects\usb keyboard folder\platform-tools\adb.exe
```

If ADB is installed somewhere else, open `windows/start-usb-keyboard.bat` in Notepad and update the `ADB` variable to the correct path.

The script also targets the phone with serial number `ZD222GGVL2`. If your phone's serial number changes or you use a different device, update it in the script.

To check connected devices, run:

```bat
"D:\Projects\usb keyboard folder\platform-tools\adb.exe" devices
```

Your phone should appear with the status `device`.

### 3. Start the Windows receiver

1. Open the project's `windows` folder.
2. Double-click `start-usb-keyboard.bat`.
3. The script checks the phone connection and configures USB reverse forwarding.
4. The Python receiver starts. Keep its terminal window open while using the app.

If Python is not installed, install Python 3 and ensure it is available through the Windows `py` or `python` command.

### 4. Open the Android app

1. Launch USB Phone Keyboard on your phone.
2. Connect the phone to the PC using USB.
3. Make sure the Windows receiver is running.
4. Type your text and use the app's send function.
5. The received text should be pasted into the currently active Windows application.

## Build and Run from Android Studio

1. Open Android Studio.
2. Open the project root containing `settings.gradle.kts`.
3. Wait for Gradle Sync to complete.
4. Connect your phone and select it as the target device.
5. Click **Run ▶** to build and install the application.

Once installed, the app remains on your phone even after Android Studio is closed.

## Troubleshooting

### ADB not found

Verify the path to `adb.exe` in `start-usb-keyboard.bat`.

### Phone not detected

- Check the USB cable and port.
- Enable USB debugging.
- Unlock the phone and accept the authorization prompt.
- Run `adb devices` to check the connection.

### USB forwarding fails

- Confirm that the correct phone serial number is used.
- Make sure the phone is connected and authorized.
- Check whether another application is already using port `8765`.

### Text is not appearing in Windows

- Keep the receiver terminal open.
- Ensure the Android app is using the correct port.
- Click inside the target Windows application before sending text.
- Check for errors in the receiver terminal.

## How It Works

The Android application sends text to a local HTTP endpoint on port `8765`. ADB reverse forwarding makes that endpoint accessible over the USB connection. The Python receiver processes the incoming text and attempts to paste it into the active Windows application.

This project uses ADB and clipboard-based pasting; it does not emulate a physical USB HID keyboard.

## Security Notes

- The receiver is intended for local use over USB.
- Avoid exposing the receiver to untrusted networks.
- Review the receiver code before using it with sensitive text.
- Do not commit passwords, API keys, signing keys, or other secrets to GitHub.

## License

Choose a license before distributing or reusing this project. If no license is provided, normal copyright restrictions apply.

