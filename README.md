---
config:
  flowchart:
    nodeSpacing: 30
    rankSpacing: 15
    htmlLabels: true
---
flowchart LR
  subgraph Device ["Device"]
    VIB["Vibrator"]:::large
    ACC["Accel."]:::large
    MCU["ESP32<br>Board"]:::large
    PWR["Battery"]:::large
  end
  subgraph Mobile ["Mobile"]
    APP["App Proc."]:::large
    ENC["Encrypt"]:::large
  end
  subgraph Cloud ["Cloud"]
    PRE["Preproc"]:::large
    FEAT["Features"]:::large
    ML["ML Detect"]:::large
    DB["DB"]:::large
    NOTIFY["Notify"]:::large
  end
  USER(["User"]):::large --> VIB & ACC
  VIB --> MCU
  ACC --> MCU
  PWR --> MCU
  MCU -- BLE --> APP
  APP --> ENC
  ENC -- TLS --> PRE
  PRE --> FEAT
  FEAT --> ML
  ML --> DB & NOTIFY
  NOTIFY -- SMS/Push --> APP
  APP -- Alert --> USER

  classDef large font-size:22px,font-weight:bold
  class VIB,ACC,MCU,PWR,APP,ENC,PRE,FEAT,ML,DB,NOTIFY,USER large
