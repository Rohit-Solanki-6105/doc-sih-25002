# Smart Tourist Safety Monitoring & Incident Response System
## Technical Documentation
### Live Dashboard Production Link : https://gov-police-dashboard-sih.vercel.app
### Token Generation: https://police-token-generation.vercel.app

### Project Overview

**Organization:** Ministry of Development of North Eastern Region  
**Department:** Ministry of Tourism / Ministry of Home Affairs  
**Category:** Software  
**Theme:** Travel & Tourism  

### Problem Statement

Development of a comprehensive Smart Tourist Safety Monitoring & Incident Response System leveraging AI, Blockchain, and Geo-Fencing technologies to ensure tourist safety in high-risk regions, particularly in Northeast India.

### Technology Stack

- **Mobile Application:** Flutter
- **Web Portal:** Next.js
- **Backend & Real-time Communication:** Python (FastAPI/Flask + Socket.io)
- **Database:** MongoDB
- **Blockchain:** Ethereum/Polygon for Digital ID
- **AI/ML:** Python (TensorFlow/PyTorch)
- **Real-time Features:** WebSocket connections

---

## System Architecture

### High-Level Architecture

```
┌─────────────────┐                           ┌───────────────────┐
│   Flutter App   │                           │   Next js Web     │
│   (Tourist)     │                           │ (Dashboard & All) │
└─────────┬───────┘                           └─────────┬─────────┘
          │                                             │
          └─────────────────────────────────────────────┘
                                 │
              ┌─────────────────────────────────┐
              │        API Gateway              │
              │      (Load Balancer)            │
              └─────────────┬───────────────────┘
                            │
          ┌─────────────────────────────────────────┐
          │           Python Backend                │
          │  ┌─────────────┐  ┌─────────────────┐   │
          │  │   FastAPI   │  │  Socket.io      │   │
          │  │   Server    │  │  Server         │   │
          │  └─────────────┘  └─────────────────┘   │
          │  ┌─────────────┐  ┌─────────────────┐   │
          │  │   AI/ML     │  │  Blockchain     │   │
          │  │  Services   │  │   Interface     │   │
          │  └─────────────┘  └─────────────────┘   │
          └─────────────┬───────────────────────────┘
                        │
    ┌───────────────────┼───────────────────┐
    │                   │                   │
┌───▼────┐    ┌────────▼────────┐    ┌─────▼─────┐
│MongoDB │    │   Blockchain    │    │   Redis   │
│        │    │   Network       │    │   Cache   │
└────────┘    └─────────────────┘    └───────────┘
```

---

## Core Components

### 1. Digital Tourist ID Generation Platform

**Technology:** Blockchain (Ethereum/Polygon)

#### Features:
- Secure blockchain-based digital ID issuance
- KYC integration (Aadhaar/Passport verification)
- Trip itinerary storage
- Emergency contact management
- Time-bound validity

#### Implementation:
```python
# Smart Contract Structure
class TouristID:
    - tourist_id: string
    - kyc_hash: string
    - itinerary_hash: string
    - emergency_contacts: array
    - issue_date: timestamp
    - expiry_date: timestamp
    - status: enum (active, expired, suspended)
```

#### Database Schema (MongoDB):
```javascript
// Tourist ID Collection
{
  _id: ObjectId,
  blockchain_address: String,
  tourist_id: String,
  personal_info: {
    name: String,
    passport_number: String,
    aadhaar_hash: String,
    nationality: String,
    photo_hash: String
  },
  trip_details: {
    entry_point: String,
    planned_itinerary: Array,
    duration: Number,
    purpose: String
  },
  emergency_contacts: Array,
  issue_timestamp: Date,
  expiry_timestamp: Date,
  status: String
}
```

### 2. Mobile Application (Flutter)

#### Key Features:

