# RaspPI-Power-Alarm

A Raspberry Pi-based alarm system that sends text notifications in the event of commercial power failure.

---

## Features
- Detects power failures and sends notifications via SMS.
- Designed to work with off-the-shelf hardware components.

---

## Hardware Requirements
The following hardware components are required to build the system (all are available on Amazon):
1. **Raspberry Pi** (I used 4B)
2. **GeeekPi Cooling Fan**
3. **LED and 330Ω resistor**
4. **UPS Hat** (from SunFounder)
5. **Waveshare 4G Hat** (based on SIM7600E-H)
6. **4G SIM Card**
7. **3D Printed Case** (optional)

---

## Getting Started
Follow these steps to set up the **RaspPI-Power-Alarm** system:

1. Assemble the hardware components:
   - Attach the UPS Hat below the Raspberry Pi. Make sure to connect all the cables properly.
     
     ![Assembling UPS hat.](assets/Assembly-1.jpg)
   - Connect the cooling fan to the GPIO pins 1 & 9 (for 3.3V) or 4 & 6 (for 5V fan) as shown in the image.
     
     ![Connecting the fan.](assets/fan.jpg)
   - Connect a Power LED to RaspPi as shown [here](https://howchoo.com/pi/build-a-simple-raspberry-pi-led-power-status-indicator/). It is useful to have a power LED to know the status of the RaspPi while running.
2. Insert the prepaid 4G SIM card into the Waveshare 4G Hat.
3. Assemble the Waveshare 4G Hat on top of RaspPi as shown below.
   
   ![Assembling 4G hat.](assets/Assembly-2.jpg)
5. Install the necessary software (instructions provided below).
---

## Software Installation
1. Install the Raspberry Pi OS on your Raspberry Pi.
2. Clone this repository:
   ```bash
   git clone https://github.com/your-username/RaspPI-Power-Alarm.git
   cd RaspPI-Power-Alarm

---

## Edit the setup script:
- The script already contains information necessary to identify the battery status of the UPS as well as for the functioning of the 4G hat. Use any of the script editors to edit.
- Make sure to enter the phone numbers in the line:
```bash
# List of phone numbers
    recipient_numbers = ["<your_phone_number_1>", "<your_phone_number_2>"]
```

---

- To have custom messages depending on the power status of the device, edit the message in the power detection section:
```bash
# Power detection
        if GPIO.input(17):  # if port 17 == 1 (power is detected)
            if power_failure_start_time is not None:  # Power was previously off
                power_restored_time = datetime.now().strftime("%d-%m-%Y %H:%M:%S")
                duration_of_failure = datetime.now() - power_failure_start_time
                message = (f"Commercial power has been restored at {power_restored_time}.\n"
                            f"Power was OFF for {duration_of_failure}.\n"
                            f"Power failure started at {power_failure_start_time.strftime('%d-%m-%Y %H:%M:%S')}")
                send_sms(recipient_numbers, message)  # Replace with your phone numbers
                power_failure_start_time = None  # Reset after sending SMS
            elif init == 1:  # Cold boot or after power failure
                message = "Power is ON after reboot from extended power failure or device reset."
                send_sms(recipient_numbers, message)  # Replace with your phone numbers
                init = 0  # Set init to 0 after first SMS is sent
            while GPIO.input(17):  # Do nothing if power stays on
                time.sleep(0.1)  # Use time.sleep() here
        else:  # Power is off
            if power_failure_start_time is None:  # Power just went off
                power_failure_start_time = datetime.now()
                failure_time_str = power_failure_start_time.strftime("%d-%m-%Y %H:%M:%S")
                message = f"Commercial power supply in Somex Lab went OFF at: {failure_time_str}."
                send_sms(recipient_numbers, message)  # Replace with your phone numbers
            while GPIO.input(17) == 0:  # Do nothing while power is off
                time.sleep(0.1)  # Use time.sleep() here
```

- Next, run the script and you are done!
```bash
python3 powercheck.py
```

## Usage:
1. Power on the Raspberry Pi.
2. Monitor the system to ensure proper functioning.
3. In the event of a power failure, the system will send an SMS notification to the configured phone number.

---

## Contributions
Contributions are welcome! Please fork this repository and submit a pull request with your changes.

---

## License
This project is licensed under the CCZero License. See the LICENSE file for more details.



