# Remote Monitoring System - RMS

## Overview

This repository houses the details for RMS, a comprehensive system that combines a user interface, user management, report generation, UX design, and API interactions. The project also integrates with various components such as servers, domains, and ensures secure communications with SSL.

## Work Overview

- [System Architecture](#system-architecture)
- [Setup Guide](#setup-guide)
- [User Interface](#user-interface)
- [User Management](#user-management)
- [Reports](#reports)
- [UX Design](#ux-design)
- [APIs](#apis)
- [Server Interactions](#Server-interactions)
- [Domain Integration](#domain-integration)
- [SSL Configuration](#ssl-configuration)

## Features

- User-friendly web-based user interface.
- User management system.
- Report generation and visualization capabilities.
- Thoughtful UX design for enhanced user experience.
- APIs for seamless interactions with the backend.
- Integration with domains for a customized user experience.
- SSL configuration for secure communication.

## Brief Architecture

```mermaid
graph TD
  subgraph UIUX
    UserInterface
    UXDesign
  end

  subgraph Functionality
    UserManagement
    Reports
    APIs
  end

  subgraph Infrastructure
    BackendServer
    Domain
    SSL
  end

  UserInterface --> UserManagement
  UserInterface --> Reports
  UserInterface --> UXDesign
  UserManagement --> APIs
  APIs --> BackendServer
  APIs --> Domain
  APIs --> SSL
````


-----


# Time Series Data Analysis


## Assumptions

1. **Data Frequency:** Producers send data at fixed 1-minute intervals.
2. **Data Size:** Each data point from a producer is assumed to be 200 bytes.

## System Requirements and Scalability Considerations

To estimate the system requirements and scalability, we make the following assumptions and calculations:

### Producers and Data Points

- **Number of Producers:** 25,000
- **Data Points per Producer per Day:** 24 hours/day * 60 minutes/hour = 1440 data points/day
- **Total Data Points per Day:** 25,000 producers * 1440 data points/producer = 36,000,000 data points/day

### Data Size

- **Data Size per Data Point:** 200 bytes

### Storage Requirements

- **Daily Storage Usage:** 36,000,000 data points/day * 200 bytes/data point = 7.2 GB/day
- **Monthly Storage Usage:** 7.2 GB/day * 30 days/month = 216 GB/month

### Write Throughput

- **Data Points per Minute:** 25,000 producers * 1 data point/minute/producer = 25,000 data points/minute
- **Data Size per Minute:** 25,000 data points/minute * 200 bytes/data point = 5 MB/minute
- **Write Throughput:** The system should be able to handle 5 MB/minute write throughput.

## Setting Up the System

Follow the steps below to set up the Time Series Data Handling System:

1. **Install the Time Series Database:** Refer to the official installation guide for your chosen Time Series Database.

2. **Database Configuration:**
   - Configure the database for optimal performance, taking into account the expected write throughput and storage requirements.
   - Adjust database configuration parameters based on your system's specifications.

3. **Schema Design:**
   - Design an appropriate schema for your time-series data, considering the specific requirements and queries expected to be performed on the data.

4. **Write API:**
   - Develop a write API to handle data ingestion from the 25,000 producers.
   - Implement a mechanism to batch incoming data points efficiently.

5. **Monitoring and Scaling:**
   - Set up monitoring tools to keep track of database performance, storage usage, and system health.
   - Implement scaling strategies, such as vertical scaling by upgrading hardware or horizontal scaling by adding more nodes, as needed.


## Data Flow from IoT Device to Server


```mermaid
sequenceDiagram
    participant IoTDevice as "IoT Device"
    participant Gateway as "Gateway"
    participant Server as "Server"
    participant Database as "Database"

    IoTDevice->>Gateway: Data Packet
    activate Gateway
    Gateway->>Server: Forward Data Packet
    activate Server
    Server->>Database: Save Raw Packet and Processed Packet
    activate Database
    Database-->>Server: Acknowledgment
    deactivate Database
    Server-->>Gateway: Response
    deactivate Server
    Gateway-->>IoTDevice: Response
    deactivate Gateway

```


## Tasks Overview

```mermaid
graph TD
  subgraph SystemSetup
    InstallTimeSeriesDB
    ConfigureDatabase
    DesignSchema
  end

  subgraph WriteAPI
    DevelopAPI
    ImplementBatching
  end

  subgraph Testing
    UnitTesting
    IntegrationTesting
    PerformanceOptimization
  end

  subgraph Documentation
    SystemArchitecture
    SetupGuide
    APIDocumentation
  end

  subgraph Monitoring
    SetMonitoringTools
    ScalingStrategies
  end

  SystemSetup --> WriteAPI
  WriteAPI --> Testing
  Testing --> Documentation
  Documentation --> Monitoring

````
