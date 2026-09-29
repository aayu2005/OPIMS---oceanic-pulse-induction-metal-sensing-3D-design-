# O-PIMS — Oceanic Pulse Induction Metal Sensing

## 🌊 Overview

**O-PIMS (Oceanic Pulse Induction Metal Sensing)** is a proposed low-cost, compact, and deployable seafloor sensing system designed for **preliminary detection and mapping of potential metal-rich mineral zones in deep-ocean environments**.

The system is designed for exploration of resources such as **polymetallic nodules and hydrothermal sulphide deposits**, while reducing the complexity associated with large underwater exploration platforms.

> **O-PIMS is intended as a preliminary exploration and anomaly-detection platform, not a replacement for full-scale AUV/ROV systems or laboratory mineral analysis.**

---

## 🎯 Objectives

* Detect potential metallic/mineralized anomalies near the seafloor.
* Map potential mineralized zones using multiple sensors.
* Provide a compact and relatively low-cost exploration platform.
* Enable deployment and recovery from a research vessel.
* Reduce direct interaction with the seabed during preliminary exploration.
* Support future multi-node and tethered deployment.

---

## 🔬 Core Technology

### Pulse Induction (PI)

O-PIMS uses **Pulse Induction electromagnetic sensing** as its primary metal-anomaly detection technique.

Basic working principle:

1. A high-current electrical pulse is applied to the sensing coil.
2. The pulse generates a transient electromagnetic field.
3. Conductive/metallic targets produce a secondary electromagnetic response.
4. The response is measured after the excitation pulse.
5. Multiple samples are processed to identify anomalies.
6. The detected anomaly is combined with sonar, camera, and environmental data.

The PI sensor provides evidence of a **conductive/metallic anomaly**; it does not directly determine the exact chemical composition of the mineral.

---

## 🧩 System Components

### 1. Pressure Protection

Proposed mechanical architecture:

* Borosilicate glass pressure sphere
* SS316L structural frame
* Polyurethane protective coating
* Waterproof electrical feedthroughs
* Pressure-rated internal electronics

At approximately **5 km depth**, hydrostatic pressure can approach **500 bar**, so the final deep-sea version requires proper pressure-housing design, testing, and certification.

### 2. PI Detection System

Main components:

* PI sensing coil
* MOSFET/power switching stage
* Gate driver
* Pulse-generation circuit
* Analog front-end
* ADC
* ESP32-based processing/control

The coil geometry, pulse current, sampling windows, and detection distance must be experimentally calibrated for the intended operating environment.

### 3. Sonar / Altimeter

The sonar system can be used to:

* Measure distance from the seafloor.
* Maintain/estimate sensor altitude.
* Identify seafloor morphology.
* Detect structures, mounds, chimneys, and other features.
* Support spatial mapping.

Sonar does **not directly detect metal**; it provides complementary structural information.

### 4. Underwater Camera

A camera with high-intensity LEDs provides visual information in the dark deep-ocean environment.

It can help identify:

* Exposed polymetallic nodules
* Seafloor structures
* Hydrothermal-vent-related features
* Sediment conditions
* Objects near the sensor

The camera cannot reliably identify buried deposits beneath the sediment.

### 5. Environmental Sensors

Potential sensors include:

* Pressure/depth sensor
* Temperature sensor
* Conductivity sensor
* IMU
* Distance/altitude sensor

These measurements can be used to compensate for environmental variations and improve interpretation of PI measurements.

### 6. Local Data Storage

An **SD card** can locally store:

* PI measurements
* Sensor readings
* Sonar data
* Depth
* Temperature
* Conductivity
* IMU data
* Timestamps
* System status

Local storage is important because conventional GPS, Wi-Fi, and cellular communication are unavailable underwater.

---

## 🌊 Seawater Compensation

Seawater is electrically conductive and can produce an environmental response during electromagnetic measurements.

Therefore:

**Measured Signal = Target Response + Seawater Response + Background/Sediment Response + Electronics Noise**

O-PIMS can use environmental measurements such as:

* Conductivity
* Temperature
* Sensor-to-seafloor distance
* Depth
* IMU orientation

to estimate the background response.

A possible processing approach is:

