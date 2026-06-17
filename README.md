


Synthewi is a portable digital synthesizer built around the **ESP32-S3**. The hardware has been designed from the ground up to provide a compact musical instrument combining capacitive touch sensing, real-time sound synthesis, battery operation, and an intuitive user interface.

The synthesizer integrates:

- ESP32-S3 microcontroller
- 8 capacitive touch keys
- 2 octave shift touch buttons
- 8 analog potentiometers
- Rotary encoder
- 1.8" TFT LCD display
- 3-position waveform selector
- Integrated Li-Ion battery charger and protection
- USB programming interface
- Speaker amplifier
- Audio Jack output

---

# 2.1 3D PCB Model

The following images illustrate the complete mechanical appearance of the synthesizer PCB.

| Isometric View | Perspective View |
|---------------|------------------|
| ![](https://github.com/bejaouihamza/Synthewi/blob/main/synthewi_3d_model_1.png) | ![](https://github.com/bejaouihamza/Synthewi/blob/main/synthewi_3d_model_2.png)|


The PCB has been designed as a fully integrated synthesizer platform where every interface required for sound generation is directly available on-board.

---

# 2.2 Hardware Overview

The synthesizer combines multiple subsystems:

- ESP32-S3 processor
- 1.8" TFT Display
- Rotary Encoder
- Eight capacitive touch keys
- Two octave touch buttons
- Eight analog potentiometers
- Three-position waveform selector
- Speaker
- Audio Jack output
- USB programming interface
- Battery Management System
- 3.3V power supply

The following labeled image identifies every major hardware block.

<p align="center">

![](Images/synthewi_with_labels.png)

</p>

---

# 2.3 User Interface

The objective of the hardware is to make sound design intuitive while minimizing menu complexity.

When powered on, the LCD displays the synthesizer menu.

The rotary encoder allows the user to navigate through the available menus, select parameters, and validate settings.

| LCD Menu | Rotary Encoder |
|----------|----------------|
| ![](Images/lcd_display.png) | ![](Images/rotary_encoder(2).png) |

The display acts as the central interface for configuring every sound parameter of the synthesizer.

---

# 2.4 Waveform Selector

The synthesizer features a dedicated three-position hardware selector used to instantly switch between the three primary oscillator waveforms.

- Square Wave
- Triangle Wave
- Sawtooth Wave

![](Images/waveform_selector(2).png)

Unlike software-only synthesizers, the physical selector allows immediate waveform switching during live performance.

---

# 2.5 ADSR Envelope Controls

Four dedicated potentiometers control the envelope generator.

![](Images/adsr_envelope.png)

These controls adjust:

- Attack
- Decay
- Sustain
- Release

The ADSR envelope determines how the amplitude of each note evolves over time.

---

# 2.6 Sound Effect Controls

Another set of four potentiometers provides real-time sound shaping.

![](Images/sound_effects.png)

These controls are used for tuning synthesis parameters such as filters, modulation, resonance, or additional sound effects depending on the firmware configuration.

---

# 2.7 Capacitive Touch Keyboard

The keyboard consists of eight capacitive touch electrodes.

![](Images/touch_pads.png)

Each pad corresponds to a musical note.

When a finger approaches a copper pad, the ESP32-S3 measures the increase in capacitance and triggers the corresponding oscillator frequency.

This approach eliminates mechanical switches, improves durability, and provides a smooth playing experience.

---

# 2.8 Octave Shifter

Two additional touch electrodes allow the performer to change the active octave.

![](Images/octave_shifter.png)

The octave controls extend the playable range without increasing the PCB dimensions.

---

# 2.9 Capacitive Touch Sensing

Synthewi uses the native capacitive sensing peripheral integrated inside the ESP32-S3.

Each copper electrode forms one plate of a capacitor.

When a finger approaches the electrode, the effective capacitance increases.

The ESP32 continuously measures this capacitance variation and determines whether the pad is touched.

This sensing method provides:

- No mechanical wear
- Fast response
- Low power consumption
- High reliability

---

# 2.10 Wiring Diagram

The overall hardware interconnection is illustrated below.

![](Images/wirring_diagram.png)

The ESP32-S3 communicates with every peripheral including:

- TFT Display
- Touch Sensors
- Audio Amplifier
- Rotary Encoder
- Analog Multiplexer
- Battery Management System

---

# 2.11 Complete Schematic

The complete electrical schematic was designed using KiCad.

![](Images/full_schematic.png)

The design is organized into multiple functional blocks which are explained individually below.

---

# 2.12 ESP32-S3 Module

![](Images/esp32s3_n8r2.png)

The ESP32-S3 is the heart of the synthesizer.

It performs:

- Audio synthesis
- Touch sensing
- Display control
- Menu management
- I2S audio transmission
- ADC acquisition
- Rotary encoder decoding

---

# 2.13 USB Interface

![](Images/usb_connector.png)

The USB interface provides:

- Firmware programming
- Serial communication
- Power input

An ESD protection IC protects the USB data lines from electrostatic discharge.

---

# 2.14 Battery Management System

![](Images/bms.png)

Battery charging is handled by the TP4056.

Protection against:

- Overcharge
- Over-discharge
- Over-current

is provided by the DW01A protection circuit.

---

# 2.15 Power Path and Voltage Regulation

![](Images/power_path_orring_and_3.3v_regulator.png)

The power stage automatically selects between USB power and battery power.

An OR-ing circuit prevents reverse current.

The AMS1117 regulator generates the regulated 3.3V supply used by the ESP32-S3 and peripherals.

---

# 2.16 TFT Display

![](Images/1.8_inch_display.png)

A 1.8-inch SPI TFT display provides:

- User menus
- Parameter visualization
- Configuration feedback

---

# 2.17 Rotary Encoder

![](Images/rotary_encoder.png)

The rotary encoder provides intuitive menu navigation.

Its quadrature outputs allow the firmware to determine both rotation direction and speed.

---

# 2.18 Waveform Selector Circuit

![](Images/waveform_selector.png)

The selector connects three hardware positions to GPIO inputs, allowing immediate waveform selection.

---

# 2.19 Analog Multiplexer

![](Images/8_potentiometers_with_mux.png)

Since the ESP32-S3 has a limited number of ADC channels, an analog multiplexer is used.

It sequentially connects the eight potentiometers to the ADC, reducing GPIO usage while maintaining full control over all synthesis parameters.

---

# 2.20 Audio Amplifier

![](Images/audio_amp_and_speaker.png)

Digital audio generated by the ESP32-S3 is transmitted through the I2S peripheral.

The amplifier converts the digital stream into an analog signal capable of driving the onboard speaker.

---

# 2.21 Audio Jack Output

![](Images/jack_connector.png)

A dedicated headphone jack provides external audio output.

A low-pass filter removes unwanted high-frequency switching components before the signal reaches the connector.

---

# 2.22 PCB Layout

The synthesizer is implemented on a four-layer PCB.

### Top Layer

![](Images/layout_top_layer.png)

Contains:

- Components
- High-speed routing
- Touch electrodes

---

### Inner Layer 1

![](Images/layout_inner_layer1.png)

Dedicated ground plane providing:

- Signal return paths
- Reduced EMI
- Stable reference for capacitive sensing

---

### Inner Layer 2

![](Images/layout_inner_layer2.png)

Primarily used for power distribution and internal routing.

---

### Bottom Layer

![](Images/layout_bottom_layer.png)

Contains additional routing, passive components, and connectors.

---

# Capacitive Touch Considerations

The PCB stack-up directly influences touch sensitivity.

Parameters such as:

- Copper thickness
- Dielectric thickness
- Ground plane distance

affect the electric field generated by each touch electrode.

A thinner dielectric between the touch electrode and the ground plane increases parasitic capacitance, reducing sensitivity. Conversely, increasing the dielectric thickness generally improves touch detection range by reducing baseline capacitance.

Careful optimization of the PCB stack-up was therefore an important aspect of the Synthewi hardware design.
