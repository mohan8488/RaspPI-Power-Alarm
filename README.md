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
3. **UPS Hat** (from SunFounder)
4. **Waveshare 4G Hat** (based on SIM7600E-H)
5. **4G SIM Card**

---

## Getting Started
Follow these steps to set up the **RaspPI-Power-Alarm** system:

1. Assemble the hardware components:
   - Attach the UPS Hat to the Raspberry Pi.
   - Install the Waveshare 4G Hat on top of the UPS Hat.
   - Connect the cooling fan to the Raspberry Pi for better heat management.
2. Insert the 4G SIM card into the Waveshare 4G Hat.
3. Install the necessary software (instructions provided below).

---

## Software Installation
1. Install the Raspberry Pi OS on your Raspberry Pi.
2. Clone this repository:
   ```bash
   git clone https://github.com/your-username/RaspPI-Power-Alarm.git
   cd RaspPI-Power-Alarm
