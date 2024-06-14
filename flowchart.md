```mermaid
flowchart TD
A[Initialization] --> B[Main Loop]
B --> C[Check for IR Remote Commands]
C --> D{Power Button Pressed?}
D --> E[Toggle System State ON/OFF]
D --> F{Volume Up Button Pressed?}
F --> G[Increase Volume]
F --> H{Volume Down Button Pressed?}
H --> I[Decrease Volume]
H --> J{Reset Button Pressed?}
J --> K[Reset Game]
E --> L{System ON?}
L --> M[Update Game Display]
L --> N[Check Ultrasonic Sensor]
L --> O[Wait for Next Command]
M --> P[Scroll Row Left and Right]
P --> Q[Draw Screen]
N --> R[Measure Distance]
R --> S{Distance Valid?}
S --> T[Turn on LED if 100-800mm]
S --> U[Turn off LED]
S --> V[Ignore Invalid Measurements]
C --> O
O --> B

subgraph Button Pressed ISR
W[Button Pressed] --> X[Debounce Button]
X --> Y[Increment Row Count]
Y --> Z[Combine Current and Previous Row]
Z --> AA[Calculate New Block Size]
AA --> AB[Play Sound Effect]
AB --> AC{Top Row Reached?}
AC --> AD[Open Servo]
end

subgraph Power Down System
AE[Set All Pins to INPUT]
end

subgraph Power Up System
AF[Set All Pins to OUTPUT]
AF --> AG[Reinitialize Setup]
end

subgraph Open Servo
AH[Move Servo to 90 Degrees]
AH --> AI[Move Servo Back to 0 Degrees]
end

subgraph Reset Game
AJ[Reset Game Variables]
AJ --> AK[Reset Display Rows]
end

B --> W
B --> AE
B --> AF
B --> AH
B --> AJ
