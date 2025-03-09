# Staying_Awake_Staying_Focused
📌 README.md - Voxel51 Hackathon: AI-Powered Driver Safety System
🚀 Using YOLOv5 & FiftyOne to Detect Drowsiness & Phone Usage in Real-Time

👨‍💻 Developed by: Isaac Gbaba & Team
📅 Hackathon: Voxel51 Hackathon 2024
📍 Tools Used: FiftyOne, YOLOv5, PyTorch, OpenCV, Raspberry Pi

📌 Project Overview
🎯 Goal:
Develop an AI-based system that detects drowsiness & phone usage while driving, tracks duration, and triggers real-time alerts via a car’s horn, hazard lights, or radio.

🔥 Why This Matters?
✅ Prevents road accidents due to drowsy driving
✅ Detects unsafe mobile phone usage behind the wheel
✅ Uses AI-powered object detection with real-time monitoring

📂 Project Structure
bash
Copy
Edit
/voxel51_Hackathon
│── /Drowsy_dataset/         # Drowsy detection dataset
│── /phone_dataset/          # Phone detection dataset
│── /yolo_dataset/           # Converted YOLOv5 dataset (images + labels)
│── dataset.json             # COCO annotation file
│── train.py                 # YOLOv5 training script
│── inference.py             # YOLOv5 detection script
│── fiftyone_analysis.py      # Dataset analysis in FiftyOne
│── car_alert.py             # Raspberry Pi alert system
│── README.md                # Project documentation
🛠️ Installation
1️⃣ Install Dependencies
Run the following command to install YOLOv5, FiftyOne, and OpenCV:

bash
Copy
Edit
pip install ultralytics fiftyone torch torchvision opencv-python RPi.GPIO
2️⃣ Clone the YOLOv5 Repository
bash
Copy
Edit
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt
📊 Step 1: Load and Analyze Dataset in FiftyOne
Before training, we load the dataset into FiftyOne to inspect images and labels:

python
Copy
Edit
import fiftyone as fo

# Load dataset
dataset = fo.Dataset.from_dir(
    dataset_type=fo.types.ImageDirectory,
    dataset_dir="Drowsy_dataset"
)

# Launch FiftyOne app
session = fo.launch_app(dataset)
🎯 What you can do in FiftyOne:

Filter & sort images based on labels
Check data quality before training
Balance dataset to avoid bias
🔄 Step 2: Convert Data to YOLOv5 Format
YOLOv5 needs images & labels in the correct structure. Convert the dataset:

python
Copy
Edit
import fiftyone.utils.yolo as fouy

yolo_dataset_dir = "yolo_dataset"

fouy.export_yolo_dataset(
    dataset=fo.load_dataset("drowsy_phone_dataset"),
    export_dir=yolo_dataset_dir,
    split="train",
)
🚀 Step 3: Train YOLOv5 Model
Modify data.yaml for YOLOv5:

yaml
Copy
Edit
train: C:/Users/isaacg/Desktop/voxel51_Hackathon/yolo_dataset/train/images
val: C:/Users/isaacg/Desktop/voxel51_Hackathon/yolo_dataset/valid/images

nc: 2
names: ["drowsy", "phone"]
Run YOLOv5 training:

bash
Copy
Edit
python train.py --img 640 --batch 16 --epochs 50 --data yolo_dataset/data.yaml --weights yolov5s.pt --device 0
📌 Training Outputs:

Model checkpoints
Precision/Recall curves
Training loss graphs
📸 Step 4: Running Inference on Test Data
After training, test the model on unseen images:

python
Copy
Edit
from ultralytics import YOLO

model = YOLO("yolov5/runs/train/exp/weights/best.pt")
results = model.predict(source="yolo_dataset/test/images", save=True)
📌 Predictions saved in yolov5/runs/detect/exp/

📊 Step 5: Evaluating Model Performance in FiftyOne
We load predictions back into FiftyOne for deeper analysis:

python
Copy
Edit
import fiftyone.utils.yolo as fouy

test_dataset = fo.Dataset.from_dir(
    dataset_type=fo.types.YOLOv5Dataset,
    dataset_dir="yolo_dataset/test",
    labels_path="yolo_dataset/test/labels"
)

session = fo.launch_app(test_dataset)
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

🔗 GitHub Repo: [Add Your Link Here]
📨 Contact: [Your Name & Email]

🚀 Voxel51 Hackathon Project – Built with AI & FiftyOne
