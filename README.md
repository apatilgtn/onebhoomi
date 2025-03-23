# OneBhoomi Project

OneBhoomi is a comprehensive multi-cloud configuration and identity management platform designed to provide organizations with a unified interface for managing cloud resources, configurations, identities, and deployments across AWS, Azure, GCP, and other platforms.

## Project Overview

The platform incorporates best practices from industry tools like Octopus Deploy, AWS CodeDeploy, and Azure DevOps to create a single-pane-of-glass solution for multi-cloud management.

### Key Features

- **Unified Dashboard**: Real-time visibility across all cloud environments
- **Resource Management**: Discovery and management of cloud resources
- **Identity Management**: Centralized user and role management
- **Deployment Automation**: Unified deployment across multiple tools and platforms
- **Configuration Management**: Compliance and security management
- **Analytics & Reporting**: Cost and resource utilization insights

## Repository Structure

The project is organized as a set of microservices in separate repositories:

1. `onebhoomi-api-gateway` - API Gateway for routing requests
2. `onebhoomi-auth-service` - Authentication and authorization service
3. `onebhoomi-cloud-adapters` - Cloud provider integrations (AWS, Azure, GCP)
4. `onebhoomi-deployment-service` - Deployment automation
5. `onebhoomi-identity-service` - Identity and access management
6. `onebhoomi-configuration-service` - Configuration management
7. `onebhoomi-compliance-service` - Compliance and security
8. `onebhoomi-analytics-service` - Analytics and reporting
9. `onebhoomi-frontend` - React-based web interface
10. `onebhoomi-docs` - Project documentation
11. `onebhoomi-infrastructure` - Infrastructure as code
12. `onebhoomi-common` - Shared libraries and utilities

## System Requirements

### Development Environment

- **Operating System**: Any (Windows, macOS, Linux)
- **JDK**: Java Development Kit 17 or higher
- **Node.js**: v16.x or higher
- **Maven**: 3.8.x or higher
- **Docker**: Latest stable version
- **Docker Compose**: Latest stable version
- **Kubernetes**: kubectl and a local cluster (Minikube, kind, or Docker Desktop)
- **IDE**: IntelliJ IDEA, VS Code, or Eclipse
- **Git**: Latest version

### Production Environment

- **Kubernetes Cluster**: EKS, AKS, GKE, or self-managed
- **PostgreSQL**: 13.x or higher
- **MongoDB**: 5.x or higher
- **Redis**: 6.x or higher
- **Apache Kafka**: 3.x or higher
- **Elasticsearch**: 7.x or higher

## Setup Instructions

### 1. GitHub Setup

1. Create a GitHub organization named `onebhoomi`
2. Create the repositories listed above
3. Set up branch protection rules
4. Configure GitHub Actions

### 2. Local Development Setup

```bash
# Create a directory for the project
mkdir onebhoomi
cd onebhoomi

# Clone the repositories
git clone https://github.com/onebhoomi/onebhoomi-api-gateway.git
git clone https://github.com/onebhoomi/onebhoomi-auth-service.git
git clone https://github.com/onebhoomi/onebhoomi-cloud-adapters.git
git clone https://github.com/onebhoomi/onebhoomi-deployment-service.git
git clone https://github.com/onebhoomi/onebhoomi-identity-service.git
git clone https://github.com/onebhoomi/onebhoomi-configuration-service.git
git clone https://github.com/onebhoomi/onebhoomi-compliance-service.git
git clone https://github.com/onebhoomi/onebhoomi-analytics-service.git
git clone https://github.com/onebhoomi/onebhoomi-frontend.git
git clone https://github.com/onebhoomi/onebhoomi-docs.git
git clone https://github.com/onebhoomi/onebhoomi-infrastructure.git
git clone https://github.com/onebhoomi/onebhoomi-common.git
```

### 3. Initialize Backend Services

For each Java-based service, follow these steps:

```bash
# Go to the service directory
cd onebhoomi-service-name

# Create the basic file structure
mkdir -p src/main/java/com/onebhoomi/servicename/{config,controller,service,model,repository,dto,exception}
mkdir -p src/main/resources
mkdir -p src/test/java/com/onebhoomi/servicename

# Create the initial Maven POM file
cat > pom.xml << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.7.8</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.onebhoomi</groupId>
    <artifactId>service-name</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>OneBhoomi Service</name>
    <description>OneBhoomi Service Description</description>
    
    <properties>
        <java.version>17</java.version>
        <spring-cloud.version>2021.0.5</spring-cloud.version>
    </properties>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt-api</artifactId>
            <version>0.11.5</version>
        </dependency>
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt-impl</artifactId>
            <version>0.11.5</version>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt-jackson</artifactId>
            <version>0.11.5</version>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
EOF

# Create application properties file
cat > src/main/resources/application.yml << 'EOF'
server:
  port: 8080
  servlet:
    context-path: /api/v1/service-name

spring:
  application:
    name: onebhoomi-service-name
  datasource:
    url: jdbc:postgresql://${DB_HOST:localhost}:${DB_PORT:5432}/${DB_NAME:onebhoomi_db}
    username: ${DB_USER:postgres}
    password: ${DB_PASSWORD:postgres}
  jpa:
    hibernate:
      ddl-auto: update
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
        format_sql: true
    show-sql: true

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
EOF

# Create main application class
cat > src/main/java/com/onebhoomi/servicename/Application.java << 'EOF'
package com.onebhoomi.servicename;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
EOF

# Create Dockerfile
cat > Dockerfile << 'EOF'
FROM eclipse-temurin:17-jdk-alpine as build
WORKDIR /workspace/app

COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src

RUN ./mvnw install -DskipTests
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf ../*.jar)

FROM eclipse-temurin:17-jre-alpine
VOLUME /tmp
ARG DEPENDENCY=/workspace/app/target/dependency
COPY --from=build ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=build ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=build ${DEPENDENCY}/BOOT-INF/classes /app
ENTRYPOINT ["java","-cp","app:app/lib/*","com.onebhoomi.servicename.Application"]
EOF

# Create .gitignore file
cat > .gitignore << 'EOF'
HELP.md
target/
!.mvn/wrapper/maven-wrapper.jar
!**/src/main/**/target/
!**/src/test/**/target/

### STS ###
.apt_generated
.classpath
.factorypath
.project
.settings
.springBeans
.sts4-cache

### IntelliJ IDEA ###
.idea
*.iws
*.iml
*.ipr

### NetBeans ###
/nbproject/private/
/nbbuild/
/dist/
/nbdist/
/.nb-gradle/
build/
!**/src/main/**/build/
!**/src/test/**/build/

### VS Code ###
.vscode/

### Logs ###
logs/
*.log

### Environment Variables ###
.env
EOF

# Create GitHub Actions workflow file
mkdir -p .github/workflows
cat > .github/workflows/ci.yml << 'EOF'
name: CI

on:
  push:
    branches: [ feature/*, develop ]
  pull_request:
    branches: [ develop, main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Set up Java
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
          
      - name: Build and test
        run: ./mvnw clean verify
EOF

# Return to the main directory
cd ..
```

### 4. Initialize Frontend