**Tourist Safety Score Algorithm:**
```python
def calculate_safety_score(tourist_data):
    base_score = 100
    
    # Location risk factor
    current_location_risk = get_location_risk_level(tourist_data.current_location)
    score -= current_location_risk * 20
    
    # Time of day factor
    if is_night_time():
        score -= 15
    
    # Deviation from planned route
    route_deviation = calculate_route_deviation(tourist_data.planned_route, tourist_data.current_route)
    score -= route_deviation * 10
    
    # Communication frequency
    last_activity = get_last_activity_time(tourist_data.tourist_id)
    if last_activity > 2_hours:
        score -= 25
    
    return max(0, min(100, score))
```

**Geo-fencing Implementation:**
```dart
// Flutter Geo-fencing Service
class GeofencingService {
  static const platform = MethodChannel('geofencing');
  
  Future<void> setupGeofences(List<GeoFence> fences) async {
    for (var fence in fences) {
      await platform.invokeMethod('addGeofence', {
        'id': fence.id,
        'latitude': fence.center.latitude,
        'longitude': fence.center.longitude,
        'radius': fence.radius,
        'riskLevel': fence.riskLevel
      });
    }
  }
  
  void onGeofenceEvent(GeofenceEvent event) {
    if (event.type == GeofenceEventType.enter && event.riskLevel == 'high') {
      showHighRiskAlert();
      sendLocationToAuthorities();
    }
  }
}
```

#### App Structure:
```
lib/
├── main.dart
├── services/
│   ├── auth_service.dart
│   ├── location_service.dart
│   ├── geofencing_service.dart
│   ├── blockchain_service.dart
│   └── socket_service.dart
├── screens/
│   ├── registration/
│   ├── dashboard/
│   ├── emergency/
│   └── settings/
├── models/
│   ├── tourist.dart
│   ├── location.dart
│   └── alert.dart
└── widgets/
    ├── safety_score_widget.dart
    ├── panic_button.dart
    └── map_widget.dart
```

### 3. Web Dashboard (Next.js)

#### Dashboard Features:
- Real-time tourist tracking
- Heat maps of high-risk zones
- Alert management system
- Digital ID verification
- Automated E-FIR generation

#### Technology Implementation:
```javascript
// Next.js API Route Structure
pages/
├── api/
│   ├── tourists/
│   │   ├── [id].js
│   │   ├── location.js
│   │   └── alerts.js
│   ├── dashboard/
│   │   ├── heatmap.js
│   │   └── statistics.js
│   └── emergency/
│       ├── efir.js
│       └── alerts.js
├── dashboard/
│   ├── index.js
│   ├── tourists.js
│   ├── alerts.js
│   └── analytics.js
└── components/
    ├── Map/
    ├── Dashboard/
    └── Alerts/
```

#### Real-time Updates:
```javascript
// Socket.io Integration
import io from 'socket.io-client';

const socket = io(process.env.SOCKET_SERVER_URL);

socket.on('tourist_location_update', (data) => {
  updateTouristLocation(data.tourist_id, data.location);
});

socket.on('emergency_alert', (alert) => {
  displayEmergencyAlert(alert);
  triggerNotification(alert);
});
```

### 4. Python Backend Services

#### Main Server Structure:
```python
# FastAPI Application Structure
app/
├── main.py
├── models/
│   ├── tourist.py
│   ├── location.py
│   ├── alert.py
│   └── blockchain.py
├── services/
│   ├── ai_service.py
│   ├── blockchain_service.py
│   ├── geofencing_service.py
│   ├── notification_service.py
│   └── socket_service.py
├── api/
│   ├── tourists.py
│   ├── location.py
│   ├── alerts.py
│   └── dashboard.py
└── utils/
    ├── database.py
    ├── security.py
    └── helpers.py
```

