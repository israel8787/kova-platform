# Kova Platform

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/node.js-18+-green.svg)](https://nodejs.org/)
[![React](https://img.shields.io/badge/react-18+-blue.svg)](https://reactjs.org/)
[![Rust](https://img.shields.io/badge/rust-1.70+-orange.svg)](https://www.rust-lang.org/)
[![Build Status](https://github.com/kovasystems/kova-platform/workflows/CI/badge.svg)](https://github.com/kovasystems/kova-platform/actions)

**Web platform and simulation engine for the Kova ecosystem**

Kova Platform is a comprehensive web-based platform that provides a unified interface for managing decentralized robotics data networks. It includes a simulation engine, real-time monitoring dashboard, data visualization tools, and fleet management capabilities.

## Features

- **Web Dashboard**: Modern React-based dashboard for monitoring and control
- **Simulation Engine**: Advanced robotics simulation with Gazebo integration
- **Real-time Monitoring**: Live data streaming and visualization
- **Fleet Management**: Multi-robot coordination and management
- **Data Visualization**: Interactive charts and 3D visualizations
- **Blockchain Integration**: Seamless integration with Kova blockchain
- **API Gateway**: RESTful and GraphQL APIs
- **User Management**: Authentication and authorization system
- **Deployment Tools**: Docker and Kubernetes deployment support

## Quick Start

### Prerequisites

- Node.js 18+
- Rust 1.70+
- Docker and Docker Compose
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/kovasystems/kova-platform.git
cd kova-platform

# Install dependencies
npm install

# Start development environment
docker-compose up -d

# Start the platform
npm run dev
```

### Access the Platform

- **Web Dashboard**: http://localhost:3000
- **API Gateway**: http://localhost:8080
- **Simulation Engine**: http://localhost:8081
- **Documentation**: http://localhost:3001

## Architecture

### Frontend (React)

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Dashboard     │───▶│  Data Viz       │───▶│  Fleet Mgmt     │
│   Components    │    │  Components     │    │  Components     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  State Mgmt     │    │  WebSocket      │    │  API Client     │
│  (Redux)        │    │  Connection     │    │  (Axios)        │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Backend (Rust)

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   API Gateway   │───▶│  Simulation     │───▶│  Data Pipeline  │
│   (Axum)        │    │  Engine         │    │  (Tokio)        │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Authentication │    │  Gazebo Bridge  │    │  Blockchain     │
│  (JWT)          │    │  (ROS2)         │    │  Integration    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## Components

### Web Dashboard

The React-based dashboard provides:

- **Real-time Monitoring**: Live sensor data visualization
- **Fleet Management**: Multi-robot coordination interface
- **Data Analytics**: Historical data analysis and reporting
- **Simulation Control**: Start/stop simulation environments
- **User Management**: Authentication and role-based access
- **Settings**: Platform configuration and preferences

### Simulation Engine

The Rust-based simulation engine includes:

- **Gazebo Integration**: Physics-based robotics simulation
- **Multi-Robot Support**: Simulate multiple robots simultaneously
- **Sensor Simulation**: Camera, LiDAR, IMU, GPS, and thermal sensors
- **Environment Models**: Various simulation environments
- **Real-time Rendering**: High-performance 3D visualization
- **API Interface**: RESTful API for simulation control

### API Gateway

The API gateway provides:

- **RESTful APIs**: Standard HTTP APIs for all operations
- **GraphQL APIs**: Flexible query interface
- **WebSocket Support**: Real-time data streaming
- **Authentication**: JWT-based authentication
- **Rate Limiting**: API rate limiting and throttling
- **Documentation**: Interactive API documentation

## Usage

### Starting a Simulation

```bash
# Start simulation via API
curl -X POST http://localhost:8080/api/v1/simulation/start \
  -H "Content-Type: application/json" \
  -d '{
    "environment": "warehouse",
    "robots": [
      {
        "id": "robot_001",
        "type": "mobile_robot",
        "sensors": ["camera", "lidar", "imu"]
      }
    ]
  }'
```

### Monitoring Fleet

```bash
# Get fleet status
curl http://localhost:8080/api/v1/fleet/status

# Get robot details
curl http://localhost:8080/api/v1/fleet/robots/robot_001
```

### Data Visualization

```javascript
// WebSocket connection for real-time data
const ws = new WebSocket('ws://localhost:8080/ws');

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    updateVisualization(data);
};
```

## Configuration

### Environment Variables

```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/kova_platform

# Redis
REDIS_URL=redis://localhost:6379

# Blockchain
SOLANA_RPC_URL=https://api.mainnet-beta.solana.com
IPFS_API_URL=http://localhost:5001

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRY=24h

# Simulation
GAZEBO_MASTER_URI=http://localhost:11345
ROS_DOMAIN_ID=0
```

### Configuration Files

#### `config/database.toml`

```toml
[database]
url = "postgresql://user:password@localhost:5432/kova_platform"
max_connections = 100
min_connections = 10
connection_timeout = 30

[redis]
url = "redis://localhost:6379"
max_connections = 50
```

#### `config/simulation.toml`

```toml
[simulation]
gazebo_master_uri = "http://localhost:11345"
ros_domain_id = 0
max_robots = 10
simulation_timeout = 3600

[environments]
warehouse = "worlds/warehouse.world"
factory = "worlds/factory.world"
outdoor = "worlds/outdoor.world"
```

## Development

### Frontend Development

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Run tests
npm test

# Build for production
npm run build
```

### Backend Development

```bash
# Install Rust dependencies
cargo build

# Run tests
cargo test

# Start development server
cargo run --bin kova-platform

# Run with specific features
cargo run --features simulation,blockchain
```

### Full Stack Development

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## API Documentation

### REST API

- **Base URL**: `http://localhost:8080/api/v1`
- **Authentication**: Bearer token in Authorization header
- **Content-Type**: `application/json`

#### Endpoints

- `GET /health` - Health check
- `GET /fleet/robots` - List all robots
- `POST /fleet/robots` - Add new robot
- `GET /fleet/robots/{id}` - Get robot details
- `POST /simulation/start` - Start simulation
- `POST /simulation/stop` - Stop simulation
- `GET /simulation/status` - Get simulation status
- `GET /data/sensors` - Get sensor data
- `POST /data/validate` - Validate sensor data

### GraphQL API

- **Endpoint**: `http://localhost:8080/graphql`
- **Playground**: `http://localhost:8080/graphql/playground`

#### Schema

```graphql
type Query {
  robots: [Robot!]!
  robot(id: ID!): Robot
  simulations: [Simulation!]!
  simulation(id: ID!): Simulation
  sensorData(robotId: ID!): [SensorData!]!
}

type Mutation {
  createRobot(input: RobotInput!): Robot!
  startSimulation(input: SimulationInput!): Simulation!
  stopSimulation(id: ID!): Boolean!
}

type Subscription {
  robotStatus(robotId: ID!): RobotStatus!
  sensorData(robotId: ID!): SensorData!
}
```

## Deployment

### Docker Deployment

```bash
# Build images
docker-compose build

# Deploy to production
docker-compose -f docker-compose.prod.yml up -d
```

### Kubernetes Deployment

```bash
# Apply Kubernetes manifests
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/ingress.yaml

# Check deployment status
kubectl get pods -n kova-platform
kubectl get services -n kova-platform
```

### Cloud Deployment

#### AWS

```bash
# Deploy to AWS EKS
eksctl create cluster --name kova-platform --region us-west-2
kubectl apply -f k8s/aws/
```

#### GCP

```bash
# Deploy to GCP GKE
gcloud container clusters create kova-platform --zone us-central1-a
kubectl apply -f k8s/gcp/
```

#### Azure

```bash
# Deploy to Azure AKS
az aks create --name kova-platform --resource-group kova-rg
kubectl apply -f k8s/azure/
```

## Monitoring

### Health Checks

```bash
# Check platform health
curl http://localhost:8080/health

# Check simulation engine
curl http://localhost:8081/health

# Check database
curl http://localhost:8080/api/v1/health/database
```

### Metrics

The platform exposes Prometheus metrics:

- `kova_platform_requests_total` - Total API requests
- `kova_platform_request_duration_seconds` - Request duration
- `kova_platform_active_simulations` - Active simulations
- `kova_platform_connected_robots` - Connected robots
- `kova_platform_sensor_data_points` - Sensor data points

### Logging

```bash
# View platform logs
docker-compose logs -f kova-platform

# View simulation logs
docker-compose logs -f simulation-engine

# View database logs
docker-compose logs -f postgres
```

## Testing

### Unit Tests

```bash
# Frontend tests
npm test

# Backend tests
cargo test

# Integration tests
cargo test --test integration
```

### End-to-End Tests

```bash
# Run E2E tests
npm run test:e2e

# Run with specific browser
npm run test:e2e -- --browser chrome
```

### Performance Tests

```bash
# Load testing
npm run test:load

# Stress testing
npm run test:stress
```

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

1. Fork the repository
2. Clone your fork
3. Create a feature branch
4. Make your changes
5. Add tests
6. Run the test suite
7. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Links

- [Website](https://www.kova.systems/)
- [Documentation](https://docs.kova.systems/platform/)
- [API Reference](https://api.kova.systems/)
- [Discord](https://discord.gg/kova)
- [Twitter](https://twitter.com/KovaSystems)

## Acknowledgments

- The React community for excellent frontend tooling
- The Rust community for high-performance backend development
- The Gazebo team for robotics simulation capabilities
- The Kova Systems team for the platform requirements

---

**Made with ❤️ by the Kova Systems team**