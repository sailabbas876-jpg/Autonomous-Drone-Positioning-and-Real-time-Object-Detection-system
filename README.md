# Autonomous Drone Positioning and Real-time Object Detection

### Developed by Sail Abbas

This repository contains my term-long course project for Electrical and Electronics Engineering. This project was sponsored by **Actinfly**.

---

## Project Overview

This repository is tested with a **PX4-compatible flight controller (Pixhawk 4)** and uses a **Jetson Nano** as the onboard computer to run the following code simultaneously.

The project contains a web page built with **Angular 2+, Java Spring Boot, and Flask**, which is used by the end-user to monitor and control the drone. Custom flight modes are available through a responsive web interface that allows the user to interact with the drone in real time.

The web page allows users to initiate custom flight actions from the drone while simultaneously observing annotated real-time footage from the camera mounted on the drone.

The Jetson Nano board is mounted on the drone and connected to the **Pixhawk 4 flight controller**, configured to communicate using **MAVLink**, along with a USB camera.

Upon successful hardware installation, the repository can be cloned to the onboard computer and the available functionalities can be accessed through the web page served by the Jetson Nano.

For further investigation and technical details, please refer to the **Project Report.pdf** included in this repository.

---

## Content

1. **Single-shot Deep Learning based Computer Vision Algorithm**

   * Detects occupancy of car parking spaces visible to the camera mounted on the drone in real time.

2. **Custom Flight Control Scripts**

   * Provides custom control scripts for autonomously controlling the drone.

3. **Platform-independent Web Page**

   * Provides a web interface for monitoring and autonomously controlling the drone.

---

## Folder Structure

### 1. `drone_backend`

Contains the backend **Java Spring Boot** code responsible for calling the custom flight modes available in the `python_control_scripts` folder from the web page.

### 2. `drone-fronend`

Contains the **Angular 2+** frontend code for the web page.

This is a single-page website that contains custom flight-mode configurations and displays the output of the car occupancy detection system in real time.

> **Note:** You need to provide your own Google Maps API key in this folder to use the customized Google Maps functionality for easily entering LLA coordinates.

### 3. `object-detector`

Contains the code for the deep object-detection model, based on a modified version of **YOLOv5**, along with the **Flask** backend used to serve annotated frames from the real-time video stream.

By changing the model weights available in this folder, the drone can be equipped with another object-detection model while continuing to use the existing web interface.

The backend responsible for serving annotated real-time video frames is located in the `utils/drone_project_utils` folder.

### 4. `python_control_scripts`

Contains Python code that initiates custom flight behaviors from the drone.

It uses **ROS 1, Kimera, and MAVROS**. Each script accepts its corresponding flight parameters as terminal inputs.

These scripts are called with arguments parsed from the web page through services available in the `drone_backend` folder.

> For further information and explanation, please refer to the comments in the source code.

---

## Results

### Web-site screenshot taken on iPhone 11 Pro Max

<img src="./ss/ss1.PNG" width="300px">

### Web-site screenshot

<img src="./ss/ss3.png" width="1000px">

### Live Object Detector — Car Occupancy Detection

<img src="./ss/ss2.JPG" width="1000px">

### Drone equipped with Pixhawk 4, USB Camera, and Jetson Nano

<img src="./ss/drone ss.png" width="350px">

---

# How to Run

## 1. Start Gazebo Simulation (SITL)

```bash
cd /path/to/PX4-Autopilot
make px4_sitl gazebo
```

For more information, refer to the PX4 Gazebo documentation.

<img src="./ss/ss4.png" width="500px">

---

## 2. Launch MAVROS

```bash
roslaunch mavros px4.launch fcu_url:="udp://:14540@192.168.1.36:14557"
```

For a Pixhawk 4 controller connected to the Jetson Nano through the telem port:

```bash
roslaunch mavros px4.launch fcu_url:=/dev/ttyUSB0:57600
```

You may need to modify the `fcu_url` parameter according to your hardware and network configuration.

<img src="./ss/ss5.png" width="500px">

---

## 3. Start Web Page Backend Server

```bash
cd drone_backend
mvn clean install
cd target
java -jar drone_backend-0.0.1-SNAPSHOT.jar
```

<img src="./ss/ss6.png" width="500px">

### Google Maps API

To use the customized Google Maps functionality for LLA coordinate input, obtain your own Google Maps API key and add it to:

```text
drone-fronend/src/app/app.component.ts
```

<img src="./ss/api key ss.png" width="700px">

---

## 4. Start Web Page Frontend Server

```bash
cd drone-fronend
npm install
ng serve --host 127.0.0.1
```

The UI can be accessed at:

```text
http://localhost:4200/
```

The same UI can also be accessed from another machine by replacing `localhost` with the corresponding device IP address, provided the required ports are properly configured.

<img src="./ss/ss7.png" width="500px">

---

## 5. Start Object Detector

Start the Car Occupancy Detector and its corresponding backend server:

```bash
cd object-detector/yolov5/utils/drone_project_utils
python3.8 expose_stream.py --source 0 --droneLiveStream --weight ../../best.pt
```

The `best.pt` file is used as the object-detection model weights.

You can change the detector's behavior by replacing these weights with a custom YOLOv5 model without requiring major modifications to the existing web interface.

<img src="./ss/ss8.png" width="700px">

---

# 👨‍💻 About the Developer

## Developed by Sail Abbas

**Sail Abbas** is a passionate and dedicated developer with a strong interest in **artificial intelligence, software development, and innovative digital solutions**.

He holds a **BS in Information Technology, Batch 2022–2026**, and is committed to continuous learning, building practical projects, and contributing to the growing field of technology.

Sail Abbas is a motivated developer focused on:

* Artificial Intelligence
* Automation
* Modern Software Solutions
* Practical Problem Solving
* User-Centered Design
* Innovative Digital Solutions

He enjoys creating impactful projects that combine technical skills with practical problem-solving and modern user experiences.

---

# 📧 Contact Information

| Information   | Details                                                 |
| ------------- | ------------------------------------------------------- |
| **Developer** | Sail Abbas                                              |
| **Email**     | [sailabbas876@gmail.com](mailto:sailabbas876@gmail.com) |
| **Education** | BS Information Technology, Batch 2022–2026              |

---

# 🎯 Developer Interests

Sail Abbas is particularly interested in developing solutions involving:

* 🤖 Artificial Intelligence
* 🧠 Machine Learning
* 🚁 Autonomous Systems
* 💻 Software Development
* ⚙️ Automation
* 👁️ Computer Vision
* 🌐 Modern Web Applications
* 🔬 Innovative Technology Solutions

---

# 📄 Project Report

For detailed information about the project architecture, implementation, experiments, and results, refer to:

**`Project Report.pdf`**

---

# 🙏 Acknowledgement

Special thanks to **Actinfly** for sponsoring this project and supporting the development of this autonomous drone positioning and real-time object detection system.

---

## Author

**Sail Abbas**

**BS Information Technology — Batch 2022–2026**

📧 **[sailabbas876@gmail.com](mailto:sailabbas876@gmail.com)**

---

## License

This project is intended for educational, research, and development purposes.