`Target Signal = Measured Signal − Estimated Background`

The compensation parameters should be determined through controlled laboratory and underwater calibration experiments rather than assumed theoretically.

---

## 🧠 Sensor Fusion

O-PIMS combines multiple sensing modalities instead of depending on a single sensor.

### PI + Sonar + Camera

**PI:**
Detects potential conductive/metallic anomalies.

**Sonar:**
Provides seafloor structure, distance, and morphology.

**Camera:**
Provides visual confirmation of exposed targets and structures.

Together, these measurements can generate a **potential mineralized-zone map**.

---

## 📡 Communication

### Initial Prototype

The prototype can primarily use:

* Local SD-card storage
* Tethered copper communication where practical

### Future Version

A future tethered O-PIMS system could use **pressure-rated underwater Ethernet/PoE-based interfaces** for:

* Power delivery
* High-speed data transfer
* Real-time monitoring
* Centralized processing on the surface vessel

Standard commercial PoE hardware should not be assumed to be suitable for deep-sea pressure without appropriate underwater-rated interfaces and protection.

---

## ⚓ Deployment Concept

O-PIMS can be deployed from a research vessel using a suitable deployment/tow arrangement.

A possible mission sequence:

```text
Research Vessel
      ↓
Deployment
      ↓
Controlled Descent
      ↓
Seafloor Survey
      ↓
PI + Sonar + Camera + Environmental Sensing
      ↓
Local Data Logging
      ↓
Potential Mineral Anomaly Detection
      ↓
Controlled Ballast Release
      ↓
Buoyancy-Assisted Ascent
      ↓
Surface Recovery
```

---

## 🪂 Recovery Mechanism

The concept uses **controlled buoyancy** for recovery.

During descent:

**Negative buoyancy → O-PIMS sinks**

After completing the survey:

**Ballast release → Positive buoyancy → O-PIMS rises**

A biodegradable sacrificial ballast concept, such as a corn-starch-based material, can be investigated for reducing persistent deployment waste.

The ballast should use a **controlled mechanical release mechanism** rather than relying on an assumed dissolution time at a particular depth.

---

## 🗺️ Mapping Concept

Each measurement can be associated with:

* Timestamp
* Depth
* Sensor altitude
* PI response
* Conductivity
* Temperature
* IMU orientation
* Sonar measurements
* Camera observations
* Surface/deployment position information where available

This information can be processed to generate a spatial map of potential anomalies.

For accurate georeferencing, underwater positioning can be combined with surface GPS and suitable acoustic positioning systems such as USBL/LBL.

---

## 🛠️ 3D Model

The GitHub repository includes a **3D CAD/Blender representation** of the proposed O-PIMS architecture.

The model represents:

* Borosilicate glass pressure sphere
* SS316L structural frame
* PI sensing coil
* Sonar/altimeter
* Underwater camera
* LED illumination
* Sensor modules
* Electronics enclosure
* Deployment/recovery components
* Tow/deployment arrangement

The 3D model is intended for **concept visualization, mechanical arrangement, component placement, and future prototype development**.

---

## 📐 Proposed Architecture

```text
                 O-PIMS
                    │
       ┌────────────┴────────────┐
       │                         │
 Pressure Protection       Sensing System
       │                         │
 Glass Sphere              ┌─────┼─────┐
 SS316L Frame               │     │     │
 PU Protection             PI   Sonar Camera
                           │     │     │
                           └─────┼─────┘
                                 │
                       Environmental Sensors
                                 │
                    ESP32 / Edge Processing
                                 │
                    ┌────────────┴────────────┐
                    │                         │
               SD Card                  Tethered Link
                    │                         │
              Local Data                Surface Vessel
```

---

## 💻 Software & Data Processing

The proposed processing pipeline is:

```text
Sensor Acquisition
       ↓
Signal Filtering
       ↓
Baseline Estimation
       ↓
Environmental Compensation
       ↓
PI Transient Analysis
       ↓
Anomaly Detection
       ↓
Sensor Fusion
       ↓
Spatial Mapping
       ↓
Potential Mineralized-Zone Map
```

Future software development may include:

