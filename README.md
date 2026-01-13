# Keypad Matrix Design & Debugging  
### Using Helmut Neemann Digital Logic Simulator

## Overview
This repository documents the complete process of designing and debugging a **keypad matrix using pure digital logic** in the **Helmut Neemann Digital Simulator**.

The focus of this project is **not just the final circuit**, but the **step-by-step debugging journey**:
- Starting from a basic keypad matrix
- Understanding why incorrect outputs occur
- Applying one-hot encoding
- Detecting multiple key presses
- Stabilizing outputs using latching logic

This repository serves as a **learning reference** for keypad scanning and digital input systems.

---

## Tool Used
- **Helmut Neemann – Digital Logic Simulator**

---

## Objective
- Design a keypad matrix that uniquely identifies key presses
- Avoid ghosting and ambiguous outputs
- Detect and analyze multiple key presses
- Hold a key state until the next valid press
- Understand the difference between combinational and sequential logic in input systems

---

## Step 1: Basic Keypad Matrix
A row–column keypad matrix was created using basic logic gates.

### Observed Issues
- Multiple columns became HIGH for a single key press
- No unique key identification
- Output ambiguity due to shared logic paths

**Conclusion:**  
A raw keypad matrix is insufficient for unique key detection.

---

## Step 2: Logic Analysis
At this stage, the main problem was identified:
- Each key press must map to a **unique output**
- Multiple active paths caused false detections

This led to the exploration of encoding methods.

---

## Step 3: One-Hot Encoding Implementation
Each key was mapped to a **unique one-hot output line**.

### Results
- Clean and unique key identification
- Only one output HIGH per valid key press

### New Issue
- Multiple key presses caused multiple outputs to go HIGH
- No mechanism to resolve simultaneous presses

---

## Step 4: Multiple Key Press Detection
Intentional multiple key presses were tested:
- Same row
- Different rows and columns

### Observations
- System detected multiple active outputs
- No priority or press validation existed

**Conclusion:**  
One-hot encoding does not prevent multi-press conflicts.

---

## Step 5: Sequential Scanning using Ring Counter
A **ring counter** was introduced to activate rows sequentially.

### Improvements
- Controlled row activation
- Reduced ghosting effects
- More predictable key detection

### Remaining Issue
- Output changed while a key was held
- Previous key state was not retained

---

## Step 6: Latching / Hold-State Logic
A latching circuit was added to stabilize the output.

### Purpose
- Capture the detected key output
- Hold the output until the next valid key press
- Prevent output flickering during long presses

### Final Behavior
- One stable output per key press
- Output remains latched
- New press updates the state only after release

---

## Final Logic Flow
1. Ring counter activates one row
2. Column logic detects key press
3. One-hot encoding ensures unique output
4. Latch stores the key state
5. Output remains stable until next press

---

## Key Learnings
- Combinational logic alone is insufficient for keypad systems
- One-hot encoding simplifies decoding but requires control logic
- Multiple key press detection is unavoidable and must be handled
- Sequential logic is essential for human input systems
- Latching is critical for stable outputs

---

## Common Issues Debugged
- Multiple outputs HIGH simultaneously
- First and last columns activating together
- Output changing while key is held
- No memory of previous key press

Each issue is addressed incrementally in this repository.

---

## Why This Repository
This project demonstrates:
- Digital logic design fundamentals
- Systematic debugging methodology
- Real-world keypad input challenges
- Clear separation of combinational and sequential logic

---

## Author
**Megha Akku Mathew**  
Digital Logic | Embedded Systems | Hardware Design
