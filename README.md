---
config:
  layout: dagre
---
flowchart TD
 subgraph subGraph0["Smart Bra Device"]
        VIB["Vibrator Array<br>(Controlled Mechanical Actuators)"]
        ACC["Accelerometer Array<br>(Tri-axial MEMS Sensors)"]
        MCU["ESP32-based MYOSA Board<br>(Bluetooth + Data Acquisition)"]
        PWR["Battery & Power Regulation Module"]
  end
 subgraph subGraph1["Mobile Device Layer"]
        PHONE_APP["Local Pre-processing<br>(Filtering, FFT, Noise Reduction)"]
        DATA_ENC["Data Encryption &amp; Packaging<br>(Secure JSON Payloads)"]
  end
 subgraph subGraph2["Cloud Backend (Python Server)"]
        PREPROC["Signal Pre-Processing<br>(Normalization, Denoising)"]
        FEATEXT["Feature Extraction<br>(Tissue Resonance, Vibration Damping, Frequency Shift)"]
        MLALGO["ML-based Pattern Detection<br>(Cancerous vs. Normal Tissue Signature)"]
        DB[("Secure Database<br>Encrypted User Profiles &amp; History")]
        ALERT["Alerting &amp; Notification API<br>(Twilio / App Push)"]
  end
    User(["User Wearing Smart Bra"]) --> VIB & ACC
    VIB --> MCU
    ACC --> MCU
    PWR --> MCU
    MCU -- Bluetooth Low Energy (BLE) --> PHONE["Smartphone Application<br>(MYOSA App)"]
    PHONE --> PHONE_APP
    PHONE_APP --> DATA_ENC
    DATA_ENC -- HTTPS (TLS) --> CLOUD["Remote Processing Server"]
    CLOUD --> PREPROC
    PREPROC --> FEATEXT
    FEATEXT --> MLALGO
    MLALGO --> DB & ALERT
    ALERT -- Notification or SMS --> PHONE
    PHONE -- Alerts User --> User
     VIB:::hardware
     ACC:::hardware
     MCU:::hardware
     PWR:::hardware
     PHONE_APP:::software
     DATA_ENC:::software
     PREPROC:::cloud
     FEATEXT:::cloud
     MLALGO:::cloud
     DB:::data
     ALERT:::cloud
     User:::user
     PHONE:::network
     CLOUD:::network
    classDef hardware fill:#E6F7FF,stroke:#0099CC,stroke-width:2px,color:#003366,font-weight:bold
    classDef software fill:#FFF5E6,stroke:#FF9933,stroke-width:2px,color:#663300,font-weight:bold
    classDef network fill:#F0FFE6,stroke:#33CC33,stroke-width:2px,color:#003300,font-weight:bold
    classDef cloud fill:#F5E6FF,stroke:#9933FF,stroke-width:2px,color:#330066,font-weight:bold
    classDef user fill:#FFE6E6,stroke:#CC3333,stroke-width:2px,color:#660000,font-weight:bold
    classDef data fill:#FFFFE6,stroke:#CCCC33,stroke-width:2px,color:#666600,font-weight:bold