#### AI Anomaly Detection:
```python
import tensorflow as tf
from sklearn.ensemble import IsolationForest

class AnomalyDetectionService:
    def __init__(self):
        self.model = self.load_model()
        self.isolation_forest = IsolationForest(contamination=0.1)
    
    def detect_anomalies(self, tourist_data):
        # Location anomaly detection
        location_anomaly = self.detect_location_anomaly(tourist_data.locations)
        
        # Activity pattern anomaly
        activity_anomaly = self.detect_activity_anomaly(tourist_data.activities)
        
        # Communication pattern anomaly
        communication_anomaly = self.detect_communication_anomaly(tourist_data.communications)
        
        risk_score = self.calculate_risk_score(
            location_anomaly, 
            activity_anomaly, 
            communication_anomaly
        )
        
        if risk_score > 0.7:
            self.trigger_alert(tourist_data.tourist_id, risk_score)
        
        return risk_score
    
    def detect_location_anomaly(self, locations):
        # Implement location-based anomaly detection
        features = self.extract_location_features(locations)
        return self.isolation_forest.predict([features])[0] == -1
    
    def trigger_alert(self, tourist_id, risk_score):
        alert = {
            'tourist_id': tourist_id,
            'type': 'anomaly_detected',
            'risk_score': risk_score,
            'timestamp': datetime.now(),
            'status': 'active'
        }
        # Send to dashboard and mobile app
        socket_service.emit('emergency_alert', alert)
```

#### Socket.io Server:
```python
import socketio
from fastapi import FastAPI

sio = socketio.AsyncServer(async_mode='asgi', cors_allowed_origins="*")

@sio.event
async def connect(sid, environ):
    print(f"Client {sid} connected")

@sio.event
async def location_update(sid, data):
    # Process location update
    await process_location_update(data)
    
    # Broadcast to dashboard
    await sio.emit('tourist_location_update', data, room='dashboard')

@sio.event
async def emergency_alert(sid, data):
    # Process emergency
    await handle_emergency(data)
    
    # Notify all relevant parties
    await sio.emit('emergency_alert', data, room='authorities')

async def handle_emergency(data):
    # Create emergency record
    emergency_record = await create_emergency_record(data)
    
    # Notify nearest police station
    await notify_authorities(data['location'], emergency_record)
    
    # Generate E-FIR
    await generate_efir(emergency_record)
```

### 5. Database Design (MongoDB)

#### Collections Structure:

**Tourists Collection:**
```javascript
{
  _id: ObjectId,
  tourist_id: String,
  digital_id_address: String,
  personal_info: {
    name: String,
    email: String,
    phone: String,
    nationality: String,
    passport_number: String,
    aadhaar_hash: String
  },
  trip_info: {
    entry_point: String,
    planned_itinerary: [
      {
        location: String,
        planned_arrival: Date,
        planned_departure: Date
      }
    ],
    accommodation: Array,
    local_contacts: Array
  },
  emergency_contacts: [
    {
      name: String,
      relation: String,
      phone: String,
      email: String
    }
  ],
  safety_profile: {
    current_score: Number,
    risk_level: String,
    last_updated: Date
  },
  status: String,
  created_at: Date,
  updated_at: Date
}
```

**Location Tracking Collection:**
```javascript
{
  _id: ObjectId,
  tourist_id: String,
  location: {
    type: "Point",
    coordinates: [longitude, latitude]
  },
  accuracy: Number,
  altitude: Number,
  speed: Number,
  heading: Number,
  timestamp: Date,
  source: String, // 'mobile', 'iot_device'
  battery_level: Number,
  network_type: String
}
```

**Alerts Collection:**
```javascript
{
  _id: ObjectId,
  alert_id: String,
  tourist_id: String,
  alert_type: String, // 'geofence', 'panic', 'anomaly', 'inactivity'
  severity: String, // 'low', 'medium', 'high', 'critical'
  location: {
    type: "Point",
    coordinates: [longitude, latitude]
  },
  description: String,
  triggered_by: String,
  status: String, // 'active', 'acknowledged', 'resolved'
  response_actions: Array,
  created_at: Date,
  acknowledged_at: Date,
  resolved_at: Date
}
```

