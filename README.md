## Nordic Semiconductor nRF5 Smartwatches
Forked from micooke/arduino-nRF5-smartwatches --> Thank you, micooke and all the others who have contributed, for your help and development time on this project.

Please refer to micooke's README for more information.

I only have the ID107HR v2.4 to test with, but the button and capacitive button is dead, AFAIK.
If you have any additional PR that may work, I will review the PR's, but I prefer that you send the PR's to micooke/arduino-nRF5-smartwatches, as this is repo just a fork (a planned improvement on the KX022 code libs)

### Libraries
The following libraries (which work with this core) have been added as submodules:
1. U8g2_Arduino (OLED library) https://github.com/olikraus/U8g2_Arduino
2. sparkfun-based OLED library https://github.com/micooke/sparkfun_OLED
3. Software I2C https://github.com/micooke/SoftwareI2C
4. Software Serial https://github.com/micooke/SoftwareSerial - requirement: https://github.com/sandeepmistry/arduino-nRF5/pull/205
5. Accelerometer https://github.com/micooke/Kx022-1020
6. (work in progress) Si1143 Heartrate sensor https://github.com/micooke/Si1143

### Additions
I intend to add support for interrupts (Tap/Double Tap) for the KX022 sensor, but do not know the assigned pins yet. (Still need to find that out)

As well as BLE radio example code for testing purposes. 


#### I recommend using the u8g2 library over any of micooke's OLED libraries!

micooke's Squix78 based OLED [library](https://github.com/micooke/squix78_OLED) also works.

To get these libraries without using the board manager:
```
git clone https://github.com/RuhanSA079/arduino-nRF5-smartwatches.git
git submodule update --init --recursive
```

### Pin allocation

The nRF52 based T28 is quite different. Its pin allocation table is located [here](https://github.com/micooke/micooke.github.io/blob/master/nRF52832_Lemdoie_T28.md)


| peripheral type         | name   | pin          | IDO003 | ID100HR | ID107HR | ID107HR Plus
| :---:                   | :---:  | :---:        | :---:  | :---:   | :---:   | :---:
| accelerometer           | Kx022  | SCL          | 14     | 14      | 14      | 5 
|                         |        | SDA          | 16     | 16      | 16      | 3 
|                         |        | INT          | ---    | ---     | ---     | 6 
|                         |        | ADDR         | ---    | ---     | ---     | 4
|                         |        | NCS          | ---    | ---     | ---     | 7
| optical HR sensor       | Si1143 | SCL          | ---    | 26      | 22      | 18
|                         |        | SDA          | ---    | 28      | 23      | 10
|                         |        | INT          | ---    | ---     | 24      | 8
|                         |        | LED          | ---    | ---     | ---     | 9
| SPI flash memory        | MX25L  | MISO         | ---    | ---     | ---     | 27
|                         |        | MOSI         | ---    | ---     | ---     | 31
|                         |        | SCK          | ---    | ---     | ---     | 30
|                         |        | CE           | ---    | ---     | ---     | 28
| side tactile button     | ---    | BUTTON1      | 4      | 4       | 4       | ---
| capacitive touch button | RH6015C| BUTTON2      | 4      | 7       | 7       | ?
| capacitive touch screen | IQS263 | ---          | ---    | ---     | ---     | ?
| vibrate motor           | ---    | VIBRATE -or- | 7      | 8       | 6       | ?
|                         |        | LED_BUILTIN  |        |         |         |    
| serial UART             | ---    | Tx           | 18     | 18      | 18      | 23
|                         |        | Rx           | 17     | 17      | 17      | 24
| OLED                    | ---    | MISO         | 31     | 3       | 3       | ?
|                         | ---    | MOSI         | 29     | 2       | 2       | ?
|                         | ---    | SCK          | 30     | 1       | 1       | ?
|                         | ---    | RST          | 1      | 30      | 30      | ?
|                         | ---    | CS           | 2      | 29      | 29      | ?
|                         | ---    | DC           | 0      | 0       | 0       | ?
| battery voltage level   | ---    | ---          | ?      | ?       | \*      | ?

* --- : not applicable
*  ?  : unknown
* \*  : unknown (easily found - perform an analog read on each pin), but AIN{0:7} = p{28,27,1,2,3,4,9,10} so it must be one of p9,p10,p27,p28

### I2C addresses
1. 0x1F : Accelerometer (Kx022/Kx023)
2. 0x5A : Heart Rate Sensor / PPG (Si1143)
3. 0x76 : Altitude / Pressure / Temperature (HP203B)

### References
* micooke's original code (forked from)
* nRF5 core is written and maintained by Sandeep Mistry
* Support for these smartwatches originate from Roger's [arduino-nRF5-customised](https://github.com/rogerclarkmelbourne/arduino-nRF5-customised) repo
* [ID100HR picture](http://www.rogerclark.net/wp-content/uploads/2016/09/ID100HR_back_smart_watch-1024x576.jpg) is from Roger, embedded on his website [article](http://www.rogerclark.net/arduino-on-the-id100hr-fitness-tracker/)
* (Modified) [IDO003 picture](https://espruino.microco.sm/api/v1/files/ba591802419c40145d825db2924360eb162cc026.JPG) is from Gordon, embedded in this [conversation](http://forum.espruino.com/conversations/280747/)
* ID107HR picture is my own
* [ID107HR Plus picture](http://www.rogerclark.net/wp-content/uploads/2017/06/id107plus-7-770x1024.jpg) is from Curt, embedded on Roger's website [article](http://www.rogerclark.net/new-nrf52832-based-smart-watch-available/)
* (Modified) [ID107HR Plus pads](http://www.rogerclark.net/wp-content/uploads/2017/06/id107plus-3.jpg) is from Curt, embedded on Roger's website [article](http://www.rogerclark.net/new-nrf52832-based-smart-watch-available/)
