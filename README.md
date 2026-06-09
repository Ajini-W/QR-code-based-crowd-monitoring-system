# QR Code Based Crowd Monitoring System

## Overview

The **QR Code Based Crowd Monitoring System** is a full-stack Java application designed to monitor and control crowd density in public venues such as conference halls, temples, shopping malls, and exhibition centers. The system uses dynamically generated, expiring QR codes to manage zone-wise entry, provides real-time occupancy tracking, and automatically generates alerts when capacity limits are reached.

## Features

- **Zone Management** – Create and manage multiple zones with custom names, locations, and maximum capacity limits.
- **Dynamic QR Generation** – Generate unique QR codes for each zone that expire after 5 minutes (using ZXing library).
- **QR Code Scanning** – Scan QR codes using any device camera (via Html5Qrcode library) to validate entry.
- **Real-Time Entry Control** – Automatically allow or deny entry based on current occupancy vs. maximum capacity.
- **Automated Alerts** – Generate and store alerts when a zone reaches full capacity.
- **Admin Dashboard** – Live statistics showing total zones, total alerts, and current crowd across all zones (auto-refreshes every 5 seconds).
- **Alert Logs** – View all capacity violation alerts with timestamps.
- **Secure & Expiring QR Codes** – QR codes cannot be reused, shared, or copied beyond their 5-minute expiry window.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Spring Boot 3.3.2, Java 17 |
| Frontend | HTML5, CSS3, JavaScript |
| QR Generation | Google ZXing 3.5.3 |
| QR Scanning | Html5Qrcode |
| Database | MySQL 8.0 |
| ORM | Spring Data JPA (Hibernate) |
| Build Tool | Maven |

## System Architecture
[Frontend: HTML/CSS/JS]
↕ REST API
[Backend: Spring Boot]
↕ JPA
[Database: MySQL]


### Modules

1. **Zone Management** – CRUD operations for venue zones
2. **QR Generation** – Creates time-limited QR codes (5 min expiry)
3. **QR Scanning** – Validates QR codes and processes entry
4. **Alert System** – Logs capacity violations automatically
5. **Admin Dashboard** – Live crowd statistics
6. **Logs Viewer** – Historical alert records

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/admin/zones` | Create a new zone |
| POST | `/api/admin/zones/{id}/qrcode` | Generate QR code for a zone |
| GET | `/api/admin/zones` | Get all zones |
| GET | `/api/admin/alerts` | Get all alerts |
| POST | `/api/user/scan` | Process a QR code scan |

## Prerequisites

- Java 17 or higher
- MySQL 8.0
- Maven 3.8+
- Modern web browser (Chrome, Firefox, Edge)
- Webcam (for scanning)

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/qr-crowd-monitoring.git
cd qr-crowd-monitoring

2. Configure MySQL Database
Start MySQL and create the database and user:

CREATE DATABASE qr_crowd_db;
CREATE USER 'qr_user'@'localhost' IDENTIFIED BY 'qr_pass';
GRANT ALL PRIVILEGES ON qr_crowd_db.* TO 'qr_user'@'localhost';
FLUSH PRIVILEGES;

3. Configure Application Properties
Update src/main/resources/application.properties if needed:
spring.datasource.url=jdbc:mysql://localhost:3306/qr_crowd_db?createDatabaseIfNotExist=true
spring.datasource.username=qr_user
spring.datasource.password=qr_pass
server.port=8080

4. Build and Run the Backend
mvn clean package
mvn spring-boot:run
The backend will start at http://localhost:8080

5. Access the Frontend
Open the following files directly in your browser:

frontend.html – Main navigation page

generate qr.html – Create zones and generate QR codes

scanner.html – Scan QR codes for entry

dashboard.html – Live admin dashboard

logs.html – View alert history

Project Structure
qr-crowd-monitoring/
├── src/main/java/com/example/qrcrowdmanagement/
│   ├── controller/
│   │   ├── AdminController.java
│   │   ├── UserController.java
│   │   └── ApiExceptionHandler.java
│   ├── service/
│   │   ├── ZoneService.java
│   │   ├── QrCodeService.java
│   │   ├── EntryService.java
│   │   ├── AlertService.java
│   │   └── UserService.java
│   ├── repository/
│   │   ├── ZoneRepository.java
│   │   ├── QrCodeRepository.java
│   │   ├── EntryRepository.java
│   │   ├── AlertRepository.java
│   │   └── UserRepository.java
│   ├── entity/
│   │   ├── Zone.java
│   │   ├── QrCode.java
│   │   ├── Entry.java
│   │   ├── Alert.java
│   │   └── User.java
│   └── dto/
├── src/main/resources/
│   └── application.properties
├── frontend/
│   ├── frontend.html
│   ├── generate qr.html
│   ├── scanner.html
│   ├── dashboard.html
│   └── logs.html
└── pom.xml

Future Enhancements
Mobile application (Android/iOS) with offline scanning

Email/SMS alerts for capacity thresholds (80%, 90%, 100%)

Historical analytics dashboard with charts

Exit scanning for true real-time occupancy

Role-based access control (super admin, event manager, security)

Cloud deployment (AWS/Azure)

License
This project is open-source and available under the MIT License.

Acknowledgments
Spring Boot Documentation

ZXing QR Code Library

Html5Qrcode Library

MySQL Community Server