```bash
# Go to the frontend directory
cd onebhoomi-frontend

# Initialize React application
npx create-react-app .

# Install dependencies
npm install react-router-dom @mui/material @emotion/react @emotion/styled @mui/icons-material axios redux react-redux redux-thunk recharts

# Create directories
mkdir -p src/{components,pages,services,store,utils,assets/images,assets/styles,layouts}

# Create basic structure
cat > src/App.js << 'EOF'
import React from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { ThemeProvider, createTheme } from '@mui/material/styles';
import CssBaseline from '@mui/material/CssBaseline';
import { Provider } from 'react-redux';
import store from './store';

// Layouts
import DashboardLayout from './layouts/DashboardLayout';
import AuthLayout from './layouts/AuthLayout';

// Pages
import Dashboard from './pages/Dashboard';
import Login from './pages/auth/Login';
import NotFound from './pages/NotFound';

// Create theme
const theme = createTheme({
  palette: {
    primary: {
      main: '#1976d2',
    },
    secondary: {
      main: '#dc004e',
    },
    background: {
      default: '#f5f5f5',
    },
  },
});

function App() {
  return (
    <Provider store={store}>
      <ThemeProvider theme={theme}>
        <CssBaseline />
        <Router>
          <Routes>
            {/* Auth routes */}
            <Route element={<AuthLayout />}>
              <Route path="/login" element={<Login />} />
            </Route>
            
            {/* Dashboard routes */}
            <Route element={<DashboardLayout />}>
              <Route path="/" element={<Dashboard />} />
            </Route>
            
            {/* 404 */}
            <Route path="*" element={<NotFound />} />
          </Routes>
        </Router>
      </ThemeProvider>
    </Provider>
  );
}

export default App;
EOF

# Create basic store
mkdir -p src/store/{actions,reducers}
cat > src/store/index.js << 'EOF'
import { createStore, applyMiddleware, compose } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const initialState = {};
const middleware = [thunk];

const store = createStore(
  rootReducer,
  initialState,
  compose(
    applyMiddleware(...middleware),
    window.__REDUX_DEVTOOLS_EXTENSION__ ? window.__REDUX_DEVTOOLS_EXTENSION__() : f => f
  )
);

export default store;
EOF

cat > src/store/reducers/index.js << 'EOF'
import { combineReducers } from 'redux';
import authReducer from './authReducer';

export default combineReducers({
  auth: authReducer
});
EOF

cat > src/store/reducers/authReducer.js << 'EOF'
const initialState = {
  token: localStorage.getItem('token'),
  isAuthenticated: false,
  user: null,
  loading: false,
  error: null
};

export default function(state = initialState, action) {
  const { type, payload } = action;
  
  switch(type) {
    case 'LOGIN_SUCCESS':
      localStorage.setItem('token', payload.token);
      return {
        ...state,
        token: payload.token,
        isAuthenticated: true,
        loading: false
      };
    case 'LOGIN_FAIL':
    case 'LOGOUT':
      localStorage.removeItem('token');
      return {
        ...state,
        token: null,
        isAuthenticated: false,
        loading: false,
        user: null
      };
    default:
      return state;
  }
}
EOF

# Create Dockerfile
cat > Dockerfile << 'EOF'
# Build stage
FROM node:16-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
EOF

# Create .gitignore file
cat > .gitignore << 'EOF'
# dependencies
/node_modules
/.pnp
.pnp.js

# testing
/coverage

# production
/build

# misc
.DS_Store
.env.local
.env.development.local
.env.test.local
.env.production.local

npm-debug.log*
yarn-debug.log*
yarn-error.log*
EOF

# Create GitHub Actions workflow file
mkdir -p .github/workflows
cat > .github/workflows/ci.yml << 'EOF'
name: CI

on:
  push:
    branches: [ feature/*, develop ]
  pull_request:
    branches: [ develop, main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Run tests
        run: npm test -- --passWithNoTests
        
      - name: Build
        run: npm run build
EOF

# Return to the main directory
cd ..
```

### 5. Initialize Infrastructure

```bash
# Go to the infrastructure directory
cd onebhoomi-infrastructure

# Create directory structure
mkdir -p terraform/{aws,azure,gcp}
mkdir -p kubernetes/{namespaces,infrastructure,services,config}
mkdir -p docker-compose
mkdir -p scripts

# Create basic docker-compose file
cat > docker-compose/docker-compose.yml << 'EOF'
version: '3.8'

services:
  postgres:
    image: postgres:13-alpine
    container_name: onebhoomi-postgres
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: onebhoomi
    ports:
      - "5432:5432"
    volumes:
      - postgres-data:/var/lib/postgresql/data

  mongodb:
    image: mongo:5
    container_name: onebhoomi-mongodb
    environment:
      MONGO_INITDB_ROOT_USERNAME: mongodb
      MONGO_INITDB_ROOT_PASSWORD: mongodb
    ports:
      - "27017:27017"
    volumes:
      - mongodb-data:/data/db

  redis:
    image: redis:6-alpine
    container_name: onebhoomi-redis
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data

  zookeeper:
    image: confluentinc/cp-zookeeper:7.0.1
    container_name: onebhoomi-zookeeper
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports:
      - "2181:2181"

  kafka:
    image: confluentinc/cp-kafka:7.0.1
    container_name: onebhoomi-kafka
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:29092,PLAINTEXT_HOST://localhost:9092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1

volumes:
  postgres-data:
  mongodb-data:
  redis-data:
EOF

# Create Kubernetes namespace file
mkdir -p kubernetes/namespaces
cat > kubernetes/namespaces/onebhoomi-namespace.yaml << 'EOF'
apiVersion: v1
kind: Namespace
metadata:
  name: onebhoomi
EOF

# Create basic deployment script
mkdir -p scripts
cat > scripts/setup-dev-environment.sh << 'EOF'
#!/bin/bash

echo "Setting up OneBhoomi development environment..."

# Start Docker Compose services
cd docker-compose
docker-compose up -d

echo "Development environment started."
echo "PostgreSQL: localhost:5432"
echo "MongoDB: localhost:27017"
echo "Redis: localhost:6379"
echo "Kafka: localhost:9092"
EOF

chmod +x scripts/setup-dev-environment.sh

# Return to the main directory
cd ..
```