**Geofences Collection:**
```javascript
{
  _id: ObjectId,
  fence_id: String,
  name: String,
  location: {
    type: "Polygon",
    coordinates: Array
  },
  risk_level: String, // 'low', 'medium', 'high', 'restricted'
  description: String,
  restrictions: Array,
  active_hours: {
    start: String,
    end: String
  },
  created_by: String,
  created_at: Date,
  status: String
}
```

### 6. IoT Integration (Optional)

#### Smart Band/Tag Features:
- GPS tracking
- Health monitoring (heart rate, temperature)
- SOS button
- Low battery alerts
- Waterproof design

#### IoT Device Communication:
```python
# IoT Device Handler
class IoTDeviceService:
    def __init__(self):
        self.mqtt_client = mqtt.Client()
        self.setup_mqtt_connection()
    
    def setup_mqtt_connection(self):
        self.mqtt_client.on_connect = self.on_connect
        self.mqtt_client.on_message = self.on_message
        self.mqtt_client.connect("mqtt.broker.url", 1883, 60)
    
    def on_message(self, client, userdata, msg):
        data = json.loads(msg.payload.decode())
        
        if data['type'] == 'location_update':
            await self.process_location_update(data)
        elif data['type'] == 'sos_triggered':
            await self.handle_sos_alert(data)
        elif data['type'] == 'health_alert':
            await self.handle_health_alert(data)
    
    async def handle_sos_alert(self, data):
        # Create emergency alert
        alert = {
            'tourist_id': data['tourist_id'],
            'device_id': data['device_id'],
            'type': 'sos_triggered',
            'location': data['location'],
            'timestamp': data['timestamp'],
            'battery_level': data['battery_level']
        }
        
        # Immediate response
        await emergency_service.handle_emergency(alert)
```

---

## Security & Privacy Implementation

### Data Encryption:
```python
from cryptography.fernet import Fernet
import hashlib

class SecurityService:
    def __init__(self):
        self.key = Fernet.generate_key()
        self.cipher = Fernet(self.key)
    
    def encrypt_sensitive_data(self, data):
        return self.cipher.encrypt(data.encode())
    
    def decrypt_sensitive_data(self, encrypted_data):
        return self.cipher.decrypt(encrypted_data).decode()
    
    def hash_pii(self, pii_data):
        return hashlib.sha256(pii_data.encode()).hexdigest()
```

### Blockchain Integration:
```python
from web3 import Web3
import json

class BlockchainService:
    def __init__(self):
        self.w3 = Web3(Web3.HTTPProvider('YOUR_BLOCKCHAIN_RPC_URL'))
        self.contract_address = "YOUR_CONTRACT_ADDRESS"
        self.contract_abi = json.loads(CONTRACT_ABI)
        self.contract = self.w3.eth.contract(
            address=self.contract_address,
            abi=self.contract_abi
        )
    
    def issue_digital_id(self, tourist_data):
        # Create digital ID on blockchain
        transaction = self.contract.functions.issueTouristID(
            tourist_data['tourist_id'],
            tourist_data['kyc_hash'],
            tourist_data['itinerary_hash'],
            tourist_data['emergency_contacts_hash']
        ).buildTransaction({
            'from': self.w3.eth.default_account,
            'gas': 2000000,
            'gasPrice': self.w3.toWei('20', 'gwei')
        })
        
        signed_txn = self.w3.eth.account.signTransaction(
            transaction, 
            private_key=PRIVATE_KEY
        )
        
        tx_hash = self.w3.eth.sendRawTransaction(signed_txn.rawTransaction)
        return tx_hash.hex()
    
    def verify_digital_id(self, tourist_id):
        return self.contract.functions.verifyTouristID(tourist_id).call()
```

---

## Multilingual Support Implementation

