# Figures Directory

This directory contains all diagrams and images used in the internship report.

## Required Images (Generated from Mermaid Diagrams)

### 1. org_structure.png
**Location:** Chapter 1 - Overview
**Mermaid Code:**
```mermaid
graph TB
    A[NTQ Solutions JSC] --> B[NTEX Division]
    A --> C[Software Development]
    A --> D[Consulting Services]
    
    B --> E[R&D Department]
    B --> F[Product Management]
    
    E --> G[Edge AI Team]
    E --> H[IoT Solutions Team]
    E --> I[Computer Vision Team]
    
    style A fill:#1e88e5,color:#fff
    style B fill:#43a047,color:#fff
    style E fill:#fb8c00,color:#fff
```

### 2. system_architecture.png
**Location:** Chapter 3 - Implementation
**Mermaid Code:**
```mermaid
graph TB
    subgraph "Application Layer"
        A1[React Native App]
        A2[WebSocket Client]
        A3[User Interface]
    end
    
    subgraph "Cloud Layer"
        B1[FastAPI Server]
        B2[MQTT Broker]
        B3[WebSocket Manager]
        B4[TimescaleDB]
        B5[AI Engine]
    end
    
    subgraph "Edge Layer"
        C1[Raspberry Pi 4]
        C2[Audio Capture]
        C3[DHT22 Sensor]
        C4[YOLO Inference]
        C5[MQTT Publisher]
    end
    
    C2 --> C4
    C3 --> C5
    C4 --> C5
    C5 -->|MQTT| B2
    B2 --> B1
    B1 --> B3
    B1 --> B4
    B1 --> B5
    B3 -->|WebSocket| A2
    A2 --> A1
    A1 --> A3
    
    style C1 fill:#ff6b6b,color:#fff
    style B1 fill:#4ecdc4,color:#fff
    style A1 fill:#45b7d1,color:#fff
```

### 3. edge_pipeline.png
**Location:** Chapter 3 - Implementation
**Mermaid Code:**
```mermaid
graph LR
    A[Microphone] -->|16kHz PCM| B[Producer Thread]
    B -->|Queue| C[Consumer Thread]
    C --> D[STFT Processing]
    D --> E[Mel-Spectrogram]
    E -->|BytesIO| F[YOLOv8 Model]
    F --> G{Cry Detected?}
    G -->|Yes| H[Publish Alert]
    G -->|No| I[Continue Monitoring]
    H --> J[MQTT Client]
    
    K[DHT22 Sensor] --> L[Read T&H]
    L --> J
    J -->|TLS| M[Cloud MQTT Broker]
    
    style F fill:#ff6b6b,color:#fff
    style J fill:#95e1d3,color:#000
```

### 4. backend_flow.png
**Location:** Chapter 3 - Implementation
**Mermaid Code:**
```mermaid
sequenceDiagram
    participant Edge as Edge Device
    participant MQTT as MQTT Broker
    participant API as FastAPI Server
    participant DB as TimescaleDB
    participant WS as WebSocket Manager
    participant App as Mobile App
    
    Edge->>MQTT: Publish(topic, payload)
    MQTT->>API: on_message(payload)
    API->>API: Validate Schema
    API->>DB: INSERT INTO sensor_data
    DB-->>API: ACK
    API->>API: Evaluate Severity
    API->>WS: broadcast(alert)
    WS->>App: WebSocket Push
    App->>App: Display Notification
    App->>App: Play Alarm & Vibrate
```

### 5. stft_process.png
**Location:** Chapter 2 - Theory
**Mermaid Code:**
```mermaid
graph LR
    A[Raw Audio Signal] --> B[Apply Window Function]
    B --> C[Segment 1]
    B --> D[Segment 2]
    B --> E[Segment N]
    
    C --> F1[FFT]
    D --> F2[FFT]
    E --> F3[FFT]
    
    F1 --> G[Magnitude Spectrum]
    F2 --> G
    F3 --> G
    
    G --> H[Mel-Scale Mapping]
    H --> I[Mel-Spectrogram]
    
    style I fill:#ffd93d,color:#000
```

## How to Generate PNG Images

### Option 1: Using Mermaid Live Editor (Recommended)
1. Visit https://mermaid.live/
2. Paste the Mermaid code for each diagram
3. Click "Export" → "PNG"
4. Save the PNG file with the corresponding name in this directory

### Option 2: Using mermaid-cli
```bash
# Install mermaid-cli
npm install -g @mermaid-js/mermaid-cli

# Generate PNG (example)
mmdc -i diagram.mmd -o org_structure.png -b transparent -w 1200
```

### Option 3: Using VS Code Extension
1. Install "Markdown Preview Mermaid Support" extension
2. Create a markdown file with the mermaid code
3. Use the extension to export to PNG

## Image Specifications
- **Format:** PNG
- **Background:** Transparent or White
- **Width:** 1200-1600px (for good quality in PDF)
- **DPI:** 300 (for print quality)