* ESP32 firmware
* PI signal-processing algorithms
* Sensor calibration
* Data visualization
* Seafloor mapping
* Anomaly classification
* Multi-node data fusion
* Edge-AI-assisted anomaly detection

---

## 🤖 Future AI Integration

AI/ML can be added after sufficient experimental data is collected.

Possible inputs:

* PI transient decay
* Conductivity
* Temperature
* Depth
* Sensor altitude
* Sonar features
* Camera images
* IMU data

Possible outputs:

* Anomaly classification
* Potential nodule-zone detection
* Potential sulphide-zone identification
* False-positive reduction
* Seafloor anomaly mapping

AI should support the sensing system rather than being presented as a substitute for physical measurements or mineralogical analysis.

---

## 🚢 Scalability

One of the major future possibilities of O-PIMS is **multi-node deployment**.

Multiple units could be:

* Transported by the same research vessel.
* Deployed at different survey locations.
* Towed or positioned along predefined survey paths.
* Recovered after completing their measurements.
* Used to create a larger-area anomaly map.

This creates the possibility of a distributed seafloor sensing network.

---

## 🌱 Environmental Considerations

O-PIMS is designed around **preliminary, non-contact sensing** rather than direct excavation.

Potential environmental advantages include:

* No initial seabed drilling required for anomaly detection.
* PI sensing can operate without physically contacting the target.
* Camera and sonar provide remote observation.
* Reusable hardware architecture.
* Potential use of biodegradable sacrificial deployment material.

However, O-PIMS should not be described as completely impact-free. Deployment, recovery, cables, vessel operations, and underwater motion can still have environmental impacts.

---

## 💰 Cost Concept

The initial prototype is targeted toward a **low-cost development approach**, with an approximate prototype target of:

**1.5 lakhs**

This target applies to the proposed prototype and does **not** represent the cost of a certified 5–6 km operational deep-sea system.

A real deep-sea product would require additional costs for:

* Certified pressure housing
* Pressure testing
* Deep-sea connectors
* High-reliability electronics
* Deployment/recovery equipment
* Underwater communication
* Calibration
* Environmental testing
* Research-vessel operations

---

## 🔭 Future Scope

Future development can include:

1. 5–6 km pressure-tested housing
2. Improved PI coil and analog front-end
3. Multi-frequency/multi-window PI processing
4. Adaptive seawater compensation
5. High-resolution sonar mapping
6. AI-assisted anomaly classification
7. Acoustic underwater positioning
8. Pressure-rated Ethernet/PoE tether
9. Real-time surface dashboard
10. Multi-O-PIMS deployment
11. Automated survey-path planning
12. Improved buoyancy and recovery system
13. Experimental validation with real polymetallic nodules and sulphide samples

---

## ⚠️ Current Limitations

* PI detection range depends strongly on coil size, target size, material, seawater conductivity, and sensor altitude.
* PI alone cannot determine exact mineral composition.
* Camera cannot detect buried deposits.
* Sonar does not directly identify metal.
* Deep-sea pressure protection requires engineering validation.
* Underwater positioning requires dedicated positioning technology.
* Environmental compensation requires experimental calibration.
* The current 3D model represents a **concept/prototype architecture**, not a certified operational deep-sea vehicle.

---

## 📌 Project Status

**Stage:** Concept / 3D Mechanical Design / Prototype Development

The current repository focuses on the **3D visualization and proposed mechanical architecture** of O-PIMS. Hardware, sensing electronics, signal processing, pressure testing, and underwater validation are intended as subsequent development stages.

---

## 👥 Project

**Project:** O-PIMS — Oceanic Pulse Induction Metal Sensing
**Application:** Deep-Ocean Resource Exploration
**Primary Technology:** Pulse Induction Electromagnetic Sensing
**Platform:** Deployable Seafloor Sensor
**Target Resources:** Polymetallic Nodules, Hydrothermal Sulphides
**Prototype Target:** Low-cost development platform
**3D Software:** Blender

---

## 📜 Disclaimer

O-PIMS is a proposed engineering concept and prototype-development project. Performance values such as detection range, descent/ascent speed, pressure rating, and underwater communication range require experimental validation and should not be interpreted as certified operational specifications.

---
