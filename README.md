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

## RS845 Communication Details
- Data Bits: 8-bit
- Parity Bits: NO
- Stop Bit: 1
- Error Checking: CRC
- Baud Rate: 2400, 4800 (default), 9600
- Device Address: 0x01
- Function Code: 0x03
- Data Code: 16 bits

### 3-in-1 Soil Sensor Parameters
- Request Frame (8 Bytes)

| Address Code | Function Code | Start Address Register | Length of Register  | CRC        |
| ------------ | ------------- | ---------------------- | ------------------- | ---------- |
| 0x01         | 0x03          | 0x00 0x00              | 0x00 0x03           | 0x05 0xCB  |

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

- Example of Response Frame (19 Bytes)

| Address Code | Function Code | Byte Number | Moisture  | Temperature | EC        | pH        | Nitrogen (N) | Phosphorus (P)  | Potassium (K) | CRC        |
| ------------ | ------------- | ----------- | --------- | ----------- | --------- | --------- | ------------ | --------------- | ------------- | ---------- |
| 0x01         | 0x03          | 0x0E        | 0x01 0xE6 | 0x01 0x55   | 0x05 0xDC | 0x01 0x34 | 0x00 0x20    | 0x00 0x25       | 0x00 0x30     | 0x04 0x08  |
- Byte Response Example Calculation
    - Moisture Content = (0x01 * 256 + 0xE6) * 0.1 = 48.6 %
    - Temperature = (0x01 * 256 + 0x55) * 0.1 = 34.1 °C
    - EC = (0x05 * 256 + 0xDC) = 1500 uS/cm
    - pH = (0x01 * 256 + 0x34) * 0.1 = 3.08
    - N = (0x00 * 256 + 0x20) = 32 mg/kg
    - P = (0x00 * 256 + 0x25) = 37 mg/kg
    - K = (0x00 * 256 + 0x30) = 48 mg/kg

## Contact Us
- Call or [WhatsApp 6013-2859151](https://wa.me/60132899151)
