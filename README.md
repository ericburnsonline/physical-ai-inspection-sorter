# Physical AI Inspection Sorter

A modular Physical AI platform for vision-based inspection, classification, singulation, and automated sorting of real-world objects.

## Status

**Early prototype / architecture phase**

This project is currently being developed from the mechanical and system architecture outward. Initial work focuses on object handling, camera-based inspection, electromechanical actuation, and a software pipeline that can later move from PC-based development to edge AI hardware.

The first planned application is **coin inspection and sorting**, but the platform is intentionally designed to support other workloads such as:

- Electronic components and memory modules
- Industrial parts
- Stator faces and similar machined components
- Salvage and recycling inventory
- Small-part quality inspection
- Other visually identifiable physical objects

## Why This Project Exists

Many AI demonstrations stop after identifying an object on a screen.

This project explores the next step:

**Can an AI-enabled system reliably interact with the physical world?**

The goal is to build a small but realistic platform that combines:

- Physical material handling
- Object singulation
- Sensors
- Machine vision
- Computer vision and AI
- Decision logic
- Electromechanical actuation
- Automated sorting
- Telemetry and event logging
- Failure detection and recovery
- Human review of uncertain results

The project is also intended as a hands-on learning environment for skills relevant to:

- Physical AI
- Industrial automation
- Machine vision
- Edge AI
- Robotics
- Solutions Engineering
- Sales Engineering
- Forward Deployed Engineering
- Field Applications Engineering
- Customer Support Engineering

## Initial Use Case: Coin Inspection

The first workload will use mixed coins as inexpensive, highly variable physical objects.

Coins provide useful real-world machine-vision challenges including:

- Different sizes and thicknesses
- Reflective surfaces
- Wear and corrosion
- Scratches and damage
- Similar visual appearance
- Dates and mint marks
- Foreign coins and tokens
- Unknown objects mixed into bulk material

The initial system will focus on basic denomination recognition and physical sorting.

Future experiments may include:

- Year recognition
- Mint mark recognition
- Heads / tails identification
- Anomaly detection
- Interesting-coin detection
- Confidence-based routing
- Human review queues
- Foreign coin and token detection

The system is not intended to perform automatic coin appraisal. Potentially interesting or uncertain objects can instead be routed to a manual review bin.

## Planned Architecture

```text
Bulk Objects
     |
     v
+-------------+
|   Hopper    |
+-------------+
     |
     v
+-------------+
| Singulator  |
+-------------+
     |
     v
+-------------+
|   Sensor    |
+-------------+
     |
     v
=====================================
        Inspection Conveyor
=====================================
                 |
                 v
        +----------------+
        | Camera / Vision|
        +----------------+
                 |
                 v
        +----------------+
        | Classification |
        |   / Decision   |
        +----------------+
                 |
                 v
        +----------------+
        | Controller     |
        +----------------+
                 |
                 v
        +----------------+
        | Sort / Reject  |
        +----------------+
```

## Prototype Hardware

Hardware currently available for early development includes:

### Vision

- Logitech Brio webcam
- Logitech C920 webcam

The initial prototype will use a conventional USB camera before moving to dedicated machine-vision or depth hardware.

### Control

- Arduino-compatible microcontrollers
- Stepper motors
- Linear actuators
- Servos and other electromechanical components

### Compute

Initial development will run on a conventional PC.

Future versions may migrate inference and control workloads to edge hardware such as:

- NVIDIA Jetson
- Raspberry Pi with AI acceleration
- Other embedded AI platforms

This allows the project to compare development systems with production-style edge deployment.

### Material Handling

A small conveyor approximately **8 inches wide by 36 inches long** is currently planned.

Bulk feeding and singulation may use:

- Custom rotating-disc mechanisms
- Salvaged coin-handling hardware
- Repurposed consumer coin sorters
- Parking-system coin mechanisms
- Custom stepper-driven feeders

## Design Principles

### Modular

The inspection system should not depend on coins specifically.

