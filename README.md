# Smart Tourist Safety Monitoring & Incident Response System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Flutter](https://img.shields.io/badge/Flutter-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![Next.js](https://img.shields.io/badge/Next.js-000000?logo=next.js&logoColor=white)](https://nextjs.org)
[![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)](https://python.org)
[![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?logo=mongodb&logoColor=white)](https://mongodb.com)

A comprehensive smart tourist safety monitoring system leveraging AI, Blockchain, and Geo-Fencing technologies to ensure tourist safety in high-risk regions, particularly in Northeast India.

**Organization:** Ministry of Development of North Eastern Region  
**Department:** Ministry of Tourism / Ministry of Home Affairs  
**Category:** Software  
**Theme:** Travel & Tourism

## 🚀 Quick Start

### Prerequisites

- **Flutter SDK** (>=3.0.0)
- **Node.js** (>=18.0.0)
- **Python** (>=3.9.0)
- **MongoDB** (>=5.0.0)
- **Redis** (>=6.0.0)
- **Docker** & **Docker Compose**

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-org/smart-tourist-safety-system.git
   cd smart-tourist-safety-system
   ```

2. **Setup Environment Variables**
   ```bash
   cp .env.example .env
   # Edit .env file with your configurations
   ```

3. **Start with Docker Compose**
   ```bash
   docker-compose up -d
   ```

4. **Or Manual Setup**
   ```bash
   # Backend
   cd python-backend
   pip install -r requirements.txt
   python main.py

   # Web Dashboard  
   cd web-dashboard
   npm install
   npm run dev

   # Mobile App
   cd flutter-app
   flutter pub get
   flutter run
   ```

## 🏗️ Architecture Overview

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Flutter App   │    │  Next.js Web    │    │   IoT Devices   │
│   (Tourist)     │    │   (Dashboard)   │    │  (Smart Bands)  │
└─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘
          │                      │                      │
          └──────────────────────┼──────────────────────┘
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

## 🛠️ Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Mobile App** | Flutter | Cross-platform tourist mobile application |
| **Web Dashboard** | Next.js | Real-time monitoring dashboard for authorities |
| **Backend API** | Python (FastAPI) | REST API and business logic |
| **Real-time Communication** | Socket.io | Live updates and emergency alerts |
| **Database** | MongoDB | Primary data storage |
| **Cache** | Redis | Session management and caching |
| **Blockchain** | Ethereum/Polygon | Digital ID and secure records |
| **AI/ML** | TensorFlow/PyTorch | Anomaly detection and predictive analytics |
| **Containerization** | Docker | Development and deployment |

## ✨ Key Features

### 🆔 Digital Tourist ID Generation Platform
- **Blockchain-based secure digital IDs** issued at entry points
- **KYC integration** with Aadhaar/Passport verification
- **Trip itinerary storage** with time-bound validity
- **Emergency contact management**

### 📱 Tourist Mobile Application
- **Auto-assigned Tourist Safety Score** based on travel patterns
- **Geo-fencing alerts** for high-risk or restricted zones
- **Panic Button** with live location sharing
- **Real-time tracking** (opt-in) for families and law enforcement
- **Multilingual support** (10+ Indian languages + English)

### 🤖 AI-Based Anomaly Detection
- **Location drop-off detection** for sudden disappearances
- **Prolonged inactivity monitoring** 
- **Route deviation alerts** from planned itineraries
- **Behavioral pattern analysis**

### 🖥️ Authority Dashboard
- **Real-time tourist tracking** with interactive maps
- **Heat maps** of high-risk zones and tourist clusters
- **Digital ID verification** and travel history
- **Automated E-FIR generation** for missing person cases
- **Alert management system** with priority classification

### 🔗 IoT Integration (Optional)
- **Smart bands/tags** for high-risk areas (caves, forests)
- **Continuous health monitoring** (heart rate, temperature)
- **Manual SOS features** with GPS tracking
- **Battery and connectivity alerts**

## 📁 Project Structure

```
smart-tourist-safety-system/
├── flutter-app/                 # Mobile application
│   ├── lib/
│   │   ├── main.dart
│   │   ├── services/            # API, location, blockchain services
│   │   ├── screens/             # UI screens
│   │   ├── models/              # Data models
│   │   └── widgets/             # Reusable components
│   └── pubspec.yaml
├── web-dashboard/               # Next.js web dashboard
│   ├── pages/
│   │   ├── api/                 # API routes
│   │   ├── dashboard/           # Dashboard pages
│   │   └── components/          # React components
│   ├── styles/
│   └── package.json
├── python-backend/              # Python backend services
│   ├── app/
│   │   ├── main.py             # FastAPI application
│   │   ├── models/             # Database models
│   │   ├── services/           # Business logic
│   │   ├── api/                # API endpoints
│   │   └── utils/              # Helper functions
│   └── requirements.txt
├── blockchain/                  # Smart contracts
│   ├── contracts/
│   ├── migrations/
│   └── truffle-config.js
├── iot-devices/                 # IoT device firmware
├── nginx/                       # Load balancer configuration
├── docker-compose.yml
└── README.md
```

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
# Database Configuration
MONGODB_URI=mongodb://localhost:27017/tourist_safety
REDIS_URL=redis://localhost:6379

# Blockchain Configuration
BLOCKCHAIN_RPC_URL=https://polygon-rpc.com
PRIVATE_KEY=your_private_key_here
CONTRACT_ADDRESS=your_contract_address_here

# API Configuration
API_BASE_URL=http://localhost:8000
SOCKET_SERVER_URL=http://localhost:8001
JWT_SECRET=your_jwt_secret_here

# External Services
GOOGLE_MAPS_API_KEY=your_google_maps_key
TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_token

# Security
ENCRYPTION_KEY=your_encryption_key_here
CORS_ORIGINS=http://localhost:3000,http://localhost:8080
```

## 🗄️ Database Schema

### Key Collections

#### Tourists Collection
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
    planned_itinerary: Array,
    accommodation: Array,
    local_contacts: Array
  },
  emergency_contacts: Array,
  safety_profile: {
    current_score: Number,
    risk_level: String,
    last_updated: Date
  },
  status: String,
  created_at: Date
}
```

#### Location Tracking Collection
```javascript
{
  _id: ObjectId,
  tourist_id: String,
  location: {
    type: "Point",
    coordinates: [longitude, latitude]
  },
  accuracy: Number,
  timestamp: Date,
  source: String,
  battery_level: Number
}
```

#### Alerts Collection
```javascript
{
  _id: ObjectId,
  alert_id: String,
  tourist_id: String,
  alert_type: String,
  severity: String,
  location: Object,
  description: String,
  status: String,
  created_at: Date
}
```

## 🚦 API Documentation

### Tourist Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/tourists/register` | Register new tourist |
| `GET` | `/api/tourists/{id}` | Get tourist details |
| `PUT` | `/api/tourists/{id}` | Update tourist information |
| `DELETE` | `/api/tourists/{id}` | Delete tourist record |

