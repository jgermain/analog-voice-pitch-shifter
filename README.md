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

# What I Learned

- How analog multipliers (AD633) perform frequency translation
- Stability limitations of LM741 on single-supply audio signals
- Biasing microphones for op-amp audio conditioning
- How COS and SIN carrier frequency influences pitch shift
- Layout considerations for ±15 [V] analog circuits
- Noise reduction using capacitive coupling
