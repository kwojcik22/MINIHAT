# MINIHAT

|  # | Interfejs              | Opis                                   |   HW  |   FW  |   MCU periph  |
| -: | ---------------------- | -------------------------------------- | :---: | :---: | :-----------: |
|  1 | CAN                    | Odbiór / (nadawanie) ramek CAN         | **K** | **V** |   FW          |
|  2 | Ethernet (LAN8720)     | Podłączenie do komputera               | **V** | **V** |   FW          |
|  3 | USB                    | Podłączenie do komputera               | **V** | **K** |   FW          |
|  4 | MIPI                   | Wyświetlanie informacji podstawowych   | **K** | **K** |   DSI HOST    |
|  5 | Bluetooth (bez anteny) | Podłączenie do telefonu, odbiór muzyki | **K** | **K** |   USART2      |
|  6 | Wyjście audio          | Wyjście na głośniki                    | **V** | **K** |   FW          |
|  7 | DEBUG                  |                                        | **K** | **K** |   USART1      |
|  8 | Zasilanie płytki       | _proponowany_ akumulator ładowany z usb| -     | -     |               |



# MCU
SMT32: 	H747IGTX

can 120ohm
usb 90ohm
ethernet ma 50ohm

![alt text](schemat_ideowy.drawio.svg)

# SRC
- [RM0399 Reference manual STM32H745/755 and STM32H747/757](https://www.st.com/resource/en/reference_manual/rm0399-stm32h745755-and-stm32h747757-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)
- [Introduction to LCD-TFT display controller (LTDC) for STM32 MCUs](https://www.st.com/resource/en/application_note/an4861-introduction-to-lcdtft-display-controller-ltdc-on-stm32-mcus-stmicroelectronics.pdf)
- [DS STM32H747x](https://www.st.com/resource/en/datasheet/stm32h747ig.pdf)

## COMPONENTS SEARCH
- [display round](https://eu.mouser.com/ProductDetail/Newhaven-Display/NHD-2.1-480480AF-ASXP?qs=%252BXxaIXUDbq0eZ2IOf2mxVQ%3D%3D)
- [ST antena design for STM32WB 2.4GHz ](https://www.st.com/resource/en/application_note/an5129-low-cost-pcb-antenna-for-24ghz-radio-meander-design-for-stm32wb-series-stmicroelectronics.pdf)
- [BT chip](https://www.mouser.pl/ProductDetail/STMicroelectronics/BLUENRG-234N?qs=yqaQSyyJnNj1fpgr7V7RSw%3D%3D&mgh=1&vip=1)
- 