### Language Configuration:
```dart
// Flutter Localization
class AppLocalizations {
  static const supportedLocales = [
    Locale('en', 'US'), // English
    Locale('hi', 'IN'), // Hindi
    Locale('as', 'IN'), // Assamese
    Locale('bn', 'IN'), // Bengali
    Locale('mni', 'IN'), // Manipuri
    // Add more regional languages
  ];
  
  static const localizationsDelegates = [
    AppLocalizationsDelegate(),
    GlobalMaterialLocalizations.delegate,
    GlobalWidgetsLocalizations.delegate,
    GlobalCupertinoLocalizations.delegate,
  ];
}
```

### Voice Emergency Access:
```python
import speech_recognition as sr
from gtts import gTTS
import pygame

class VoiceService:
    def __init__(self):
        self.recognizer = sr.Recognizer()
        self.microphone = sr.Microphone()
        self.supported_languages = {
            'en': 'en-US',
            'hi': 'hi-IN',
            'as': 'as-IN',
            'bn': 'bn-IN'
        }
    
    def listen_for_emergency(self, language='en'):
        with self.microphone as source:
            self.recognizer.adjust_for_ambient_noise(source)
            audio = self.recognizer.listen(source)
        
        try:
            text = self.recognizer.recognize_google(
                audio, 
                language=self.supported_languages[language]
            )
            
            if self.is_emergency_keyword(text, language):
                return self.extract_emergency_info(text, language)
                
        except sr.UnknownValueError:
            return None
    
    def speak_response(self, text, language='en'):
        tts = gTTS(text=text, lang=language, slow=False)
        tts.save("response.mp3")
        pygame.mixer.init()
        pygame.mixer.music.load("response.mp3")
        pygame.mixer.music.play()
```

---

## Deployment Architecture

### Production Environment:
```yaml
# Docker Compose Configuration
version: '3.8'

services:
  # Next.js Web Application
  web-dashboard:
    build: ./web-dashboard
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=mongodb://mongodb:27017/tourist_safety
    depends_on:
      - mongodb
      - python-backend
  
  # Python Backend Services
  python-backend:
    build: ./python-backend
    ports:
      - "8000:8000"
      - "8001:8001" # Socket.io server
    environment:
      - DATABASE_URL=mongodb://mongodb:27017/tourist_safety
      - REDIS_URL=redis://redis:6379
      - BLOCKCHAIN_RPC_URL=${BLOCKCHAIN_RPC_URL}
    depends_on:
      - mongodb
      - redis
  
  # MongoDB Database
  mongodb:
    image: mongo:5.0
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=${MONGO_USERNAME}
      - MONGO_INITDB_ROOT_PASSWORD=${MONGO_PASSWORD}
  
  # Redis Cache
  redis:
    image: redis:6.2
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
  
  # Load Balancer
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
    depends_on:
      - web-dashboard
      - python-backend

volumes:
  mongodb_data:
  redis_data:
```

### Scaling Considerations:
- Horizontal scaling for Python backend services
- Database sharding for large-scale deployments
- CDN integration for mobile app updates
- Load balancing for high availability

---

## Testing Strategy

### Unit Testing:
```python
# Python Backend Tests
import pytest
from fastapi.testclient import TestClient
from app.main import app

client = TestClient(app)

def test_create_tourist():
    tourist_data = {
        "name": "John Doe",
        "passport_number": "A1234567",
        "nationality": "US",
        "entry_point": "Guwahati Airport"
    }
    response = client.post("/api/tourists/", json=tourist_data)
    assert response.status_code == 201
    assert response.json()["name"] == "John Doe"

def test_geofence_alert():
    location_data = {
        "tourist_id": "T001",
        "latitude": 26.1445,
        "longitude": 91.7362,
        "timestamp": "2024-01-01T10:00:00Z"
    }
    response = client.post("/api/location/update", json=location_data)
    assert response.status_code == 200
```

