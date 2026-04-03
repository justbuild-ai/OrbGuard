# OrbGuard

**Autonomous orbital situational awareness and debris avoidance system**

There are over 27,000 tracked debris objects in Earth orbit and an estimated 500,000+ fragments too small to track — yet large enough to disable or destroy an active satellite on impact. As orbital congestion accelerates, the window between debris detection and catastrophic collision is measured in minutes or seconds. Ground-based monitoring and manual response are no longer sufficient at scale.

OrbGuard is a system architecture exploration and early-stage R&D project aimed at building an autonomous, onboard orbital situational awareness and collision avoidance pipeline — one that detects, predicts, and responds to debris threats without depending on ground uplink latency.

---

## 🎯 System Vision

A fully realized OrbGuard system operates across three layers:

```
[ SENSE ]          [ REASON ]            [ ACT ]
Hull Inspection → Situational Awareness → Avoidance Control
ai_hull_inspection   OrbGuard Core          Thruster / Alert Interface
```

**Sense** — Onboard camera and edge AI inference detects hull surface anomalies and impact damage in real time. See: [ai_hull_inspection](https://github.com/justbuild-ai/ai_hull_inspection)

**Reason** — OrbGuard ingests external debris tracking data, computes conjunction risk, and maintains a local threat model updated independently of ground station contact.

**Act** — When collision probability exceeds defined thresholds, OrbGuard triggers avoidance maneuvers, safe-mode transitions, or priority alerts to ground operations — autonomously or with operator confirmation depending on mission profile.

---

## 🌐 Market Context

The on-orbit servicing, assembly, and manufacturing (OSAM) market is projected to exceed $4B by 2030. Autonomous spacecraft operations — including collision avoidance — are identified as a critical capability gap by NASA, ESA, and commercial operators alike. Current solutions are ground-dependent, latency-constrained, and do not scale to the debris environment projected through 2035.

Key drivers:
- **Kessler Syndrome risk** — cascading debris collisions could render entire orbital shells unusable
- **Mega-constellation growth** — Starlink, OneWeb, and others are adding thousands of satellites to already congested orbits
- **Latency gap** — ground-based avoidance maneuver commands can take hours; onboard autonomous response operates in seconds
- **Regulatory pressure** — FCC, ITU, and ESA are tightening debris mitigation requirements for new launches

---

## 🏗️ Architecture (Design Stage)

### Data Inputs
- **External debris catalogs** — Space-Track.org (18th Space Defense Squadron), LeoLabs, ESA DISCOS, NASA ODPO
- **TLE / orbital element sets** — Two-Line Element data for conjunction analysis
- **Onboard sensor feeds** — Camera inputs from hull inspection layer
- **Ephemeris data** — Spacecraft state vectors for relative position computation

### Core Modules (Planned)

```
OrbGuard/
├── ingestion/          # Debris catalog parsers (TLE, JSON, CSV)
├── conjunction/        # Conjunction analysis and probability computation
├── threat_model/       # Local threat state, object tracking, risk scoring
├── avoidance/          # Maneuver planning and decision logic
├── alerts/             # Notification pipeline (ground uplink, onboard log)
├── simulation/         # Orbital mechanics sandbox for testing
├── api/                # Interface layer for sensor inputs (hull inspection, etc.)
└── config/             # Mission profile parameters and thresholds
```

### Design Principles
- **Edge-first** — core threat assessment runs onboard without ground dependency
- **Modular** — each layer (sense, reason, act) is independently testable
- **Mission-configurable** — avoidance thresholds and response profiles adapt to mission type (LEO constellation, GEO comsat, crewed vehicle)
- **Fail-safe** — degraded mode operation when external data feeds are unavailable

---

## 🔬 Current Status

This repository is in active design and early scaffolding phase.

| Layer | Status |
|---|---|
| Hull inspection / damage sensing | ✅ Prototype built — see [ai_hull_inspection](https://github.com/justbuild-ai/ai_hull_inspection) |
| Debris dataset research | 🔲 Space-Track, LeoLabs, ESA DISCOS identified |
| TLE ingestion module | 🔲 Architecture defined, implementation pending |
| Conjunction analysis | 🔲 Design stage |
| Avoidance decision logic | 🔲 Concept stage |
| Simulation environment | 🔲 Planned |
| Ground alert interface | 🔲 Planned |

---

## 🔗 Related Projects

- [ai_hull_inspection](https://github.com/justbuild-ai/ai_hull_inspection) — Edge AI damage detection on Hailo-8L NPU. Provides the onboard sensing layer that feeds into OrbGuard's situational awareness pipeline.

---

## 📚 Reference & Inspiration

- [Space-Track.org](https://www.space-track.org) — 18th Space Defense Squadron debris catalog
- [LeoLabs](https://leolabs.space) — Commercial space domain awareness
- [ESA Space Debris Office](https://www.esa.int/Space_Safety/Space_Debris)
- [NASA Orbital Debris Program Office](https://orbitaldebris.jsc.nasa.gov)
- Kessler & Cour-Palais (1978) — foundational collision cascade analysis

---

*OrbGuard is an independent R&D project exploring autonomous space safety systems. Not affiliated with any spacecraft operator or government program.*
