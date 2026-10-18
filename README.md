# Analog Voice Pitch Shifter

Built with LM741/UA741 op-amps and AD633 analog multipliers. This project implements an analog voice pitch shifter (also known as a voice modulator) using multiple LM741 op-amps and two AD633N analog multipliers. The microphone signal is amplified, filtered, and then multiplied with a cosine carrier to shift its spectral content and change the perceived pitch. The design is fully analog and powered from ±15 V, making it ideal for exploring practical analog signal processing, op-amp behavior, and multiplier-based frequency translation.

# Features

- Analog pitch shifting using spectral translation
- Microphone preamplifier based on LM741
- Band-pass / coupling capacitors for voice-band conditioning
- Two AD633N multiplier stages for spectral shifting
- COS oscillator source driving the AD633
- ±15 V op-amp power rails for maximum headroom
- Output suitable for audio amplifiers or headphones (buffering recommended)

# How the Circuit Works
1) Microphone Input Stage (U1)
   - The microphone passes through a 47 nF coupling capacitor
   - The LM741 provides initial gain and biasing
   - This stage conditions the small microphone signal into a line-level signal
2) Signal Conditioning & Filtering (U2 + RC Network)
   - Additional LM741 stages filter and stabilize the voice signal
   - Capacitors (10 nF, 0.1 µF, etc.) prevent DC offset and shape frequency response
   - Resistor network sets gain
3) Carrier Generation
   - Sin and Cos waves were produced from the same waveform generator to ensure same clock timing
4) Analog Multiplication (U3: AD633N)
   - The filtered voice enters X1/X2 inputs
   - COS/SIN drives Y1
   - The AD633 internally computes: V_O = [(X1-X2)(Y1-Y2)]/10
   - This produces sum and difference frequencies, shifting the pitch
5) Output Stage / Coupling Capacitors
   - 0.1 µF capacitors AC-couple the final output
   - Noise is reduced before the audio leaves the circuit

  # Components Used
  1) Active Devices
     - LM741 / UA741 op-amps × 3
         - Preamp
         - Filters
         - Buffer
     - AD633N analog multipliers × 2
         - Frequency Shifting
         - Addition of both shifted waves for cancelation
  2) Passive Components
     - Resistors: 1 MΩ, 22 kΩ, etc.
     - Capacitors: 47 nF, 10 nF, 0.1 µF, 10 pF
     - Microphone


# Experimental Results

The analog voice frequency shifter was constructed on a
breadboard and evaluated using an oscilloscope, waveform
generators, and a multimeter.

| Parameter | Measured Result |
|---|---|
| Voltage Gain | 19.4 V/V |
| Signal-to-Noise Ratio | 43.17 dB |
| Total Power Consumption | 0.334 W |
| Microphone Frequency Range Observed | 250–1250 Hz |
| Frequency Conversion Test | 200 Hz input → 401.2 Hz output |

### Gain Measurement

A 100 mV peak-to-peak input signal produced a measured
output of 1.94 V peak-to-peak.

This corresponds to a voltage gain of:

$$
A_v = \frac{1.94}{0.1} = 19.4
$$

### Signal-to-Noise Ratio

Using the measured output signal and noise amplitudes:

- Signal: 10.08 Vpp
- Noise: 0.07 Vpp

The calculated signal-to-noise ratio was:

$$
SNR = 20\log_{10}\left(\frac{10.08}{0.07}\right)
\approx 43.17\text{ dB}
$$

### Power Consumption

Measured power consumption across the 5 V and ±15 V
supplies totaled approximately 0.334 W.

### Frequency-Shifting Test

With a 200 Hz test input and 200 Hz quadrature reference
signals, an output frequency of 401.2 Hz was observed.

This demonstrates the frequency-conversion behavior
of the analog multiplier circuit under the tested conditions.

### Hardware Implementation

The circuit was assembled and demonstrated using
AD633 analog multipliers and 741 operational amplifiers.

During testing, the op-amp configuration was adjusted
to improve the desired frequency-shifted output.

The original circuit schematic documents the initial design;
the final breadboard implementation includes modifications
made during testing.


# What I Learned

- How analog multipliers (AD633) perform frequency translation
- Stability limitations of LM741 on single-supply audio signals
- Biasing microphones for op-amp audio conditioning
- How COS and SIN carrier frequency influences pitch shift
- Layout considerations for ±15 [V] analog circuits
- Noise reduction using capacitive coupling
