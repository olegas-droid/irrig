Example of ESP32-based device irrigation control webserver interface.

Logic
SMART_IRRIGATION
├── PHASE_1: "CLIMB to target moisture after overnight dryback"
├── PHASE_2: "MAINTAIN target moisture with controlled drybacks"  
├── PHASE_3: "RESPECT plant rest periods and allow natural dryback"
├── EMERGENCY: "Save plants from critical stress (bypasses all phases)"
└── TRACKING: "Monitor water efficiency and daily consumption"
