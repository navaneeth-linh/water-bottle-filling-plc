💧 Water Bottle Filling System (Single Bottle)

A PLC ladder logic simulation of an automatic single-bottle water filling system built using CodeSys. The system fills one bottle at a time with a 3-second fill cycle, counts completed bottles, and includes emergency stop safety logic.


📹 Demo Video


🎥 Watch Simulation Video on YouTube ← Replace this with your YouTube link




📌 Project Overview

FieldDetailsPlatformCodeSys (Simulation)LanguageLadder Diagram (LD)CycleSingle bottle fill per cycleFill Time3 seconds per bottle (TON T#3S)SafetyEmergency Stop (Estop) included


🔌 I/O Table

Inputs

VariableTypeDescriptionSTARTBOOLStart button — initiates the systemSTOPBOOLStop button — halts the current cycleBOTTLEBOOLBottle presence sensorSENSORBOOLFill level / bottle detection sensorBSBOOLBottle in position sensor — triggers fill sequenceRESETBOOLResets the bottle counter (CTU)EstopBOOLEmergency stop — immediately cuts valve and motor

Outputs

VariableTypeDescriptionMOTORBOOLConveyor motor — moves bottle into fill positionvalveBOOLFill valve — opens to fill the bottleBKBOOLInternal flag — signals fill cycle completeSKBOOLInternal flag — conveyor step control

Timers & Counters

BlockTypeSettingDescriptionTON_0TONT#3SFill timer — keeps valve open for 3 secondselapsed_timeTIME—Tracks elapsed fill timeCTU_0CTUpreset_valueCounts completed bottlescurrent_valueWORD—Current bottle count displayRTIGG_1R_TRIG—Rising edge trigger for counter pulse


🔄 System Sequence

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


🧩 Ladder Logic — Rung Breakdown

RungLogicDescription1START + SK → MOTOR, STOP + EstopMotor start/stop with interlock2BS → SET STOPBottle sensor stops conveyor when bottle in position3STOP → SET valve, TON 3s → RESET valve, SET BK, RESET STOPFill valve control with timer4BK → SKSignals conveyor to move to next position5BK + R_TRIG → CTU count up, RESET → CTU resetBottle counter logic6Estop → RESET valve, RESET STOPEmergency stop safety rung


📁 Repository Structure

water-bottle-filling-plc/
├── media/
│   ├── image.png                                  ← Visualization screenshot
│   └── Water Bottle LD (single bottle at a time).pdf  ← Full ladder logic PDF
├── README.md


🛠️ Tools Used


CodeSys 3.5 — PLC programming and simulation
Ladder Diagram (LD) — Programming language
Soft PLC simulation — No physical hardware required



👤 Author

Navaneeth
B.Tech — Electrical and Electronics Engineering
Muthoot Institute of Science & Technology, Kerala

Show Image


📜 License

This project is open source and available for educational use.
