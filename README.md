# Smart-Traffic-Light-Controller
A smart FSM-based traffic light system in Verilog with emergency override and queue logic.

---

# 🚦 Smart Traffic Light Controller (Verilog)

A *Verilog-based Smart Traffic Light Controller* designed using FSM (Finite State Machine) architecture. It simulates intelligent traffic handling based on *car detection, **emergency override, and **queue management. Designed for **simulation using Icarus Verilog* and *waveform visualization using GTKWave*.

---

## 🎯 Key Features

- ✅ *Car/pedestrian detection* via car_detected input  
- 🚨 *Emergency override* logic using emergency signal  
- 🧠 FSM-based traffic light control with intelligent timing  
- 📈 *Queue simulation* through queue_count signal  
- 🔁 Covers *normal, emergency, and queue scenarios*  
- 💬 Well-commented and modular Verilog code

---

## 📂 Project Structure

```
📁 Smart_Traffic_Light-Controller/
├── smart_traffic_light.v        # Main FSM-based Verilog module 
├── basic_tb.v                   # Testbench for standard operation 
├── emergency_tb.v               # Testbench for emergency input handling 
├── queue_tb.v                   # Testbench simulating vehicle queue 
└── README.md                    # This descriptive project overview 
```

---

## 🧩 Module Description

### 📜 smart_traffic_light.v – The Core FSM Logic

| Signal         | Direction | Description                                  |
|----------------|-----------|----------------------------------------------|
| clk          | Input     | System clock                                 |
| rst          | Input     | Active-high reset                            |
| car_detected | Input     | Triggers state change if vehicle is present  |
| emergency    | Input     | Forces RED light for emergency handling      |
| lights       | Output    | One-hot encoded light signals (R, Y, G)      |
| queue_count  | Output    | Simulated vehicle queue (4-bit counter)      |

---

## 🔄 FSM Overview

### 🧠 States and Transitions

| *State*      | *Description*                                                         | *Transition Condition*                                |
|----------------|-------------------------------------------------------------------------|----------------------------------------------------------|
| RED          | Default state. All vehicles must stop. System waits for a car or emergency trigger.     | After 5 clock cycles → RED_YELLOW                      |
| RED_YELLOW   | Prepares traffic to move by warning.                                     | If queue_count > 0 → GREEN, else → RED             |
| GREEN        | Vehicles pass. Queue is reduced.                                         | After 3–6 clock cycles (based on queue) → YELLOW       |
| YELLOW       | Prepares vehicles to stop.                                               | After 2 clock cycles → RED                             |
| EMERGENCY    | Overrides normal flow. All lights go RED for emergency clearance.        | When emergency == 0 → RED                            |

---

### 🔁 Transition Logic

- *Emergency* has highest priority and forces transition to EMERGENCY.
- *Queue Timing*:
  - If queue_count >= 3, GREEN lasts 6 cycles.
  - If less, GREEN lasts 3 cycles.
- *car_detected* input:
  - Increments queue during RED.
  - Decrements queue during GREEN (once per cycle).

---

## 🧪 Testbenches

| File           | Scenario Simulated                  |
|----------------|-------------------------------------|
| basic_tb.v     | Normal traffic light sequencing     |
| emergency_tb.v | Emergency vehicle override (RED)    |
| queue_tb.v     | Dynamic queue-based GREEN extension |

---

## ⚙ Simulation Instructions

### 🧰 Requirements
- [Icarus Verilog](http://iverilog.icarus.com/)
- [GTKWave](http://gtkwave.sourceforge.net/)

### 🏃 Steps to Simulate

1. *Compile the design with your chosen testbench:*
   ```bash
   iverilog -o traffic_test smart_traffic_light.v basic_tb.v

2. Run the compiled simulation:
   ```bash
   vvp traffic_test

4. Visualize the output in GTKWave:
   ```
   gtkwave basic_tb.vcd
   ```

Tip: Replace file name basic_tb with emergency_tb or queue_tb; with respective extensions (.v or .vcd) to test other scenarios.
     
---

## 🛠 Tools Used

| Tool            | Purpose                     |
|-----------------|-----------------------------|
| Icarus Verilog  |	Verilog simulation          |
| GTKWave         |	Viewing .vcd waveform output|
| Verilog HDL     |	Hardware design language    |

