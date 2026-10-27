# Tomato Sorting Machine

An ESP32-based sorter that reads a tomato's colour and classifies it as raw (green), ripe (red) or rotten (dark, grey or brown), then turns a servo gate to send it to the matching bin.

> **About this repository:** I first built a tomato sorting project during my B.Tech. The original files were lost, so this is a rebuild from scratch in 2026 using the same idea. This version uses a colour sensor, and the code and thresholds still need testing and calibration on real hardware (see the test log below).

[Add a photo or short demo video of your build here]

## Why this project

Sorting produce by hand is slow and inconsistent. Colour is a simple signal for ripeness, and an ESP32 with a colour sensor is a cheap way to automate the decision.

## How it works

1. The TCS34725 sensor measures red, green, blue and clear light from the tomato under its own white LED.
2. The ESP32 normalises the colour by the clear channel and converts it to hue and saturation.
3. A simple rule classifies the tomato: very dark or grey means rotten, red hues mean ripe, green hues mean raw, and other hues (orange, yellow, brown) are treated as rotten.
4. A servo gate turns to the matching bin, then returns to its home position when the tomato has left.

## Hardware

- ESP32 dev board
- TCS34725 colour sensor
- SG90 servo
- Small tray or ramp, three bins, jumper wires
- 5 V power supply

Wiring is in [docs/wiring.md](docs/wiring.md).

## Software

- Arduino IDE with the ESP32 board package
- Libraries: Adafruit TCS34725, ESP32Servo
- Sketch: [code/tomato_sorter/tomato_sorter.ino](code/tomato_sorter/tomato_sorter.ino)

## How to run it

1. Wire the parts as in [docs/wiring.md](docs/wiring.md).
2. Open the sketch in the Arduino IDE, select your ESP32 board and upload.
3. Set `CALIBRATION_MODE = true` first, read the values for your own tomatoes in the Serial Monitor (115200 baud), and adjust the thresholds.
4. Set `CALIBRATION_MODE = false`, re-upload, and place a tomato at the sensing spot.

## Test log

Fill this in after you test your build.

| Tomato | Expected | Result | Notes |
|---|---|---|---|
| | | | |

## Limitations

- Colour thresholds depend on lighting and the sensor's distance, so recalibrate if either changes.
- A colour sensor can't see surface damage, so a rotten tomato that is still red may be classified as ripe.
- It handles one tomato at a time.

## What's next

- Replace the colour rules with a small neural network trained on photos of raw, ripe and rotten tomatoes (for example with an ESP32-CAM).
- Add a conveyor so tomatoes arrive continuously.

## Repository structure

```
code/tomato_sorter/tomato_sorter.ino   ESP32 sketch
docs/wiring.md                         wiring and set-up notes
README.md
```
