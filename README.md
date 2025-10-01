# MPU6050 Airplane Demo (Arduino Nano Every + GY-521)

Hands-on project to control a virtual airplane in real time using an **Arduino Nano Every** and a **GY-521 (MPU-6050 IMU)**. This is quite an easy setup because of the prerequisites by [Jeff Rowberg](https://github.com/jrowberg) and [Karsten Schmidt](https://github.com/postspectacular). But I wanted to make it work easily because it's my first time working with an GY-521 :)


https://github.com/user-attachments/assets/34b4fe16-4162-49a7-ae1e-5d0926705feb



## Features
- Real-time motion tracking with MPU-6050 (gyro + accelerometer).
- Arduino Nano Every runs Jeff Rowberg’s MPU6050 DMP firmware.
- Processing visualizer shows a live 3D airplane model.
- Adjusted axes & alignment fixes for Nano Every + GY-521.

## Hardware
- Arduino Nano Every  
- GY-521 (MPU-6050) breakout  
- Wires (I²C)
- Breadboard

## Dependencies
As mentioned, you'll need to use:
- [Jeff Rowberg’s i2cdevlib](https://github.com/jrowberg/i2cdevlib)  
  Used for the Arduino MPU6050 + I2Cdev libraries. Licensed under MIT.
- [toxiclibs v0021](https://github.com/postspectacular/toxiclibs/releases/tag/0021)  
  Used in the Processing visualizer for quaternion/axis-angle math. Licensed under LGPL.

**Wiring:**

| GY-521 | Nano Every |
|--------|------------|
| VCC    | 5V         |
| GND    | GND        |
| SDA    | SDA        |
| SCL    | SCL        |

# 1. Setup

### Arduino
1. Install [Arduino IDE](https://www.arduino.cc/en/software).
2. Install **Arduino megaAVR Boards** (for Nano Every).
3. Download and import [Jeff Rowberg’s i2cdevlib](https://github.com/jrowberg/i2cdevlib) and manually move the I2Cdev and MPU6050 libraries to /Arduino/libraries
4. Clone this repo, open `arduino/MPU6050_DMP6/MPU6050_DMP6.ino`.
5. Make sure that //#define OUTPUT_READABLE_YAWPITCHROLL (somewhere around line 103 is disabled and #define OUTPUT_TEAPOT is enabled (somewhere around line 120)

<img width="626" height="362" alt="Screenshot 2025-10-01 at 11 12 56" src="https://github.com/user-attachments/assets/9e32de9d-69d3-40e0-bd4d-b8a10ac1cce9" />

7. Upload to Nano Every.
8. To start DMP processing (and to see data e.g. in serial monitor), you'll have to enter any character first. Do that and then close the serial monitor so the port isn't busy.

### Processing
1. Install [Processing IDE](https://processing.org/download).
1. Download [toxiclibs-complete-0021.zip](https://github.com/postspectacular/toxiclibs/releases/tag/0021) (Hint: this is the release I've been using).
2. Extract into your Processing sketchbook’s `libraries/` folder (basically the same as with Arduino libraries).
3. Restart Processing.
3. Open `processing/AirplaneDemo.pde`.
5. Adjust serial port name if needed like this: I disabled "String portName = Serial.list()[0];" and enabled "String portName = "COM";" to enter my own serial port name. You'll get that by running it once to see the ports being shown in the termin. Copy the right one and add them to the portName = " ". It's the same as it is in Arduino IDE.

   <img width="625" height="138" alt="Screenshot 2025-10-01 at 11 16 45" src="https://github.com/user-attachments/assets/6b1d34eb-541e-4129-b1da-d97661ee5735" />
   
7. Upload the script and make sure that the rotations are correct. You'll see that it'll work when there's lines being generated in the terminal and the demo is popping up.

<img width="793" height="835" alt="Screenshot 2025-10-01 at 11 49 42" src="https://github.com/user-attachments/assets/e81ace6d-3e32-4bde-a2a8-bd947463c3ae" />


### Hints
- Rotation can be wrong depending on the rotation of your GY521 and other parameters. You can change the orientation of the plane e.g. with "rotateY(HALF_PI);" (or other values of PI)
- If an axis are e.g. inverted, you can adapt that by adapting: "rotate(axis[0], -axis[1], axis[3], axis[2]);"

<img width="638" height="258" alt="Screenshot 2025-10-01 at 11 23 23" src="https://github.com/user-attachments/assets/cce183a2-902b-41bb-94c1-ab9392fa7461" />


## 📄 License
MIT — see [LICENSE](LICENSE). 

Based on [Jeff Rowberg’s i2cdevlib](https://github.com/jrowberg/i2cdevlib), MIT license and [toxiclibs v0021 (https://github.com/postspectacular/toxiclibs/releases/tag/0021), LGPL license.