```dart
// Flutter Widget Tests
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';
import 'package:tourist_safety_app/widgets/panic_button.dart';

void main() {
  group('Panic Button Widget Tests', () {
    testWidgets('Panic button displays correctly', (WidgetTester tester) async {
      await tester.pumpWidget(
        MaterialApp(home: Scaffold(body: PanicButton())),
      );
      
      expect(find.byType(PanicButton), findsOneWidget);
      expect(find.text('EMERGENCY'), findsOneWidget);
    });
    
    testWidgets('Panic button triggers emergency', (WidgetTester tester) async {
      bool emergencyTriggered = false;
      
      await tester.pumpWidget(
        MaterialApp(
          home: Scaffold(
            body: PanicButton(
              onEmergency: () => emergencyTriggered = true,
            ),
          ),
        ),
      );
      
      await tester.longPress(find.byType(PanicButton));
      await tester.pumpAndSettle();
      
      expect(emergencyTriggered, true);
    });
  });
}
```

---

## Performance Optimization

### Database Indexing:
```javascript
// MongoDB Indexes
db.tourists.createIndex({ "tourist_id": 1 }, { unique: true })
db.tourists.createIndex({ "status": 1, "created_at": -1 })
db.location_tracking.createIndex({ "tourist_id": 1, "timestamp": -1 })
db.location_tracking.createIndex({ "location": "2dsphere" })
db.alerts.createIndex({ "tourist_id": 1, "status": 1, "created_at": -1 })
db.geofences.createIndex({ "location": "2dsphere" })
```

### Caching Strategy:
```python
import redis
import json

class CacheService:
    def __init__(self):
        self.redis_client = redis.Redis(host='localhost', port=6379, db=0)
        self.default_ttl = 3600  # 1 hour
    
    def cache_tourist_data(self, tourist_id, data):
        key = f"tourist:{tourist_id}"
        self.redis_client.setex(
            key, 
            self.default_ttl, 
            json.dumps(data)
        )
    
    def get_cached_tourist_data(self, tourist_id):
        key = f"tourist:{tourist_id}"
        cached_data = self.redis_client.get(key)
        if cached_data:
            return json.loads(cached_data)
        return None
```

---

## Monitoring & Logging

### Application Monitoring:
```python
import logging
from prometheus_client import Counter, Histogram, start_http_server

# Metrics
api_requests_total = Counter('api_requests_total', 'Total API requests', ['method', 'endpoint', 'status'])
api_request_duration = Histogram('api_request_duration_seconds', 'API request duration')

# Logging Configuration
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('/var/log/tourist_safety.log'),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger(__name__)

def log_emergency_event(tourist_id, event_type, location):
    logger.critical(f"EMERGENCY: Tourist {tourist_id} - {event_type} at {location}")
    
def log_api_request(method, endpoint, status_code, duration):
    api_requests_total.labels(method=method, endpoint=endpoint, status=status_code).inc()
    api_request_duration.observe(duration)
```

---

## Future Enhancements

### Phase 2 Features:
1. **Machine Learning Improvements:**
   - Predictive modeling for tourist behavior
   - Advanced anomaly detection algorithms
   - Sentiment analysis from communications

2. **IoT Ecosystem Expansion:**
   - Smart city integration
   - Environmental sensor networks
   - Drone surveillance integration

3. **Enhanced Analytics:**
   - Tourism pattern analysis
   - Risk assessment improvements
   - Predictive maintenance for infrastructure

4. **International Integration:**
   - Cross-border tourist tracking
   - International emergency response
   - Multi-currency payment integration

### Estimated Timeline:
- **Phase 1 (Core System):** 6-8 months
- **Phase 2 (Enhanced Features):** 4-6 months
- **Phase 3 (Scale & Optimize):** 3-4 months

---

## Compliance & Regulatory Considerations

### Data Protection:
- GDPR compliance for international tourists
- India's Personal Data Protection Act compliance
- Regular security audits and penetration testing

### Government Integration:
- Integration with existing police systems
- Compliance with tourism department protocols
- Emergency service coordination standards

### Accessibility:
- WCAG 2.1 compliance for web dashboard
- Mobile accessibility features
- Support for users with disabilities
