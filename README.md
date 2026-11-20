# Control Tow Pump By PLC

A PLC-based control system for two water pumps, programmed in Function Block Diagram (FBD) using **Siemens LOGO!**. The system alternates operation between Pump 1 and Pump 2 with a single push button, ensures that only one pump runs at a time, records each pump's operating time, and shows the live status on the LOGO! display.

---

##  Overview

In water pumping stations, running one pump all the time wears it out quickly while the second pump stays idle. This project solves that by **alternating** between two pumps, so the usage is shared equally and both pumps last longer. Runtime counters help plan maintenance, and the display gives the operator instant feedback.

##  Key Features

- **Alternating operation:** the system switches between Pump 1 and Pump 2.
- **Equal usage distribution:** balances the load between both pumps.
- **Interlock protection:** prevents both pumps from running at the same time.
- **Runtime monitoring:** an operating-hours counter for each pump supports maintenance planning.
- **Visual status indication:** the LOGO! display shows each pump's state and total running time.
- **Expandable design:** extra sensors and conditions can be added easily.

##  Inputs and Outputs

| Type | Name | Description |
|---|---|---|
| Input | I1 (START) | Push button that activates the system |
| Output | Q1 | Pump 1 control (relay / contactor) |
| Output | Q2 | Pump 2 control (relay / contactor) |
| Constant | High (hi) | Constant logic 1 that keeps the display message active |

##  Function Blocks

| Block | Type | Function |
|---|---|---|
| B005 | RS latch | Main system latch, activated by START and enables both pump branches |
| B003 | RS latch | Memory of Pump 1 selection |
| B004 | RS latch | Memory of Pump 2 selection |
| B001 | AND gate | Pump 1 runs only if the system is ON and Pump 1 is selected |
| B002 | AND gate | Pump 2 runs only if the system is ON and Pump 2 is selected |
| B007 | Operating hours counter | Counts total running time of Pump 1 (Q1) |
| B008 | Operating hours counter | Counts total running time of Pump 2 (Q2) |
| B006 | Message text | Displays pump states and total times on the LOGO! screen |


##  How It Works

1. The user presses **START (I1)**.
2. The main latch **B005** turns the system on and enables both pump branches.
3. The selection latches **B003 / B004** decide which pump runs; only one is active at a time.
4. The matching AND gate (**B001** or **B002**) drives the output **Q1** or **Q2**.
5. The hour counter of the running pump (**B007** or **B008**) starts counting.
6. When the pump is switched, the other pump takes over and its counter starts.
7. The display (**B006**) updates continuously with both pumps' status and times.

```
START → B005 (System latch) ─┬─ B003 ─ B001 (AND) ─ Q1 ─ B007 (Pump 1 timer)
                             └─ B004 ─ B002 (AND) ─ Q2 ─ B008 (Pump 2 timer)

High → B006 (Message text) → LOGO! Display
```

##  Display Output

The LOGO! display shows information like this:

```
PUMP 1 ON
TOTAL TIME
0h 1m
PUMP 2 OFF
TOTAL TIME
0h 0m
```

##  How to Run

1. Install **LOGO!Soft Comfort** .
2. Open the project file `Project control tow pump.[lsc]` from this repository.
3. Run the **simulation** mode.
4. Press the **I1 (START)** button and watch Q1 and Q2 and the display change.
5. To use on real hardware, download the program to a [LOGO! model] and connect Q1 and Q2 to the pump relays or contactors.

##  Expected Results

| Condition | Q1 (Pump 1) | Q2 (Pump 2) | Display |
|---|---|---|---|
| System off | Off | Off | Both pumps OFF |
| Pump 1 selected | On | Off | PUMP 1 ON, time counting |
| Pump 2 selected | Off | On | PUMP 2 ON, time counting |

##  Possible Improvements

- Automatic switching based on a time interval.
- Fault detection such as overload and dry-run protection.
- Tank level control with a float switch or analog sensor (PID).
- SCADA or IoT monitoring.

##  Repository Structure

```
├── Project control tow pump.[lsc]               # LOGO!Soft Comfort project file
├── Documentation/
│   └── Project_control_tow_pump.pdf # Full project report
├── Images/
│   └── FBD-Diagram.png              # Function Block Diagram
└── README.md
```

##  Skills Demonstrated

- PLC programming with Function Block Diagram (FBD)
- Latching and interlock logic design
- Operating-hours counters and maintenance monitoring
- HMI message display configuration
- Industrial automation for water pumping systems