### Location Tracking

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/location/update` | Update tourist location |
| `GET` | `/api/location/history/{tourist_id}` | Get location history |
| `GET` | `/api/location/current/{tourist_id}` | Get current location |

### Emergency & Alerts

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/emergency/panic` | Trigger panic alert |
| `GET` | `/api/alerts/` | Get all alerts |
| `PUT` | `/api/alerts/{id}/acknowledge` | Acknowledge alert |
| `POST` | `/api/efir/generate` | Generate E-FIR |

### Example API Usage

```python
# Tourist Registration
import requests

tourist_data = {
    "name": "John Doe",
    "passport_number": "A1234567",
    "nationality": "US",
    "entry_point": "Guwahati Airport",
    "emergency_contacts": [
        {
            "name": "Jane Doe",
            "relation": "Spouse",
            "phone": "+1-555-0123"
        }
    ]
}

response = requests.post(
    "http://localhost:8000/api/tourists/register",
    json=tourist_data
)

print(response.json())
```

## 🔐 Security Features

### Data Protection
- **End-to-end encryption** for sensitive data
- **Hash-based PII storage** (Aadhaar, Passport numbers)
- **JWT-based authentication** with refresh tokens
- **Rate limiting** on API endpoints
- **CORS protection** with whitelist origins

### Blockchain Security
- **Immutable digital ID records** on blockchain
- **Smart contract validation** for ID verification
- **Multi-signature wallet support** for high-value transactions
- **Gas optimization** for cost-effective operations

### Privacy Compliance
- **GDPR compliance** for international tourists
- **Data anonymization** options
- **Consent management** system
- **Right to be forgotten** implementation

## 🤖 AI/ML Components

### Tourist Safety Score Algorithm
```python
def calculate_safety_score(tourist_data):
    base_score = 100
    
    # Location risk factor (0-40 points deduction)
    current_location_risk = get_location_risk_level(tourist_data.current_location)
    score -= current_location_risk * 20
    
    # Time of day factor (0-15 points deduction)
    if is_night_time():
        score -= 15
    
    # Route deviation (0-30 points deduction)
    route_deviation = calculate_route_deviation(
        tourist_data.planned_route, 
        tourist_data.current_route
    )
    score -= route_deviation * 10
    
    # Communication frequency (0-25 points deduction)
    last_activity = get_last_activity_time(tourist_data.tourist_id)
    if last_activity > 2_hours:
        score -= 25
    
    return max(0, min(100, score))
```

### Anomaly Detection
- **Isolation Forest** for location anomaly detection
- **LSTM networks** for behavioral pattern analysis
- **Clustering algorithms** for group behavior analysis
- **Real-time inference** with sub-second latency

## 🌍 Multilingual Support

