# CampusEats: The Complete Technical Encyclopedia

This encyclopedia provides an exhaustive deep-dive into the CampusEats ecosystem, documenting the "how" and "why" behind every micro-interaction, architectural pivot, and elite-level feature.

---

## I. Architectural Core & Infrastructure

### 1. The Decoupled API (Flask)

The backend operates as a stateless REST service on **Port 5001**.

- **Blueprint Registry**: Every module (Auth, Wallet, Admin, QR) is registered as a Flask Blueprint to ensure modular isolation.
- **Factory Pattern**: Utilizes `create_app()` in `app.py` for clean initialization and environment configuration.
- **ORM (SQLAlchemy)**: Abstracts the SQLite layer, providing a relational model with foreign-key integrity between `Users` and `Transactions`.

### 2. The Persistence Layer (SQLite)

- **Multi-State Schema**: The `Transactions` table was evolved to support a `status` field (`success`, `pending`, `processing`).
- **Absolute Pathing**: Configured in `config.py` to prevent database fragmentation across different execution environments.
- **Atomic Ledgers**: Balance updates and transaction records are executed in single database sessions to prevent financial de-synchronization.

### 3. Identity & Security (JWT)

- **Stateless Auth**: Every request to protected routes must carry an `Authorization: Bearer <JWT>` header.
- **RBAC (Role-Based Access Control)**: Enforced via `require_role` decorators in the backend, ensuring vendors cannot access admin reports and students cannot trigger refunds.

---

## II. Elite Design System: Glassmorphism V2

### 1. The Visual Foundation (`index.css`)

- **Backdrop Blurs**: Heavy use of `backdrop-blur-xl` combined with semi-transparent background colors (`bg-white/5`).
- **Mesh Gradients**: Randomly positioned blur orbs in the background that create a "fluid fintech" atmosphere.
- **Custom Keyframes**:
  - `shimmer`: A linear translation scale used for the predictive forecast panels.
  - `scan`: A rapid vertical translation used in the Vendor QR scanner to simulate laser hardware.
  - `pulse-primary`: A custom opacity-pulse for the main balance display.

### 2. Tailwind Configuration

- **Radius-24**: Overruled standard rounding with a global `24px` border-radius to match premium mobile device curvature.
- **Inter Font-Stack**: Forced the `Inter` font family (900 weight for headers) to ensure a high-load, professional typography layout.

---

## III. Module Deep Dive: Features & Micro-Logic

### 1. Student Intelligence Hub

- **Numerical Ticker (`AnimatedNumber.jsx`)**: A custom hook using `setInterval` that increments the balance display over 500ms, providing a "winning" feel on top-ups.
- **Predictive Engine (`/wallet/projection`)**:
  - **Logic**: Calculates the average of the last 5 deductions to suggest a "Recovery Amount."
  - **Meal Detection**: Client-side logic detects temporal slots (Breakfast, Lunch, Dinner) to predict the cost of the _next_ meal.
  - **Confidence Score**: A mathematical weighted score (0.5 to 0.95) based on the frequency of recent transactions.
- **Reactive Pulsing**: The main balance card glows Emerald for 2000ms whenever a new projection is calculated, signaling "System Intelligence."

### 2. Admin "Intel Core"

- **Framer Motion Staggering**: Uses `variants` and `delay` to ensure components don't pop in simultaneously, but rather "roll" onto the screen in a logical sequence.
- **System Integrity Monitor**: A simulated real-time ping indicator that fluctuates between 8ms and 45ms every 5 seconds, providing a "heartbeat" to the dashboard.
- **Live Event Stream**: A pop-layout list that exits and enters items with physics-based sliding, allowing admins to track global ledger activity in real-time.
- **Time-Series Analysis**: Transitioned from static BarCharts to AreaCharts with gradient-pathing to visualize 7-day transaction growth.

### 3. Vendor universal POS

- **Session Persistence**: React state tracks the total credits "Claimed" and students "Served" for the active browser session, helping vendors keep track of meal throughput.
- **QR Decoding Rhythm**: Implemented high-speed API polling to ensure the scanner feels instantaneous to the user.

---

## IV. Global Utility & Context

### 1. Toast Notification System

- **Context-Driven**: A global `ToastContext.js` allows any functional component to trigger a notification via `showToast()`.
- **States**: Specialized styling for `success` (Emerald), `error` (Rose), and `info` (Blue), all following the glassmorphic design rules.

### 2. API Resilience Utility

- **Interceptors**: Standardized Error handling in `api.js` to automatically redirect users to logout if their token expires, preventing "Ghost States."

---

## V. Developer Operation Matrix

| Task               | Command                                                    | Environment                       |
| :----------------- | :--------------------------------------------------------- | :-------------------------------- |
| **Start Backend**  | `source venv/bin/activate && python app.py`                | Virtual Environment (Python 3.13) |
| **Start Frontend** | `PORT=4000 npm start`                                      | Node.js Runtime                   |
| **Audit DB**       | `sqlite3 campuseats.db "PRAGMA table_info(transactions);"` | CLI                               |
| **Fresh Setup**    | `pip install -r requirements.txt && npm install`           | Global                            |

---

**Documentation Status**: _Master Reference Finalized_
**Technical Level**: _Tier 1 (Complete Coverage)_
