Example of ESP32-based device irrigation control webserver interface.

feedLogic()
├── Pre-Checks
│   ├── ❌ SERVICE_MODE? → RETURN
│   ├── ❌ PUMP_ACTIVE? → RETURN  
│   └── ❌ COOLDOWN_ACTIVE? → RETURN
│
├── Emergency Watering (BYPASSES ALL PHASES)
│   ├── ✅ MOISTURE_DIFF > MAX_DRYBACK(45%)?
│   │   └── 💧 WATER(P2_SHOT) → RETURN
│
├── Phase Check
│   ├── P3 PHASE ❌ (!isIrrigationWindow())
│   │   ├── 🔄 RESET_MAINTENANCE_PHASE
│   │   └── RETURN (NO WATERING)
│   │
│   └── P1/P2 PHASE ✅ (isIrrigationWindow())
│       ├── P1 Phase (!MAINTENANCE)
│       │   ├── ✅ MOISTURE_DIFF > P1_DRYBACK(0%)?
│       │   │   └── 💧 WATER(P1_SHOT)
│       │   │
│       │   └── ✅ HIGHEST_MOISTURE ≥ TARGET?
│       │       └── 🔄 SWITCH_TO_P2_PHASE
│       │
│       └── P2 Phase (MAINTENANCE)
│           └── ✅ MOISTURE_DIFF > P2_DRYBACK(6%)?
│               └── 💧 WATER(P2_SHOT)
│
└── Daily Reset
    └── ✅ LIGHTS_ON_TIME + NEW_DAY?
        ├── 🔄 RESET_HIGHEST_MOISTURE
        └── 🔄 RESET_DAILY_WATER