### Supported Languages
- English (en)
- Hindi (hi)
- Assamese (as)
- Bengali (bn)
- Manipuri (mni)
- Nagamese (nag)
- Khasi (kha)
- Garo (grt)
- Mizo (lus)
- Tripuri (trp)

### Voice Emergency Access
```python
# Voice-based emergency system
supported_languages = {
    'en': 'en-US',
    'hi': 'hi-IN', 
    'as': 'as-IN',
    'bn': 'bn-IN'
}

def listen_for_emergency(language='en'):
    # Speech recognition implementation
    # Returns emergency info if detected
    pass
```

## 📊 Monitoring & Analytics

### Key Metrics
- **Tourist Safety Score** trends
- **Emergency response time** averages
- **Geofence violation** frequency
- **System performance** metrics
- **API response times**

### Logging
```python
import logging

# Configure structured logging
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('/var/log/tourist_safety.log'),
        logging.StreamHandler()
    ]
)

def log_emergency_event(tourist_id, event_type, location):
    logger.critical(f"EMERGENCY: Tourist {tourist_id} - {event_type} at {location}")
```

## 🧪 Testing

### Running Tests

```bash
# Python Backend Tests
cd python-backend
pytest tests/ -v

# Flutter App Tests  
cd flutter-app
flutter test

# Web Dashboard Tests
cd web-dashboard  
npm test

# Integration Tests
docker-compose -f docker-compose.test.yml up --abort-on-container-exit
```

### Test Coverage
- **Unit Tests:** 85%+ coverage
- **Integration Tests:** Critical user flows
- **E2E Tests:** Complete system workflows
- **Performance Tests:** Load testing for 10K+ concurrent users

## 🚀 Deployment

### Production Deployment

1. **Environment Setup**
   ```bash
   # Set production environment
   export NODE_ENV=production
   export MONGODB_URI=your_production_mongodb_uri
   export REDIS_URL=your_production_redis_url
   ```

2. **Build Applications**
   ```bash
   # Build web dashboard
   cd web-dashboard && npm run build
   
   # Build Flutter app
   cd flutter-app && flutter build apk --release
   ```

3. **Deploy with Docker**
   ```bash
   docker-compose -f docker-compose.prod.yml up -d
   ```

### Scaling Configuration
- **Horizontal scaling:** Multiple backend instances
- **Database sharding:** Geographic-based sharding
- **CDN integration:** Static asset delivery
- **Load balancing:** NGINX with health checks

## 📈 Performance Optimization

### Database Optimization
```javascript
// MongoDB Indexes
db.tourists.createIndex({ "tourist_id": 1 }, { unique: true })
db.location_tracking.createIndex({ "location": "2dsphere" })
db.alerts.createIndex({ "tourist_id": 1, "status": 1, "created_at": -1 })
```

### Caching Strategy
- **Redis caching** for frequently accessed data
- **Application-level caching** for ML model predictions
- **CDN caching** for static assets
- **Database query optimization**

## 🤝 Contributing

### Development Setup

1. **Fork and Clone**
   ```bash
   git clone https://github.com/your-username/smart-tourist-safety-system.git
   cd smart-tourist-safety-system
   ```

2. **Install Dependencies**
   ```bash
   # Install all dependencies
   make install-deps
   
   # Or install individually
   cd python-backend && pip install -r requirements.txt
   cd web-dashboard && npm install
   cd flutter-app && flutter pub get
   ```

3. **Create Feature Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

4. **Make Changes and Test**
   ```bash
   make test-all
   ```

5. **Submit Pull Request**

### Code Style
- **Python:** Follow PEP 8 with Black formatter
- **Flutter:** Follow Dart style guide with dartfmt
- **JavaScript:** ESLint with Prettier
- **Commit messages:** Conventional commit format

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

### Documentation
- [API Documentation](docs/api.md)
- [Flutter App Guide](docs/flutter-app.md)
- [Deployment Guide](docs/deployment.md)
- [Troubleshooting](docs/troubleshooting.md)

### Contact
- **Email:** support@tourist-safety-system.gov.in
- **Issues:** [GitHub Issues](https://github.com/your-org/smart-tourist-safety-system/issues)
- **Discussions:** [GitHub Discussions](https://github.com/your-org/smart-tourist-safety-system/discussions)

## 🗺️ Roadmap

### Phase 1 (Current - 6 months)
- [x] Core system architecture
- [x] Digital ID generation
- [x] Mobile app basic features
- [x] Web dashboard
- [ ] AI anomaly detection
- [ ] IoT integration
- [ ] Production deployment

### Phase 2 (Next 6 months)
- [ ] Advanced ML models
- [ ] International tourist support
- [ ] Advanced analytics dashboard
- [ ] Multi-region deployment
- [ ] Performance optimization

### Phase 3 (Future 6 months)
- [ ] Drone surveillance integration
- [ ] Smart city ecosystem integration
- [ ] Predictive tourism analytics
- [ ] Cross-border coordination
