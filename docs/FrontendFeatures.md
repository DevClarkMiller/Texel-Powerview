# Texel4Trading PowerView - App Features & Requirements

## 1. Project Overview

**Vision Statement:** PowerView aims to become the leading independent monitoring and analytics platform for distributed solar energy systems.
**Goal:** A unified monitoring solution that consolidates data from different inverter brands into a single platform with consistent formatting and reporting.

---

## 2. Target Groups & Role-Based Access (RBAC)

The app must support different user roles with specific access levels:

### A. Consumers (Solar Panel Owners)

- **Access:** Only to their own panels/inverters.
- **Features:**
    - Real-time on/off status.
    - Current wattage production.
    - Historical production charts (daily/weekly/monthly).
    - Notifications if production stops.

### B. Texel4Trading (Fleet Managers)

- **Access:** Full access to all data produced by monitoring devices.
- **Features:**
    - All Consumer features.
    - Advanced energy production analytics.
    - Alerts for non-working panels for servicing.
    - Fleet overview (multi-inverter monitoring).

### C. Texel Power Company (Grid Operators)

- **Access:** High-level overview of total power production.
- **Features:**
    - Summary of total energy produced across the network.
    - Regional distribution of power production.

---

## 3. Functional Requirements

### 3.1 Authentication & Authorization

- **Microsoft Integration:** Login must be handled via Microsoft (Azure AD) using `@azure/msal-react`.
- **Role Management:** Display and restrict features based on the user's role.

### 3.2 Inverter Monitoring

- **Universal Support:** Support data from various manufacturers (SolarEdge, etc.) using the custom monitoring device.
- **Key Metrics to Display:**
    - **Voltage (V):** DC and AC (Phase L1, L2, L3) voltages.
    - **Wattage (W):** Current power being produced.
    - **Energy Output (kWh):** Cumulative production (daily/lifetime).
    - **Status:** On/Off/Fault states.
    - **System Temperature:** Heatsink and component temperatures.

### 3.3 Analytics & Visualization

- **Real-time Updates:** Data should poll every 30-60 seconds without full page refreshes.
- **Historical Trends:** Interactive charts (Area Charts recommended for cumulative production).
- **Time Range Switching:** Switch views between Daily, Weekly, and Monthly.

### 3.4 Alerts & Notifications

- **Fault Detection:** Early detection of performance issues or system failures.
- **Connectivity Alerts:** Detect if a monitoring device goes offline.
- **Service Requests:** Automatic alerts for Texel4Trading when maintenance is required.

---

## 4. Technical Specifications

### 4.1 Frontend Stack

- **Framework:** React (Functional Components + Hooks).
- **Styling:** SCSS (feature-based modular structure).
- **Charts:** Recharts (AreaCharts, BarCharts).
- **State Management:** TanStack Query (Data fetching/caching) + React Context (Auth/User role).
- **Icons:** Lucide-React.

### 4.2 API Integration

- **Backend:** Monitoring device API (currently mocked).
- **Endpoints Needed:**
    - `GET /api/devices`: List all registered inverters.
    - `GET /api/latest-data?ipAddress={ip}`: Real-time metrics for a specific device.
    - `GET /api/historical-data?ipAddress={ip}&limit={n}`: Historical data for charts.

---

## 5. UI/UX Design Guidelines

- **Density & Clarity:** Focus on providing clear data for "Power Users".
- **Units:** Always display units clearly (kWh, kW, V, %).
- **Color Coding:**
    - Yellow/Gold: Solar Production.
    - Red/Blue: Consumption (if applicable).
- **Inverted Pyramid Design:** Most important metrics (e.g., "Current Total Output") at the top-left, followed by detailed charts.
- **Empty States:** Clear "No Data Found" or "Offline" states for inverters.

---

## 6. Implementation Roadmap (Next Steps)

1. [ ] **MSAL Integration:** Set up Microsoft login and wrap the app in `MsalProvider`.
2. [ ] **Role-Based Routing:** Implement protected routes and sidebar links based on user roles.
3. [x] **Real Historical Data:** Replace mock charts in `Dashboard.tsx` with data from `getHistoricalData`.
4. [x] **Advanced Analytics:** Implement cumulative production charts (kWh over time).
5. [ ] **Alerts System:** Create a notification tray/component for system faults.
6. [ ] **Responsive Refinement:** Optimize the dashboard for mobile and tablet views.