### 6. Initialize Documentation

```bash
# Go to the documentation directory
cd onebhoomi-docs

# Create directory structure
mkdir -p architecture api user-guides developer-guides operations

# Create basic README
cat > README.md << 'EOF'
# OneBhoomi Documentation

This repository contains comprehensive documentation for the OneBhoomi multi-cloud management platform.

## Contents

- **Architecture**: System design and architecture diagrams
- **API**: API documentation and specifications
- **User Guides**: End-user documentation
- **Developer Guides**: Implementation and development guides
- **Operations**: Deployment and operations manuals

## Getting Started

Refer to the appropriate section based on your role:

- **End Users**: See the [User Guides](./user-guides/README.md)
- **Developers**: See the [Developer Guides](./developer-guides/README.md)
- **Operations**: See the [Operations Manual](./operations/README.md)
EOF

# Create basic architecture document
cat > architecture/README.md << 'EOF'
# OneBhoomi Architecture

This document describes the high-level architecture of the OneBhoomi platform.

## System Components

1. **API Gateway**: Entry point for all client requests
2. **Authentication Service**: User authentication and authorization
3. **Cloud Adapters**: Integration with various cloud providers
4. **Deployment Service**: Manages deployments across different tools
5. **Identity Service**: Identity and access management
6. **Configuration Service**: Resource configuration management
7. **Compliance Service**: Compliance and security management
8. **Analytics Service**: Reporting and analytics
9. **Frontend**: React-based user interface

## Communication Patterns

- **Synchronous Communication**: REST APIs for direct service-to-service communication
- **Asynchronous Communication**: Kafka for event-driven communication
EOF

# Return to the main directory
cd ..
```

### 7. Start Local Development

```bash
# Start infrastructure services
cd onebhoomi-infrastructure
./scripts/setup-dev-environment.sh

# In separate terminals, start each service
cd onebhoomi-auth-service
./mvnw spring-boot:run

cd onebhoomi-api-gateway
./mvnw spring-boot:run

# Start frontend
cd onebhoomi-frontend
npm start
```

## Project Timeline

| Phase | Duration | Description |
|-------|----------|-------------|
| **Phase 1** | 6 weeks | Planning, environment setup, core infrastructure |
| **Phase 2** | 12 weeks | Core services development (Auth, Cloud Adapters) |
| **Phase 3** | 6 weeks | Frontend development |
| **Phase 4** | 4 weeks | Testing and quality assurance |
| **Phase 5** | 4 weeks | Beta release and refinement |
| **Phase 6** | 2 weeks | General availability and post-release support |

## Technology Stack

### Backend
- **Language**: Java 17
- **Framework**: Spring Boot 2.7.x
- **Database**: PostgreSQL (relational data), MongoDB (configuration data)
- **Cache**: Redis
- **Messaging**: Apache Kafka
- **Security**: Spring Security, JWT

### Frontend
- **Framework**: React 18
- **State Management**: Redux
- **UI Components**: Material-UI
- **HTTP Client**: Axios
- **Visualization**: Recharts

### Infrastructure
- **Containerization**: Docker
- **Orchestration**: Kubernetes
- **CI/CD**: GitHub Actions
- **Monitoring**: Prometheus, Grafana
- **Logging**: ELK Stack

## Resources

- [Java Documentation](https://docs.oracle.com/en/java/)
- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Docker Documentation](https://docs.docker.com/)

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