Object feeding, machine vision, classification, control, actuation, and telemetry should remain separable modules.

### Observable

The system should record what happened during each inspection.

Example event:

```json
{
  "object_id": "000184",
  "classification": "quarter",
  "confidence": 0.984,
  "route": "BIN_3",
  "inference_ms": 43,
  "result": "pass"
}
```

Future telemetry may include:

- Images
- Confidence scores
- Inference latency
- Sensor states
- Actuator states
- Error conditions
- Device temperature
- Throughput
- Reject rate
- Jam rate

### Failure-Aware

Real physical systems fail.

Planned experiments will deliberately introduce conditions such as:

- Poor lighting
- Camera movement
- Dirty optics
- Double feeds
- Conveyor jams
- Sensor failures
- Network outages
- Controller disconnects
- Inference failures
- Incorrect configuration
- Low-confidence classifications

These failures will be documented along with detection methods, troubleshooting procedures, and corrective actions.

### Human in the Loop

The system should not force a decision when confidence is low.

Objects may be routed into categories such as:

```text
PASS
SORT
REJECT
UNKNOWN
MANUAL REVIEW
```

## Development Roadmap

### Phase 0: Architecture

- Define system architecture
- Establish repository structure
- Document available hardware
- Define initial use cases
- Identify mechanical constraints

### Phase 1: Vision Prototype

- Capture images using USB webcam
- Detect individual objects
- Perform initial classification
- Record confidence scores
- Save inspection events

### Phase 2: Motion

- Add conveyor
- Control conveyor from microcontroller
- Detect object arrival
- Stop object in inspection position
- Trigger image capture

### Phase 3: Physical Sorting

- Add sorting gate or diverter
- Route objects based on software decision
- Track successful and failed sorts

### Phase 4: Bulk Feeding

- Add hopper
- Develop or adapt singulation mechanism
- Detect double feeds
- Measure jams and feed reliability

### Phase 5: Advanced Vision

- Improve lighting
- Improve image consistency
- Add OCR where useful
- Detect dates and other fine details
- Add anomaly detection

### Phase 6: Telemetry and Supportability

- Event logging
- Performance metrics
- Failure injection
- Troubleshooting documentation
- Health monitoring

### Phase 7: Edge AI

- Migrate inference from development PC to edge device
- Benchmark performance
- Measure latency
- Measure power and thermal behavior
- Document deployment process

### Phase 8: Additional Workloads

Adapt the platform to other objects such as:

- RAM / DIMMs
- Industrial components
- Stators
- Salvage inventory
- Manufactured parts

## Repository Structure

```text
physical-ai-inspection-sorter/
|
+-- README.md
+-- LICENSE
|
+-- docs/
|   +-- architecture.md
|   +-- roadmap.md
|   +-- design-goals.md
|   +-- lessons-learned.md
|
+-- hardware/
|   +-- bom.md
|   +-- conveyor/
|   +-- singulator/
|   +-- camera-mount/
|   +-- sorting-mechanism/
|
+-- software/
|   +-- vision/
|   +-- controller/
|   +-- telemetry/
|
+-- experiments/
|   +-- camera-tests/
|   +-- lighting-tests/
|   +-- singulation-tests/
|
+-- images/
```

## Engineering Experiments

The project will emphasize measured results instead of only demonstrations.

Example singulation test:

```text
Test: 500 mixed coins

Successful feeds: 487
Double feeds: 7
Jams: 3
Edge feeds: 3

Successful singulation rate: 97.4%
```

Mechanical changes can then be tested against the same workload.

This creates a repeatable way to improve the system rather than relying on subjective observations.

## Longer-Term Goal

The long-term goal is not simply to build a coin sorter.

The goal is to create a reusable **Physical AI inspection and automation platform** that demonstrates how software, AI, sensors, controls, mechanical systems, and operational support work together.

The same platform should eventually be useful for demonstrations, technical training, experimentation, portfolio development, and potentially real-world automation projects.

## License

This project is released under the MIT License.

See [LICENSE](LICENSE) for details.
