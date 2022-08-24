# Carbon dioxide (CO<sub>2</sub>) alarm

## Table of Contents

- [Carbon dioxide (CO<sub>2</sub>) alarm](#carbon-dioxide-cosub2sub-alarm)
  - [Table of Contents](#table-of-contents)
  - [Hardware Requirements](#hardware-requirements)
  - [Assembly and wiring](#assembly-and-wiring)
    - [LiPo SHIM for Pico](#lipo-shim-for-pico)
    - [Buzzer](#buzzer)
    - [SCD41 CO2 Sensor](#scd41-co2-sensor)
    - [Diagram](#diagram)
  - [Software and installation](#software-and-installation)
    - [Prerequisites](#prerequisites)
    - [Instalation](#instalation)

## Hardware Requirements

- 1x [Raspberry Pi Pico](https://www.raspberrypi.com/products/raspberry-pi-pico/)
- 1x [SCD41 CO2 Sensor by Pimoroni](https://shop.pimoroni.com/products/scd41-co2-sensor-breakout?variant=39652270833747)
- 1x [Buzzer 5V by Adafruit](https://www.adafruit.com/product/1536)
  - NOTE: can be substituted with regular [piezo buzzer](https://www.adafruit.com/product/160)
  - OBSERVATION: this seemed louder than a regular piezo while playing around with them
- (Optional) 1x [LiPo SHIM for Pico by Pimoroni](https://shop.pimoroni.com/products/pico-lipo-shim?variant=32369543086163)
  - For wired operation this is not required
  - NOTICE: installing headers onto the Pico is recommended
  - NOTE: Pimoroni sells these built into their own Pico models with [4MB](https://shop.pimoroni.com/products/pimoroni-pico-lipo?variant=39386149093459) and [16MB](https://shop.pimoroni.com/products/pimoroni-pico-lipo?variant=39335427080275) of flash memory.
- (Optional) 1x 3.7V rechargeable battery
  - [6700mAh lithium ion battery](https://shop.pimoroni.com/products/high-capacity-lithium-ion-battery-pack?variant=32012684591187)
- Solder, soldering iron and wires to conenct everything together
- (Optional) Breadboard for testing
- (Optional) Headers for the Pico and the CO2 sensor make testing easy

## Assembly and wiring

- [Raspberry Pi Pico documentation and pinout](https://www.raspberrypi.com/documentation/microcontrollers/raspberry-pi-pico.html)
- [SCD41 CO2 Sensor by Pimoroni schematic](https://cdn.shopify.com/s/files/1/0174/1800/files/scd41_breakout_schematic.pdf)
- [LiPo SHIM for Pico schematic](https://cdn.shopify.com/s/files/1/0174/1800/files/lipo_shim_for_pico_schematic.pdf)

### LiPo SHIM for Pico

> [You'll need to solder the SHIM to the back of your Pico, with the power button at the same end as the USB port. The text on the SHIM and the pin labels on the back of the Pico should be facing each other.](https://shop.pimoroni.com/products/pico-lipo-shim?variant=32369543086163)

### Buzzer

- Positive pin -> GPIO 15 (pin 20)
- Negative pin -> GND (pin 18)
  - NOTE: any GND pin is okay

### SCD41 CO2 Sensor

- 3-5V -> 3V3 (pin 36)
- SDA -> GPIO 4 (pin 6)
- SCL -> GPIO 5 (pin 7)
- GND -> GND (pin 8)
  - NOTE: any GND pin is okay

### Diagram

<figure>
    <img src="./assets/diagram.png" width="650" height="473"
         alt="Wiring diagram.">
    <figcaption>Wiring diagram.</figcaption>
</figure>

- Sensor shown on the diagram is made by Adafruit and is only a reference. (Couldn't find a model made by Pimoroni.)
  - [Adafruit SCD-41](https://www.adafruit.com/product/5190)

## Software and installation

### Prerequisites

- Install the latest version of [Pimoroni's custom MicroPython](https://github.com/pimoroni/pimoroni-pico) which includes the libraries necessary to use their products. [Follow their installation guide.](https://github.com/pimoroni/pimoroni-pico/blob/main/setting-up-micropython.md)

### Instalation

**1. Clone the repository.**

``` shell
git clone https://github.com/KollerFerenc/CO2Alarm-MicroPython
```

**2. Connect the Raspberry Pi Pico to the computer.**

**3. Launch [Thonny IDE](https://thonny.org/) or the Python IDE of your choice.**

**4. Open the python files in the IDE and save them to the Pico.**
   - src -> main.py
   - src -> buzzers.py

**5. Buzzer selection**

In main.py uncomment which type of buzzer you are using.

*A. Regular piezo buzzer*

```python
# NOTICE: buzzer selection!

# Use this with the 5V Buzzer by Adafruit (https://www.adafruit.com/product/1536)
# BUZZER = Buzzer3v5v(BUZZER_PIN)

# Use this with any regular piezo buzzer
BUZZER = PiezoBuzzer(BUZZER_PIN)
```

*B. [Buzzer 5V by Adafruit](https://www.adafruit.com/product/1536)*

```python
# NOTICE: buzzer selection!

# Use this with the 5V Buzzer by Adafruit (https://www.adafruit.com/product/1536)
BUZZER = Buzzer3v5v(BUZZER_PIN)

# Use this with any regular piezo buzzer
# BUZZER = PiezoBuzzer(BUZZER_PIN)
```

Save the modified file to the Pico.

**6. (Optional) Adjust the values in the Configurables section to match your setup.**

Save the modified file to the Pico.
