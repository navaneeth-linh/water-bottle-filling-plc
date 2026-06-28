# 💧 Water Bottle Filling System (Single Bottle)

A PLC ladder logic simulation of an automatic single-bottle water filling system built using **CodeSys**. The system fills one bottle at a time with a 3-second fill cycle, counts completed bottles, and includes emergency stop safety logic.

---

## 📹 Demo Video

> 🎥 [Watch Simulation Video on YouTube](#) ← *Replace this with your YouTube link*

---

## 📌 Project Overview

| Field | Details |
|---|---|
| **Platform** | CodeSys (Simulation) |
| **Language** | Ladder Diagram (LD) |
| **Cycle** | Single bottle fill per cycle |
| **Fill Time** | 3 seconds per bottle (TON T#3S) |
| **Safety** | Emergency Stop (Estop) included |

---

## 🔌 I/O Table

### Inputs

| Variable | Type | Description |
|---|---|---|
| `START` | BOOL | Start button — initiates the system |
| `STOP` | BOOL | Stop button — halts the current cycle |
| `BOTTLE` | BOOL | Bottle presence sensor |
| `SENSOR` | BOOL | Fill level / bottle detection sensor |
| `BS` | BOOL | Bottle in position sensor — triggers fill sequence |
| `RESET` | BOOL | Resets the bottle counter (CTU) |
| `Estop` | BOOL | Emergency stop — immediately cuts valve and motor |

### Outputs

| Variable | Type | Description |
|---|---|---|
| `MOTOR` | BOOL | Conveyor motor — moves bottle into fill position |
| `valve` | BOOL | Fill valve — opens to fill the bottle |
| `BK` | BOOL | Internal flag — signals fill cycle complete |
| `SK` | BOOL | Internal flag — conveyor step control |

### Timers & Counters

| Block | Type | Setting | Description |
|---|---|---|---|
| `TON_0` | TON | `T#3S` | Fill timer — keeps valve open for 3 seconds |
| `elapsed_time` | TIME | — | Tracks elapsed fill time |
| `CTU_0` | CTU | `preset_value` | Counts completed bottles |
| `current_value` | WORD | — | Current bottle count display |
| `RTIGG_1` | R_TRIG | — | Rising edge trigger for counter pulse |

---

## 🔄 System Sequence

```
START pressed
    → MOTOR turns ON (conveyor runs)
        → BS sensor detects bottle in position
            → STOP set (conveyor stops)
            → valve OPEN (fill starts)
                → TON_0 starts counting 3 seconds
                    → After 3s: valve CLOSES
                    → BK flag set (cycle done)
                    → CTU_0 increments count
                    → SK triggers next conveyor step
                        → Cycle repeats for next bottle

ESTOP pressed at any point
    → valve immediately RESET (closed)
    → STOP immediately RESET
    → System halts safely
```

---

## 🧩 Ladder Logic — Rung Breakdown

| Rung | Logic | Description |
|---|---|---|
| 1 | `START` + `SK` → `MOTOR`, `STOP` + `Estop` | Motor start/stop with interlock |
| 2 | `BS` → SET `STOP` | Bottle sensor stops conveyor when bottle in position |
| 3 | `STOP` → SET `valve`, TON 3s → RESET `valve`, SET `BK`, RESET `STOP` | Fill valve control with timer |
| 4 | `BK` → `SK` | Signals conveyor to move to next position |
| 5 | `BK` + R_TRIG → CTU count up, `RESET` → CTU reset | Bottle counter logic |
| 6 | `Estop` → RESET `valve`, RESET `STOP` | Emergency stop safety rung |

---

## 📁 Repository Structure

```
water-bottle-filling-plc/
├── media/
│   ├── image.png                                  ← Visualization screenshot
│   └── Water Bottle LD (single bottle at a time).pdf  ← Full ladder logic PDF
├── README.md
```

---

## 🛠️ Tools Used

- **CodeSys 3.5** — PLC programming and simulation
- **Ladder Diagram (LD)** — Programming language
- **Soft PLC simulation** — No physical hardware required

---

## 👤 Author

**Navaneeth**
B.Tech — Electrical and Electronics Engineering
Muthoot Institute of Science & Technology, Kerala

[![GitHub](https://img.shields.io/badge/GitHub-navaneeth--linh-181717?style=flat&logo=github)](https://github.com/navaneeth-linh)

---

## 📜 License

This project is open source and available for educational use.
