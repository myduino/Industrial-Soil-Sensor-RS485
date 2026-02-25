```
   __  ___        __     _         
  /  |/  /_ _____/ /_ __(_)__  ___ 
 / /|_/ / // / _  / // / / _ \/ _ \
/_/  /_/\_, /\_,_/\_,_/_/_//_/\___/
       /___/                       
ai.iot.education.solutions.marketplace ==================================================

Ts. Mohamad Ariffin Zulkifli
ariffin@myduino.com
```

# Industrial Soil Sensor RS485
Industrial-Grade Soil Sensor: Measure multi-parameters of soil including Temperature, Moisture, pH, EC and Nitrogen, Phosphorus and Potassium (NPK). The output signal is RS485 and can be operated broad range of voltage from 5~30 VDC.

## Soil Sensors Specifications
- Operating Voltage: 5 ~ 30 VDC
- Communication Protocol: RS485
- Temperature
    - Measurement Range: -40°C ~ 80 °C
    - Measurement Accuracy: ±0.5 °C
- Moisture Content
    - Measurement Range: 0 ~ 100 %
    - Measurement Accuracy: ±3 %
- Electrical Conductivity (EC).
    - Measurement Range: 0 ~ 20000 uS/cm
    - Measurement Resolution: 1 uS/cm
- pH
    - Measurement Range: 3 ~ 9
    - Measurement Resolution: 0.1
- NPK
    - Measurement Range: 0 ~ 2999 mg/kg
    - Measurement Resolution: 1 mg/kg 

## RS485 Communication Details
- Data Bits: 8-bit
- Parity Bits: NO
- Stop Bit: 1
- Error Checking: CRC
- Baud Rate: 2400, 4800 (default), 9600
- Device Address: 0x01
- Function Code: 0x03
- Data Code: 16 bits

### Change Device Address
The default device address is **0x01**. Valid address range is **1 to 254**. The address is stored in register **0x07D0** and can be changed using write function code **0x10**.

- Example: Change device address from 0x01 to 0x02 (11 Bytes): `01 10 07 D0 00 01 02 00 02 42 C1`

| Address Code | Function Code | Register Address | Number of Registers | Byte Count | Data (New Address) | CRC       |
| ------------ | ------------- | ---------------- | ------------------- | ---------- | ------------------ | --------- |
| 0x01         | 0x10          | 0x07 0xD0        | 0x00 0x01           | 0x02       | 0x00 0x02          | 0x42 0xC1 |

> **Note:** Power cycle the sensor after changing the device address for the new address to take effect.

### Change Baud Rate
The baud rate is stored in register **0x07D1** and can be changed using write function code **0x10**.

- Baud Rate Values: **0x00** = 2400, **0x01** = 4800 (default), **0x02** = 9600

- Example commands from device address 0x02:

| Baud Rate | Command                            |
| --------- | ---------------------------------- |
| 2400      | `02 10 07 D1 00 01 02 00 00 D6 21` |
| 4800      | `02 10 07 D1 00 01 02 00 01 17 E1` |
| 9600      | `02 10 07 D1 00 01 02 00 02 57 E0` |

> **Note:** Power cycle the sensor after changing the baud rate for the new setting to take effect.

### 3-in-1 Soil Sensor Parameters
- Request Frame (8 Bytes)

| Address Code | Function Code | Start Address Register | Length of Register  | CRC        |
| ------------ | ------------- | ---------------------- | ------------------- | ---------- |
| 0x01         | 0x03          | 0x00 0x00              | 0x00 0x03           | 0x05 0xCB  |

> **Note:** The Address Code and CRC bytes will differ if the device address has been changed from the default (0x01).

- Example of Response Frame (11 Bytes)

| Address Code | Function Code | Byte Number | Moisture  | Temperature | EC        | CRC        |
| ------------ | ------------- | ----------- | --------- | ----------- | --------- | ---------- |
| 0x01         | 0x03          | 0x06        | 0x01 0xEF | 0x01 0x44   | 0x00 0x04 | 0xB5 0x59  |

- Byte Response Example Calculation
    - Moisture Content = (0x01 * 256 + 0xEF) * 0.1 = 49.5 %
    - Temperature = (0x01 * 256 + 0x44) * 0.1 = 32.4 °C
    - EC = (0x00 * 256 + 0x04) = 4 uS/cm

### 4-in-1 Soil Sensor Parameters
- Request Frame (8 Bytes)

| Address Code | Function Code | Start Address Register | Length of Register  | CRC        |
| ------------ | ------------- | ---------------------- | ------------------- | ---------- |
| 0x01         | 0x03          | 0x00 0x00              | 0x00 0x04           | 0x44 0x09  |

> **Note:** The Address Code and CRC bytes will differ if the device address has been changed from the default (0x01).

- Example of Response Frame (13 Bytes)

| Address Code | Function Code | Byte Number | Moisture  | Temperature | EC        | pH        | CRC        |
| ------------ | ------------- | ----------- | --------- | ----------- | --------- | --------- | ---------- |
| 0x01         | 0x03          | 0x08        | 0x02 0x62 | 0x01 0x67   | 0x00 0x06 | 0x00 0x37 | 0xC2 0x06       |

- Byte Response Example Calculation
    - Moisture Content = (0x02 * 256 + 0x62) * 0.1 = 61.0 %
    - Temperature = (0x01 * 256 + 0x67) * 0.1 = 35.9 °C
    - EC = (0x00 * 256 + 0x06) = 6 uS/cm
    - pH = (0x00 * 256 + 0x37) * 0.1 = 5.5

### 7-in-1 Soil Sensor Parameters
- Request Frame (8 Bytes)

| Address Code | Function Code | Start Address Register | Length of Register  | CRC        |
| ------------ | ------------- | ---------------------- | ------------------- | ---------- |
| 0x01         | 0x03          | 0x00 0x00              | 0x00 0x07           | 0x04 0x08  |

> **Note:** The Address Code and CRC bytes will differ if the device address has been changed from the default (0x01).

- Example of Response Frame (19 Bytes)

| Address Code | Function Code | Byte Number | Moisture  | Temperature | EC        | pH        | Nitrogen (N) | Phosphorus (P)  | Potassium (K) | CRC        |
| ------------ | ------------- | ----------- | --------- | ----------- | --------- | --------- | ------------ | --------------- | ------------- | ---------- |
| 0x01         | 0x03          | 0x0E        | 0x01 0xE6 | 0x01 0x55   | 0x05 0xDC | 0x01 0x34 | 0x00 0x20         | 0x00 0x25       | 0x00 0x30     | 0x04 0x08  |

- Byte Response Example Calculation
    - Moisture Content = (0x01 * 256 + 0xE6) * 0.1 = 48.6 %
    - Temperature = (0x01 * 256 + 0x55) * 0.1 = 34.1 °C
    - EC = (0x05 * 256 + 0xDC) = 1500 uS/cm
    - pH = (0x01 * 256 + 0x34) * 0.1 = 3.08
    - N = (0x00 * 256 + 0x20) = 32 mg/kg
    - P = (0x00 * 256 + 0x25) = 37 mg/kg
    - K = (0x00 * 256 + 0x30) = 48 mg/kg

## Contact Us
- Call or [WhatsApp 6012-3859151](https://wa.me/60123859151)
- Website: [Myduino](https://myduino.com)
