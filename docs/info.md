## How it works

This project is a classic **Two-Stage CMOS Operational Amplifier** designed using the SkyWater 130nm technology node. It is optimized for general-purpose analog signal processing applications, providing a balance between high gain and wide bandwidth.

The architecture consists of three main blocks:
1.  **Differential Input Stage:** A PMOS differential pair (to improve flicker noise performance and input common-mode range near ground) with an NMOS current mirror active load. This stage provides the majority of the voltage gain.
2.  **Second Gain Stage (Class A):** A Common-Source NMOS amplifier with a PMOS active load. This stage provides additional gain and maximizes the output voltage swing.
3.  **Miller Compensation:** A compensation capacitor ($C_c$) and a nulling resistor are placed between the output and the input of the second stage. This ensures closed-loop stability by pole-splitting and eliminating the Right-Half-Plane (RHP) zero.

**Key Specifications (Simulation Results):**
* **Supply Voltage:** 1.8 V
* **DC Gain:** > 76 dB
* **Gain Bandwidth Product (GBW):** ~100 MHz (at 2pF load)
* **Phase Margin:** Designed for > 60°
* **Slew Rate:** > 20 V/µs
* **Load Capacitance:** 2 pF

## How to test

To test the functionality of the Op-Amp, you will need a standard lab setup with a voltage source, function generator, and oscilloscope.

### Pinout Mapping
The design uses the analog I/O pins of the Tiny Tapeout multiplexer:
* **ua[0]:** Non-Inverting Input ($V_{in+}$)
* **ua[1]:** Inverting Input ($V_{in-}$)
* **ua[2]:** Output ($V_{out}$)

### Test Configuration: Unity Gain Buffer
The simplest way to verify the Op-Amp is to configure it as a voltage follower (unity gain buffer).

1.  **Power Up:** Apply 1.8V to the chip supply ($V_{DD}$) and connect Ground ($V_{SS}$).
2.  **Feedback Connection:** Connect the Output pin (**ua[2]**) directly to the Inverting Input pin (**ua[1]**) using an external wire or breadboard connection.
3.  **Input Signal:** Apply a sine wave (e.g., 10 kHz, 100mVpp with 0.9V DC offset) to the Non-Inverting Input pin (**ua[0]**).
4.  **Observation:** Monitor **ua[0]** (Input) and **ua[2]** (Output) on an oscilloscope.
    * *Expected Result:* The output signal should be a replica of the input signal (same amplitude and phase).

### Test Configuration: Inverting Amplifier
1.  Connect a resistor $R_1$ (e.g., 10k$\Omega$) between the signal source and **ua[1]**.
2.  Connect a feedback resistor $R_f$ (e.g., 100k$\Omega$) between **ua[1]** and **ua[2]**.
3.  Connect **ua[0]** to a DC reference voltage (e.g., 0.9V).
4.  Apply a small AC signal to the input of $R_1$.
    * *Expected Result:* The output should be an amplified (Gain = $-R_f/R_1$) and inverted version of the input.

## External hardware

This project is a standalone analog block, but requires standard external components for testing:

* **Power Supply:** Stabilized 1.8V DC source.
* **Function Generator:** Capable of generating sine/square waves with adjustable DC offset.
* **Oscilloscope:** To observe input and output waveforms.
* **Passive Components:** Resistors and Capacitors for configuring feedback loops on a breadboard.
