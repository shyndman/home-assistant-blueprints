# Home Assistant Blueprints

This repository contains a collection of Home Assistant blueprints.

## Blueprints

All blueprints can be found in the `/blueprints` directory.

### Advanced Room Lighting Blueprint

A highly responsive, comfortable, and intelligent lighting automation for a single room that uses two-stage presence detection with self-contained state memory.

#### Features

- **Two-Stage Presence Detection**: Combines a fast-reacting radar sensor with precise camera-based person detection
- **Instant-On Capability**: Lights turn on immediately when movement is detected
- **Smart Memory System**: Automatically remembers and restores lighting state when you quickly return to a room
- **Night Mode Support**: Configurable settling period to avoid jarring light changes at night
- **Self-Contained**: No need to create helper entities - the blueprint manages its own state memory
- **Area-Based Control**: Automatically controls all lights and switches in the selected area

#### How It Works

##### Room Entry
1. **Radar Detection**: Fast radar sensor triggers initial dim lighting
2. **Person Confirmation**: Camera sensor confirms human presence within 5 seconds
3. **Memory Check**: If you recently left the room, your previous lighting state is instantly restored
4. **Light Progression**: If no memory exists, lights progress from dim to bright (with optional night mode settling)

##### Room Exit
1. **Person Departure**: Camera sensor detects person leaving
2. **Memory Creation**: Current lighting state is automatically saved
3. **Dim State**: Lights immediately dim to comfortable level
4. **Room Empty**: Radar sensor confirms room is empty, lights turn off (memory preserved)

#### Required Entities

##### Sensors
- **Radar Presence Sensor**: Fast-reacting presence detection (e.g., millimeter-wave radar)
- **Camera Person Sensor**: Precise human detection (e.g., camera with person detection)
- **Night Mode Sensor**: Binary sensor indicating when it's nighttime

##### Target
- **Light Target Area**: Home Assistant area containing the lights/switches to control

#### Configuration Parameters

| Parameter | Description | Default | Range |
|-----------|-------------|---------|-------|
| **Settle Time** | Night mode settling duration before brightening | 60s | Any duration |
| **Memory Duration** | How long to remember previous lighting state | 600s (10min) | Any duration |
| **Dim Brightness** | Brightness for intermediate dim state | 10% | 1-100% |
| **Dim Color Temperature** | Color temperature for dim state | 2700K | 2000-6500K |
| **Bright Brightness** | Brightness for final bright state | 100% | 1-100% |
| **Bright Color Temperature** | Color temperature for bright state | 3000K | 2000-6500K |
