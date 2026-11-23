# ApexCell — Unified EV Cost, Trip & Battery Insights Platform

> **ApexCell** — Enterprise EV Decision Workspace  
> **Theme:** Energy, Clean Mobility & Sustainable Fleet Intelligence  
> **Engineering Lead:** Koteswara Rao Koniki  

A modern, privacy-first EV decision platform that empowers Indian EV owners, prospective buyers, and sustainable fleet managers to calculate accurate running savings, simulate highway journeys with **live GPS mapping**, and estimate real-world range and long-term battery degradation.

---

## ⚡ Key Capabilities

- **100% Client-Side Privacy:** Zero server latency, no telemetry tracking, and zero mandatory cloud logins or paid API keys.
- **Dual-Engine Google Maps & GPS Highway Route Planner:**
  - **Native Google Maps Integration:** Supports the Google Maps JavaScript API with DirectionsService, custom high-contrast SVG charging pins, responsive InfoWindows, and dynamic Live Traffic Layer toggle.
  - **1-Click Google Maps App Deep Linking:** Launches the full driving route with all calculated highway charging stop waypoints directly in the native Google Maps app (`google.com/maps/dir`) on Android, iOS, or desktop without requiring any API key.
  - **OpenStreetMap & OSRM Engine:** Zero-configuration fallback with real road geometry from OpenStreetMap and the OSRM highway routing engine.
- **Unified Reactive Context:** A centralized vehicle and tariff configuration profile dynamically updates financial calculations, highway charging stops, and real-world range across the entire workspace.
- **Curated Indian Presets:** Pre-loaded specifications for popular Indian electric vehicles (*Tata Nexon EV, Punch EV, MG Windsor, Mahindra XUV400, Tata Tiago EV, BYD Atto 3*), State DISCOM residential electricity tariffs (*MSEDCL, BESCOM, BSES, TANGEDCO, TSSPDCL*), and major DC fast charging networks (*Tata Power EZ Charge, Jio-bp Pulse, Statiq*).
- **Design System:** Built with an accessible, high-contrast palette: Deep Forest Green (`#0B3D2E`), EV Green (`#16A34A`), Warning Amber (`#F59E0B`), Danger Red (`#DC2626`), and Light Slate (`#F8FAFC`). Fully responsive with a mobile collapsible menu.

---

## 📁 Project Architecture

```
apexcell/
├── index.html              # Landing page with executive hero, instant presets & feature showcases
├── profile.html            # Shared EV & tariff configuration with Indian presets
├── cost.html               # Module A: EV vs Petrol running costs, payback horizon & CO2 avoided
├── trip.html               # Module B: Highway trip planner with Google Maps, GPS routing & stop timeline
├── range.html              # Module C: Real-world range multi-factor estimator & battery health risk
├── about.html              # Assumptions, engineering formulas, platform boundaries & team credits
├── README.md               # Architecture documentation & setup guide
├── css/
│   └── styles.css          # Design system, accessible cards, Leaflet map styling & responsive layout
└── js/
    ├── data.js             # Curated Indian vehicle specs, GPS corridors, tariffs & constants
    ├── main.js             # Shared state (localStorage sync), persistent top summary bar & toasts
    ├── cost.js             # Financial savings & carbon emissions calculation engine
    ├── trip.js             # Dual Google Maps & GPS highway routing engine with charging stops & live traffic
    └── range.js            # Multi-factor range penalty model & battery risk assessment
```

---

## 🗺️ Interactive GPS Highway Corridors Included

1. **Bengaluru to Chennai (NH 48 / NH 44)** — $350\text{ km}$ via Krishnagiri & Vellore
2. **Delhi to Jaipur (NH 48)** — $280\text{ km}$ via Gurugram, Neemrana & Behror
3. **Mumbai to Pune (Yashwantrao Chavan Expressway)** — $150\text{ km}$ via Khalapur & Lonavala
4. **Hyderabad to Vijayawada (NH 65)** — $275\text{ km}$ via Suryapet & Kodad
5. **Delhi to Chandigarh (NH 44)** — $250\text{ km}$ via Murthal, Karnal & Ambala
6. **Custom Route Mode** — Dynamic GPS interpolation along national highway vectors

---

## 🧮 Mathematical Formulations

### Module A: EV vs. Petrol Cost & Carbon Reductions
- **Monthly Distance:** $D_{\text{month}} = D_{\text{daily}} \times 30$
- **EV Monthly Cost:** $C_{\text{EV}} = (D_{\text{month}} / \eta_{\text{EV}}) \times \text{Tariff}_{\text{kWh}}$
- **Petrol Monthly Cost:** $C_{\text{Petrol}} = (D_{\text{month}} / \eta_{\text{Petrol}}) \times \text{Price}_{\text{Litre}}$
- **Payback Horizon:** $T_{\text{Payback}} = \Delta \text{Purchase Price} / ((C_{\text{Petrol}} - C_{\text{EV}}) \times 12)$
- **Net CO2 Avoided:** Derived from Central Electricity Authority (CEA) Indian Grid baseline ($0.716\text{ kg CO}_2/\text{kWh}$) and standard petrol emissions ($2.31\text{ kg CO}_2/\text{L}$).

### Module B: GPS Highway Trip & Charging Stops
- **Safe Initial Leg Range:** $D_{\text{safe}} = \text{Capacity} \times \left(\frac{\text{SoC}_{\text{start}} - \text{SoC}_{\text{reserve}}}{100}\right) \times \eta_{\text{EV}}$
- **Charging Stop Logic:** Triggers a fast-charge stop before battery drops below arrival reserve (default 15%).
- **Charging Window:** Charges up to 80% to avoid thermal throttling and CC-CV taper delays.
- **Charging Duration:** $t_{\text{charge}} = (E_{\text{needed}} / (P_{\text{charger}} \times \eta_{\text{charger}})) \times 60\text{ min}$ (with $\eta_{\text{charger}} = 0.90$).

### Module C: Real-World Range & Battery Health
- **Multi-Factor Range Penalty:** $R_{\text{real}} = R_{\text{ideal}} \times (k_{\text{speed}} \cdot k_{\text{AC}} \cdot k_{\text{load}} \cdot k_{\text{terrain}} \cdot k_{\text{style}})$
- **Battery Health Risk:** Educational scoring matrix evaluating daily charge target (anode stress above 80%) and DC fast charging frequency (thermal degradation).

---

## 🚀 How to Run the Application

Because ApexCell is completely standalone:
1. Double-click `index.html` to open it in any web browser (Chrome, Edge, Firefox, Safari).
2. Or start a local web server:
   ```powershell
   cd "C:\Users\chala\.gemini\antigravity\scratch\apexcell"
   python -m http.server 8080
   ```
3. Open `http://localhost:8080` in your browser.
