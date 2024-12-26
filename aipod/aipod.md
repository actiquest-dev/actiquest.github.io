---
icon: hubot
label: AI Live Pod

---

# AI Live Pod Overview

 
> Description of AI Live Pod Prototype

 
## AI Live Pod
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcoG4lJjaDMtggBT3kgWuTHPsK-zkjnkg3-229vLtm4efKjTNjuAtK-w5kpZFDQL8tT3SbxUuhlVYxfjAWYcw-uTNDUBqcZL3N-vj7rpC5PdPkIhzdkVuXPPbmLupCwfD-sgF8zrg?key=AsJEkgePh24159X10uUz6PJ-)

----------

## Description

The **AI Live Pod** is a state-of-the-art portable coaching device designed to revolutionize fitness, sports, music, and learning by leveraging cutting-edge AI, VR/AR, and decentralized technology. Below, we provide links to visual representations and detailed use cases to showcase its capabilities.

1. A sleek, portable design optimized for mobility and usability in various environments.

2.  VR180 6K HDR 60 fps motion capture and depth metadata using LiDAR sensor. Combination of several AI vision methods allows to capture high-quality 3D realtime reconstruction of the complete human body, including eyes, mimic, tongue and hands, without requiring any calibration and manual intervention.

> Motion-capture technology used in film and game production typically focuses only on face, body, and hand capture independently, involves complex and costly hardware, and requires significant manual intervention.  Even though machine-learning techniques exist to overcome these problems, they typically only support a single camera, often operate on a single body part, are not precise in world space, and rarely generalize outside a specified context.

 
3. AR/VR Integration ready

- Deploys captured biomechanics data to immersive AR and VR platforms and applications in realtime.

----------

## Indoor and Outdoor Mode
 
The **AI Live Pod** features a physical switch on the top of the device that allows seamless toggling between indoor and outdoor modes. This switch adjusts the camera angles to suit the respective environment:

 
### Indoor Mode

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcYeduYP1EbqdzcZE9Q7LvHpHBAtn7KMcHhHvrA60HZQceuPePXq2Ax83_pgBObUsOvARi16Y9jM8H_lugldhP-ZPRvT_MVO3Ygf_Z8ovw8zPOc4QhbsduMOHBieFn3K7XhIjJnIA?key=AsJEkgePh24159X10uUz6PJ-)

- The cameras are configured in a **stereo pair** setup, ideal for close-range tracking and depth perception.

- This mode is optimized for personal workouts, providing real-time feedback and tracking user movements with precision.

### Outdoor Mode

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdWmd2ly1PMukj8LE1axOd8SWvyeKg-9bI64AXMPdC6gd_qGwN0aOglNdLnSY1zzgORshPiIweSECGTHEby897A7FZ8o81HPipiH7ZpobtNMl2jwCmpu0FZuJhkOwxA6CECYnr_?key=AsJEkgePh24159X10uUz6PJ-)


- The cameras are positioned **160 degrees apart**, enabling wide-angle coverage to automatically follow actions on the field.

- Designed for sports events, this mode creates a **broadcast-like experience** by tracking players and activities dynamically.

- Users can **live-stream games**, watch recordings immediately after the event, and bookmark crucial moments for later review.
- AI sportcasting experience. AI can comment the live game in realtime.

### Spatial Audio

- Showcases the Harman Kardon Spatial 3D Audio system for immersive sound. Allows to precisely synchronize audio with video positioned, transmitted from AI pod to TV.

### Wireless HDMI

The **AI Live Pod** includes a docked **wireless HDMI receiver** that offers advanced connectivity options for enhanced usability:

 **4K Resolution Support:**

- Streams high-definition visuals, ensuring clarity and detail in every frame.

 **Cable-Free Convenience:**

- Eliminates the need for physical cables, allowing seamless device setup and operation.

- Wireless functionality enhances portability and minimizes setup time, making it perfect for on-the-go users.

**Instant Connection:**

- Automatically pairs and offering quick and hassle-free streaming.

- Simplified pairing ensures users can focus on their activities without technical distractions.

----------

## Use Cases  

### Fitness and Sports Training (General)

**Personalized Workouts:**

- Real-time coaching and customized routines based on user performance.

- Injury prevention through posture correction and muscle tracking.

- Each workout is dynamically tailored to fit the user's physical condition and goals, leveraging advanced tracking and data analysis.

**Performance Analysis:**

- Tracks progress using multi-object tracking and device positioning.

- Offers feedback and data-driven recommendations for improvement.

-   The tracking system ensures precision in monitoring physical activity, giving actionable insights for better performance.

### Indoor Activities

**Equipment Recognition:**

- Automatically detects fitness equipment to suggest exercises.

- Offers zero-shot capture for hands-free setup and monitoring.

-   The system's ability to recognize equipment makes it ideal for streamlined workouts in home or gym settings.

**Progress Tracking:**

- Tracks reps and performance to provide adaptive routines.

-   With continuous tracking, the device ensures users achieve steady progress by adjusting routines in real-time.

### Outdoor Activities

**Advanced Tracking:**

- Tracking & analyzing two player games (Tennis, Paddle, Badminton etc.)
- Tracking & analyzing team games (Soccer, Baseball, Hockey etc.).

## Smart Home Hub
- Functions as a hub for other smart devices with WiFi7, Bluetooth, ZigBee support.

----------

## Health and Sport Data Integration

The **AI Live Pod** seamlessly integrates with health and sport data providers to deliver an enhanced and comprehensive user experience:

