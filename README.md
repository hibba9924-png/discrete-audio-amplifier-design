# discrete-audio-amplifier-design
A multi-stage audio amplifier built entirely from discrete MOSFETs and BJTs (no ICs), designed to amplify a millivolt-level microphone signal into enough power to drive an 8 Ω speaker.

Overview

This project builds a complete audio signal chain in four stages: a MOSFET pre-amplifier (high input impedance, for the microphone), a BJT pre-amplifier (additional voltage gain), a PNP driver stage, and a Class AB push-pull power output stage. Each stage was designed by hand-calculation, simulated in LTspice, then built and tested on breadboard hardware.

Tools & Components

LTspice (simulation)
Proteus (schematic/layout)
MOSFET (2N7000), NPN/PNP BJTs (2N3904, TIP122/TIP127)
Resistors, capacitors, diodes (1N4007) for biasing
8 Ω speaker, electret microphone, 24V DC supply, heat sinks

How it works

MOSFET pre-amp (M1): common-source stage with high input impedance, amplifies the mV-level mic signal

BJT pre-amp (Q5): common-emitter stage for additional voltage gain (~44x), unbypassed emitter resistor for stability

PNP driver (Q3): boosts current/voltage and prevents loading of the pre-amp stages

Class AB output (Q1/Q2/Q4): complementary push-pull power stage with diode biasing to reduce crossover distortion, delivering 3–5 W to the speaker

Each stage's input impedance was matched to the previous stage's output to prevent signal loss.

Results

Quantity	Simulated (LTspice)	Measured (Hardware)
Input voltage	10 mV	150 mV
Output voltage	8 V	7 V
Voltage gain	800 V/V	46.6 V/V
Verified ±5 V output swing and ~1.5 A peak current drive at the output stage
Confirmed clean, low-distortion sinusoidal output on oscilloscope
Frequency response verified across 100 Hz – 20 kHz bandwidth

What I learned

Impedance matching between cascaded discrete stages is far less forgiving than with integrated op-amps — small mismatches compound across four stages. Simulated and hardware gain values diverged significantly (800 V/V vs 46.6 V/V), which was a useful lesson in how idealized simulation assumptions (exact device parameters, no parasitic loading) break down on a real breadboard.
