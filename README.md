from pathlib import Path

# Define the README content
readme_content = """
# 🏍️ Helmet Detection System

A real-time system to **detect motorcycle riders**, **classify helmet usage**, and **extract license plate numbers** from **IP camera video feeds** using deep learning and OCR techniques. The project features a GUI interface for easy control and configuration and is implemented entirely in **Python** using libraries like **OpenCV**, **PyTorch**, **Tesseract**, and **Tkinter**.

## 🚀 Features

- **Live Detection**: Real-time object detection for motorcycle riders, helmets, and license plates.
- **Helmet Classification**: Deep learning-based classification to detect helmet usage.
- **License Plate Recognition (OCR)**: Automated text extraction using Tesseract OCR.
- **User-Friendly GUI**: Intuitive Tkinter interface for camera control and configuration.
- **Automated Data Logging**: Saves detections and logs license plates to an Excel file.
- **Modular Architecture**: Easily extendable for future features or use cases.

## 🧩 System Components

### 1. `interface.py` – Graphical User Interface

Built with **Tkinter**, this module offers:

- 📷 **IP Camera Input**: Enter and validate IP addresses.
- 🟢 **Start Monitoring**: Launches the video detection process (`main.py`).
- 🔴 **Stop Monitoring**: Terminates active detection processes.
- ⚙️ **Settings**: Save and load default IP configurations using `ConfigParser`.
- 🧠 **Start OCR API**: Runs `txtapi.py` to begin OCR processing.

> ✅ Dark-themed interface for better visual comfort.

### 2. `main.py` – Main Video Monitoring Script

Handles the **core detection logic**:

- 🔄 **IP Camera Video Feed**: Connects and reads frames using **OpenCV**.
- 🧠 **YOLOv5 Detection**: Identifies motorcycles, riders, helmets, and plates.
- 🎯 **Helmet Classification**: Secondary model classifies helmet presence on detected heads.
- 💾 **Output Saving**: Saves images with annotations and cropped plates/riders.
- 🚨 **Alerts & Annotations**: Highlights violations directly in the video feed.

### 3. `my_functions.py` – Detection & Utility Logic

A helper module with:

- ⚙️ **YOLOv5 Integration**: Loads the object detection model.
- 🧠 **Helmet Classifier**: Loads and applies the helmet classification model.
- 🧩 **Bounding Box Utilities**: Match heads to riders by bounding box containment logic.

### 4. `txtapi.py` – OCR and License Plate Processing

Responsible for reading license plate text from saved frames:

- 🧹 **Image Preprocessing**: Resizes, sharpens, and formats images for OCR.
- 🔠 **OCR using Tesseract**: Extracts license plate numbers.
- ✅ **Validation & Logging**: Validates extracted text and saves it into Excel (`OpenPyXL`).
- 🔁 **Live Monitoring**: Continuously watches an image directory for new files.

## 🛠️ Technologies Used

| Technology     | Purpose                            |
|----------------|-------------------------------------|
| Python         | Core programming language          |
| Tkinter        | GUI development                    |
| OpenCV         | Video and image processing         |
| PyTorch        | Deep learning models (YOLOv5, classifier) |
| Tesseract OCR  | Optical character recognition      |
| ConfigParser   | Config file handling                |
| psutil         | Process management                  |
| openpyxl       | Excel file writing/reading          |

## 🔁 Workflow

1. **Launch GUI**  
   Run `interface.py`:
   ```bash
   python interface.py
            +-------------------+
            |   interface.py    |
            +--------+----------+
                     |
             (Starts/stops processes)
                     |
            +--------v----------+
            |     main.py       |
            |  (YOLOv5 + Helmet |
            |   Classification) |
            +--------+----------+
                     |
          Saves cropped images + video feed
                     |
            +--------v----------+
            |     txtapi.py     |
            |    (Tesseract +   |
            |   Excel Logging)  |
            +-------------------+