**Holistic Fitness Profiles:**

- Syncs with wearable devices and health apps to gather real-time biometric data, such as heart rate, calories burned, and activity levels.
- By integrating multiple data sources, the pod creates a detailed fitness profile tailored to each user's health and performance needs.

**Custom Recommendations:**

- Leverages aggregated data to provide personalized workout plans, recovery advice, and dietary suggestions.
- Personalized insights ensure that users receive guidance aligned with their unique goals and physical conditions

**Performance Analytics:**

- Tracks key metrics like speed, endurance, and strength across various sports and fitness activities.
- Detailed analytics enable users to monitor improvements and refine their training regimens.  

**Cross-Platform Integration:**

- Connects seamlessly with popular platforms such as Apple Health, Google Fit, Strava, Suunto, Garmin and others.
- The integration ensures compatibility with existing ecosystems, enhancing usability and accessibility.

----------

## Tech Specification

The **AI Live Pod** prototype seamlessly integrates most perfect hardware and software running on it:

| Type | Description |
|--|--|
| Platform | NVIDIA Orin NX Nano 16/256  |
| OS | Linux L4T 32.3.1  |
| Vision | Stereoscopic-on-chip VR180 6K HDR, up to 120 FPS  |
| Mechanical Switcher | Indoor mode (Stereoscopic)/ Outdoor mode (160°)  |
| Lidar | Slamtec RPLIDAR A1-R6  |
| Speakers | 3 wide-brimmed speakers Harman-Univox, 15-watt max output   |
| Smart Home Connectivity | Matter  |
| Wireless Connectivity | Wi-Fi 7.0, Bluetooth  |
| HDMI | Docked wireless HDMI 2.2 Receiver  |
|Li-Pol 10KmAh Battery | Up to 5 hrs autonomy, fast charging|

----------

## MVP Requirements

### Core Functionality

1.  **Outdoor and Indoor Operation**:
    -   Operates outdoors on battery power.
    -   Charges via a docking station indoors.
2.  **Energy Efficiency**
    -   Maximum power consumption capped at 30W, with emphasis on optimization for lower consumption.
3.  **Offline Functionality**:
    -   Fully operational without internet or external data sources.
4.  **Basic Capabilities**:
    -   **Video Processing**: Real-time video stream handling from cameras.
    -   **Data Annotation and Local Reasoning**: Using a locally hosted LLM.
    -   **Speech-to-Text and Text-to-Speech (NLP)**: Processing voice commands locally.

### MVP Features

#### Video Processing

1.  **Stream Handling**:
    -   Real-time processing of video streams from two cameras.
    -   Stereo or combined single-frame processing with optical distortion correction.
2.  **Neural Network Application**:
    -   Object tracking using 1x CNN (e.g., YOLOv8).
    -   Biomechanics and motion analysis via:
        -   3x CNNs (face, body, and hands based on landmark methods).
        -   1x SOTA model and other supportive algorithms.

#### Voice Processing
1.  Bidirectional NLP (Speech-to-Text and Text-to-Speech):
    -   Variable processing loads distributed across CPU and CUDA resources.

#### Data Annotation:
1.  Local data annotation handled by CPU.

#### Reasoning and Model Training:
1.  Local reasoning using an LLM (balanced CPU+CUDA processing).
2.  Incremental training:
    -   Updates from cloud-based models to the on-device model during standby mode.

### Hardware Platform

**NVIDIA Jetson Orin NX AI Development Module**:

-   **Key Specs**:
    -   1024 CUDA Cores, 100 TOPS AI Performance.
    -   GPU: NVIDIA Ampere, 32 Tensor Cores, 918 MHz Max.
    -   CPU: 12-core ARM Cortex-A78AE, 2 GHz Max.
    -   Memory: 16 GB LPDDR5, 102.4 GB/s bandwidth.
    -   Power consumption: 10-25W.
    -   Camera support: Up to 4 physical (8 virtual channels).
    -   Multiple I/O options for USB, PCIe, and display.

**Additional Components**:
-   **Unitree 4D LiDAR L1**  (optional): For depth and absolute positioning.
-   **SYN4382**: A communication chip (WiFi 6, BLE, Matter).
-   **4x4K cameras + interface modules** (2 for binocular vision, wide-and short focus 100-160 degree fish-eye lenses for full body capure + 2 for player tracking, long focus, outdoor usage).

### User Interface

-   Simple configuration and management via a mobile application.
-   Outputs video analysis and voice command results directly to the app.

### Example Use Cases

1.  **Sports Training**: 
    -   General analysis of body angles and movements and what sport is on video
    -   Switching/Adding exact pretrained sport vision model
    -   Simple voice guidance for posture corrections (e.g., "Get ready, jump!")
    -   Answers to athlete requests
2.  **Short Video Analysis**:
    -   Record and parse short videos (1-3 minutes) with local LLM annotations.

### End Goal

-   A compact device that:
    -   Connects to a mobile app.
    -   Captures video and performs basic analysis (movements, angles, mimics, emotions).
    -   Give comments on video stream in real time.
    -   Processes voice commands locally.
    -   Operates autonomously for 4-6 hours on battery power.

### Technological Solutions

-   **Video and Neural Processing**: Efficiently leveraging both CUDA and CPU cores.
-   **Energy Management**: Ensuring high performance at minimal power consumption.
-   **Data Privacy**: Maintaining full offline functionality without internet dependency.
