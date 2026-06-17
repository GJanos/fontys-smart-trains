# Smart Trains

An embedded IoT system that reduces platform congestion at train stations by guiding
passengers toward the least-crowded wagons, spreading boarding evenly across the platform.
A group project completed during an Erasmus semester at Fontys University of Applied
Sciences (Netherlands).

> *The problem: congestion at certain points on a station platform during peak hours slows
> boarding and alighting. By directing passengers toward less-crowded wagons, load spreads
> evenly across the train and platform — improving station throughput and fewer missed
> trains.*

**Tech stack:** C++ · PlatformIO · ESP32 · MQTT · CAN bus

## Architecture

Two cooperating embedded subsystems communicating over MQTT:

- **`station/`** — the platform-side controller. Connects to the train over MQTT, requests
  train info, and drives RGB LED indicators per platform position to direct passengers.
- **`wagon/`** — the on-train controller. Tracks per-seat occupancy via button sensors,
  runs a state machine, and reports crowding over CAN (`CanManager`/`CanEvent`) and MQTT.

```
station/   include/ + src/   TrainStation, Platform, Train, RGBLED, MQTTServer
wagon/     include/ + src/   Wagon, Seat, ButtonSensor, StateMachine, CanManager, MQTTServer
```

See `Analysis.pdf` and `Design.pdf` for the full requirements and design.

## Build & upload

Each subsystem is a separate PlatformIO project:

```bash
cd station && pio run            # build (add -t upload to flash an ESP32)
cd wagon   && pio run
```

---

*Fontys (Erasmus) group project. Embedded C++ on ESP32 with MQTT and CAN-bus
communication between distributed nodes.*
