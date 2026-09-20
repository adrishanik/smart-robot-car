# Hardware Engineering & Build Journal: Smart Robot Car

* **Project:** Smart Robot Car
* **Firmware Coding Time:** 1.7 Hours (Logged via Hackatime)
* **Hands-on Hardware Bench Time:** ~8.5 Hours
* **Demo Video:** https://youtu.be/PINyae-aLyc

---

## 1. Components & Hardware Used
* 1x Arduino Uno board
* 1x L298N dual H-bridge motor driver
* 1x HC-SR04 ultrasonic distance sensor
* 1x SG90 micro servo motor
* 2x Yellow BO geared DC motors with drive wheels
* 1x Front caster support wheel
* 2x Reclaimed phone batteries wired in pack with switch
* Custom cut cardboard chassis and upper deck
* Male-to-male and male-to-female jumper wires

---

## 2. Hardware Assembly & Time Breakdown (Total: ~8.5 Hours)

### Day 1: Chassis Cutting, Motor Alignment & Rolling Base (2.0 Hours)
* Measured and hand-cut cardboard panels to make the lower drive chassis and an upper enclosure to protect the circuitry.
* Glued and aligned both yellow BO gear motors underneath the frame. I made sure both axles were parallel to avoid mechanical pulling or veering while moving forward.
* Fitted both drive wheels and installed the front caster ball. Tested the rolling resistance manually across the table to ensure the wheels didn't scrape against the cardboard frame.

### Day 2: Ultrasonic Turret & Servo Mechanical Mount (1.5 Hours)
* Hot-glued the SG90 micro servo right on the front top deck of the car.
* Attached the HC-SR04 ultrasonic sensor module directly onto the servo horn to act as a dynamic radar head.
* Cut a clean opening in the cardboard deck right behind the servo to pass the 4 sensor wires through so they do not pinch or bind when the servo sweeps 0° to 180°.
* Calibrated the mechanical center horn by hand so 90° points dead straight ahead.

### Day 3: Electrical Wiring & Driver Integration (2.5 Hours)
* Following the system wiring schematic, made all interconnects between the Arduino Uno, L298N driver, and sensors:
  * **L298N Driver Logic:** Connected inputs IN1, IN2, IN3, and IN4 to Arduino digital pins 6, 7, 8, and 9. Connected left motor leads to OUT1/OUT2 and right motor leads to OUT3/OUT4.
  * **Power Rails:** Wired the phone battery pack positive terminal through an external switch into the L298N 12V terminal. Connected the negative battery lead to the L298N GND terminal.
  * **MCU Power & Common Ground:** Ran a ground jumper from the L298N GND port directly to the Arduino Uno GND pin to establish a shared reference. Ran a 5V power feed from the L298N 5V regulated output pin into the Arduino VIN port.
  * **Sensors:** Routed 5V and GND to the HC-SR04 ultrasonic sensor and SG90 servo. Connected sensor Trigger to digital pin 2, Echo to digital pin 4, and servo signal to digital pin 10.
* Organized and bundled jumper wires inside the cardboard cavity so moving parts wouldn't snag internal connections.

### Day 4: Bench Debugging, Power Issues & Physical Corrections (2.5 Hours)
* **Fixing Motor Direction Inversion:**
  * When I first ran the motion test, the car spun in circles because one motor was running forward while the other was running in reverse.
  * *Fix:* Rather than complicating the firmware direction states, I loosened the screw terminals on the left side of the L298N motor driver, flipped the two motor wires, and re-tightened them. Both motors moved forward together.
* **Resolving Brownout Reboots on Load:**
  * Whenever both motors switched suddenly from drive to turn, the Arduino would occasionally reset itself due to the instant surge current causing a minor voltage drop.
  * *Fix:* Re-seated all heavy power wires in the L298N screw blocks, shortened the main battery jumper leads, and re-made the common ground wire with a fresh, tight jumper to stop the voltage sag.
* **Eliminating False Obstacle Triggers:**
  * During the servo scan routine, the sensor occasionally reported 0 cm distance readings, making the car stop when no obstacle was present.
  * *Fix:* Discovered a slightly loose female dupont connector on the Echo pin. Replaced the jumper wire and secured the header firmly to the sensor pins.
* **Chassis Traction & Balance Adjustment:**
  * The rear wheels initially slipped on smooth floor tiles during sharp pivot turns because the battery weight was too far forward.
  * *Fix:* Repositioned the battery pack directly over the rear motor drive axle inside the chassis to provide sufficient tire traction.

---

## 3. Reviewer Summary
* **Hackatime Tracked Code Time:** 1.7 Hours
* **Hands-on Hardware, Wiring & Bench Debugging:** ~8.5 Hours
* **Total Project Effort:** ~10.2 Hours
*
