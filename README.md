Google MQTT Demo
================

This demo application connects to 
[Google Cloud IoT](https://cloud.google.com/solutions/iot/) 
through MQTT and publishes messages.

It requires a registered [device](https://www2.keil.com/iot/google) in the Google Cloud IoT.

The following describes the various components and the configuration settings.

Once the application is configured you can:
 - Build the application
 - Connect the debugger
 - Run the application and view messages in a debug printf or terminal window


Google IoT Client
-----------------
The file `demo.c` configures the connection to Google IoT with these settings:
 - PROJECT_ID:   Project ID
 - CLOUD_REGION: Cloud region
 - REGISTRY_ID:  Registry ID
 - DEVICE_ID:    Device ID

Note: These settings need to be configured by the user!

The file `pkey.h` configures the device private key.

Note: The device private key needs to be provided by the user!


FreeRTOS Real-Time Operating System
-----------------------------------
The [FreeRTOS RTOS](https://github.com/ARM-software/CMSIS-FreeRTOS) 
implements the resource management. It is configured with the following settings:

- Global Dynamic Memory size: 24000 bytes
- Default Thread Stack size: 3072 bytes


WiFi IoT Socket
---------------
This implementation uses an IoT socket layer that connects to a 
[CMSIS-Driver WiFi](https://arm-software.github.io/CMSIS_5/Driver/html/index.html).

The file `socket_startup.c` configures the WiFi connection with these settings:
 - SSID:          network identifier
 - PASSWORD:      network password
 - SECURITY_TYPE: network security

Note: These settings need to be configured by the user!


STMicroelectronics B-L475E-IOT01A Target Board
----------------------------------------------
The Board layer contains the following configured interface drivers:

**CMSIS-Driver USART1** routed to Virtual COM port (ST-LINK):
 - RX: ST-LINK-UART1_RX (PB7)
 - TX: ST-LINK-UART1_TX (PB6)

**CMSIS-Driver USART4** routed to Arduino UNO R3 connector (CN3):
 - RX: ARD.D0-UART4_RX (PA1)
 - TX: ARD.D1-UART4_TX (PA0)

**CMSIS-Driver SPI1** routed to Arduino UNO R3 connector (CN1):
 - SCK:  ARD.D13-SPI1_SCK (PA5)
 - MISO: ARD.D12-SPI1_MISO (PA6)
 - MOSI: ARD.D11-SPI1_MOSI (PA7)

**GPIO** pins routed to Arduino UNO R3 connector (CN1):
 - output: ARD.D10-SPI_SSN (PA2)
 - input:  ARD.D9-PWM (PA15)

**CMSIS-Driver WiFi0** routed to Inventek system ISM43362-M3G-L44 module:
 - SCK:  INTERNAL-SPI3_SCK (PC10)
 - MISO: INTERNAL-SPI3_MISO (PC11)
 - MOSI: INTERNAL-SPI3_MOSI (PC12)
 - GPIO: ISM43362-SPI3_CSN (PE0)
 - GPIO: ISM43362-WAKEUP (PB13)
 - GPIO: ISM43362-RST (PE8)
 - GPIO: ISM43362-DRDY_EXTI1 (PE1)

**CMSIS-Driver VIO** with the following board hardware mapping:
 - vioBUTTON0:        Button USER (PC13)
 - vioLED0:           LD2 GREEN (PB14)
 - vioMotionGyro:     ST MEMS gyroscope (LSM6DSL)
 - vioMotionAccelero: ST MEMS accelerometer (LSM6DSL)
 - vioAIN0:           ST MEMS humidity and temperature (HTS221)
 - vioAIN1:           ST MEMS barometer (LPS22HB)
 - vioAIN3:           ST MEMS humidity and temperature (HTS221)

**STDIO** routed to Virtual COM port (ST-LINK, baudrate = 115200)

The board configuration can be modified using 
[STM32CubeMX](https://www.keil.com/pack/doc/STM32Cube/html/index.html) 
and is stored in the file `STCubeGenerated.ioc`.
