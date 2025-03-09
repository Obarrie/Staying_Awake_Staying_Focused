# Staying_Awake_Staying_Focused
📌 README.md - Voxel51 Hackathon: AI-Powered Driver Safety System
🚀 Using YOLOv5 & FiftyOne to Detect Drowsiness & Phone Usage in Real-Time

👨‍💻 Developed by: Isaac Gbaba, Osman Barrie, Paul Tran
📅 Hackathon: Voxel51 Hackathon 2024
📍 Tools Used: FiftyOne, YOLOv5, PyTorch,

📌 Project Overview
🎯 Goal:
Develop an AI-based system that detects drowsiness & phone usage while driving, tracks duration, and triggers real-time alerts via a car’s horn, hazard lights, or radio.

🔥 Why This Matters?
✅ Prevents road accidents due to drowsy driving
✅ Detects unsafe mobile phone usage behind the wheel
✅ Uses AI-powered object detection with real-time monitoring

🎯 What you can do in FiftyOne:

Compare ground truth vs. predicted labels
Filter false positives & false negatives
Improve dataset and retrain
🚗 Step 6: Integrate Car Alerts (Horn, Hazard Lights, Radio)
🔹 Trigger horn if the driver is on the phone too long 📱📢
🔹 Blink hazard lights or play a loud sound if drowsy 🚨😴
🔹 Wire detection to the car's electrical system (Raspberry Pi/Arduino)

Python Code for Raspberry Pi GPIO Alerts
python
Copy
Edit
import RPi.GPIO as GPIO
import time

# Define GPIO Pins for alerts
HORN_PIN = 17
HAZARD_LIGHTS_PIN = 27
RADIO_ALERT_PIN = 22

# Set up GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(HORN_PIN, GPIO.OUT)
GPIO.setup(HAZARD_LIGHTS_PIN, GPIO.OUT)
GPIO.setup(RADIO_ALERT_PIN, GPIO.OUT)

def alert_drowsiness():
    print("⚠️ Drowsiness detected! Activating hazard lights...")
    GPIO.output(HAZARD_LIGHTS_PIN, GPIO.HIGH)
    time.sleep(5)  # Keep lights on for 5 seconds
    GPIO.output(HAZARD_LIGHTS_PIN, GPIO.LOW)

def alert_phone_usage():
    print("⚠️ Phone detected! Activating horn...")
    GPIO.output(HORN_PIN, GPIO.HIGH)
    time.sleep(1)  # Beep horn for 1 second
    GPIO.output(HORN_PIN, GPIO.LOW)

# Example: Trigger alerts
alert_drowsiness()
alert_phone_usage()

GPIO.cleanup()
📌 Expected Outcome: If drowsy, hazard lights blink. If using a phone, horn beeps.

🎯 Final Steps
🔹 ✅ Test the tracking script & ensure detections are accurate
🔹 ✅ Integrate with Raspberry Pi for real-time alerts
🔹 ✅ Optimize alert triggers to prevent false alarms
🔹 ✅ Deploy & test the system in a real car setup

🎉 Conclusion
✅ We trained YOLOv5 for detecting drowsiness & phone usage
✅ We tracked how long these events happen using a Python script
✅ We designed an alert system to notify the driver in real-time
✅ Next, we integrate everything into a real car! 🚗💨

🚀 Voxel51 Hackathon Project – Built with AI & FiftyOne
