# Breast Cancer Early Detection System – Architecture Diagram

```mermaid
graph TD

%% ===========================
%% STYLE DEFINITIONS
%% ===========================
classDef hardware fill:#E6F7FF,stroke:#0099CC,stroke-width:2px,color:#003366,font-weight:bold
classDef software fill:#FFF5E6,stroke:#FF9933,stroke-width:2px,color:#663300,font-weight:bold
classDef network fill:#F0FFE6,stroke:#33CC33,stroke-width:2px,color:#003300,font-weight:bold
classDef cloud fill:#F5E6FF,stroke:#9933FF,stroke-width:2px,color:#330066,font-weight:bold
classDef user fill:#FFE6E6,stroke:#CC3333,stroke-width:2px,color:#660000,font-weight:bold
classDef data fill:#FFFFE6,stroke:#CCCC33,stroke-width:2px,color:#666600,font-weight:bold

%% ===========================
%% USER AND DEVICE LAYER
%% ===========================
User([User Wearing Smart Bra])
class User user

subgraph "Smart Bra Device"
    VIB[Vibrator Array<br>(Controlled Mechanical Actuators)]:::hardware
    ACC[Accelerometer Array<br>(Tri-axial MEMS Sensors)]:::hardware
    MCU[ESP32-based MYOSA Board<br>(Bluetooth + Data Acquisition)]:::hardware
    PWR[Battery & Power Regulation Module]:::hardware
end

User --> VIB
User --> ACC
VIB --> MCU
ACC --> MCU
PWR --> MCU

%% ===========================
%% COMMUNICATION LAYER
%% ===========================
MCU -->|Bluetooth Low Energy (BLE)| PHONE[Smartphone Application<br>(MYOSA App)]:::network

%% ===========================
%% MOBILE PROCESSING LAYER
%% ===========================
subgraph "Mobile Device Layer"
    PHONE_APP[Local Pre-processing<br>(Filtering, FFT, Noise Reduction)]:::software
    DATA_ENC[Data Encryption & Packaging<br>(Secure JSON Payloads)]:::software
end

PHONE --> PHONE_APP
PHONE_APP --> DATA_ENC
DATA_ENC -->|HTTPS (TLS)| CLOUD[Remote Processing Server]:::network

%% ===========================
%% CLOUD / SERVER LAYER
%% ===========================
subgraph "Cloud Backend (Python Server)"
    PREPROC[Signal Pre-Processing<br>(Normalization, Denoising)]:::cloud
    FEATEXT[Feature Extraction<br>(Tissue Resonance, Vibration Damping, Frequency Shift)]:::cloud
    MLALGO[ML-based Pattern Detection<br>(Cancerous vs. Normal Tissue Signature)]:::cloud
    DB[(Secure Database<br>Encrypted User Profiles & History)]:::data
    ALERT[Alerting & Notification API<br>(Twilio / App Push)]:::cloud
end

CLOUD --> PREPROC
PREPROC --> FEATEXT
FEATEXT --> MLALGO
MLALGO --> DB
MLALGO --> ALERT

%% ===========================
%% OUTPUT AND FEEDBACK LAYER
%% ===========================
ALERT -->|Notification or SMS| PHONE
PHONE -->|Alerts User| User

%% ===========================
%% DATA FLOW ANNOTATIONS
%% ===========================
%% Flow direction labels
linkStyle default stroke-width:2px
