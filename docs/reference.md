MicroPython class for EBYTE E32 Series LoRa modules which are based  on SEMTECH SX1276/SX1278 chipsets and are available for 170, 433, 470, 868 and 915MHz frequencies in 100mW and 1W transmitting power versions. They all use a simple UART interface to control the device.

## Pin layout E32-868T20D (SX1276 868MHz 100mW DIP Wireless Module)
```
 +---------------------------------------------+
 | 0 - M0  (set mode)        [*]               |
 | 0 - M1  (set mode)        [*]               |
 | 0 - RXD (TTL UART input)  [*]               |
 | 0 - TXD (TTL UART output) [*]               |
 | 0 - AUX (device status)   [*]               |
 | 0 - VCC (3.3-5.2V)                          +---+
 | 0 - GND (GND)                                SMA| Antenna
 +-------------------------------------------------+
```
**ALL COMMUNICATION PINS ARE 3.3V !!!**

## Transmission modes

- Transparent : all modules have the same address and channel and can send/receive messages to/from each other. No address and channel is included in the message.

- Fixed : all modules can have different addresses and channels. The transmission messages are prefixed with the destination address and channel information. If these differ from the settings of the transmitter, then the configuration of the module will be changed before the transmission. After the transmission is complete, the transmitter will revert to its prior configuration.

    1. Fixed P2P : The transmitted message has the address and channel information of the receiver. Only this module will receive the message. This is a point to point transmission between 2 modules.

    2. Fixed Broadcast : The transmitted message has address FFFF and a channel. All modules with any address and the same channel of the message will receive it.
             
    3. Fixed Monitor : The receiver has adress FFFF and a channel. It will receive messages from all modules with any address and the same channel as the receiver.

## Operating modes :
 
- 0=Normal (M0=0,M1=0) : UART and LoRa radio are on.

- 1=wake up (M0=1,M1=0) : Same as normal but preamble code is added to transmitted data to wake up the receiver.

- 2=power save (M0=0,M1=1) : UART is off, LoRa radio is on WOR(wake on radio) mode which means the device will turn on when there is data to be received. Transmission is not allowed.

- 3=sleep (M0=1,M1=1) : UART is on, LoRa radio is off. Is used to get/set module parameters or to reset the module.

## Reference for class ebyteE32

::: loraE32cp