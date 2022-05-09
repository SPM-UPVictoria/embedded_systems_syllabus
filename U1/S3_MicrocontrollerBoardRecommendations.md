## Microcontroller board recommendations

To make your life a little bit easier while choosing a microcontroller board for your next project, I would like to introduce you to a few well-known ones, which are widely used and have different areas in which they shine.

## Particle Argon/Boron/Xenon

Particle is one of the major players in the IoT development space. Their first development board, called Core, offered an affordable way to prototype connected devices without needing to buy a Wi-Fi shield. Their second generation board, the Photon, brought prices down even more. Since November, 2018, their third generation of IoT development boards have been available and makes the Thread protocol available in a development board for the first time. Thread, which we discussed in an earlier section, is a protocol for mesh networking. So, having multiple devices that need to communicate with one another and rely solely on the availability of Wi-Fi is not an option; adding mesh to the mix might be the solution. It is also a great option if you have various devices that need to communicate with one another entirely without an internet connection. 

Particle boards can be programmed in two ways—either via the cloud editor on the company's website or via Particle Dev (https://www.particle.io/developer-tools/), a desktop IDE. It is not as convenient as the Arduino IDE, because you might run into little issues here and there, but overall it offers a good user experience. The library support for external modules, such as sensors and actuators, is not as good as with Arduino, but most are supported.

A great feature baked into all Particle boards is OTA updates. You don't need to connect the Particle development board to your computer if you want to flash new firmware; it just needs to be online somewhere. This means that the device could be in a different room, city, or country. As long as it is connected to the internet, you can upload new firmware. It's pretty handy! But it also has a (little) downside—when flashing new code, it takes longer than if you just flash your Arduino via a USB serial connection. It's not crazy long, but longer.

## NodeMCU

NodeMCU is definitely the cheapest development board introduced here that can be connected to the internet. On AliExpress, one of the biggest Chinese shopping platforms, you can get a NodeMCU for just a few dollars.

Based on the ESP8266, it runs on 3.3V and offers many ports and supports protocols such as SPI or I2C. In contrast to the boards from Arduino or Particle, it only supports one analog input, though. If you plan on reading multiple analog sensors (for example, light and pressure sensors) at the same time, you should either get another board or you have to add an analog-to-digital converter (ADC) to your setup.

## Raspberry Pi 4 Model B+

In contrast to the aforementioned development boards, which use a microcontroller, Raspberry Pi is a full-blown, single-board computer with separate memory, GPU (graphics card), and multi-core CPU in a very small form factor. It typically runs a Linux operating system, often Raspbian, a special version of Linux made for the Raspberry Pi. It was the first popular single-board computer combining both worlds—microcontroller boards with GPIO pins and a full operating system with support for USB devices such as hard drives, webcams, keyboards, or mice. It also ships with an Ethernet network port to create a stable network connection, an SD-card slot, and an audio jack connector, as well as an HDMI port to connect a screen to. It really is a tiny computer.

By now, there are a multitude of system on a chip (SOC) computers, but the Raspberry Pi remains the most important for IoT prototyping, because it has a huge community, so you will find a lot of hardware add-ons (called shields) and tutorials. You can see the predecessor to the Raspberry Pi 4 Model B, the Raspberry Pi 3 Model B+.

In early 2019, some alternatives appeared that offer features that are similar to those on a Raspberry Pi board: 

  * **Coral Dev board**: The Coral Dev board (https://coral.withgoogle.com/products/dev-board) is a development board by Google designed especially for machine learning projects. It features a powerful Edge TPU coprocessor, which greatly accelerates machine learning tasks.
  * **Jetson nano development kit**: The Jetson nano development kit (https://developer.nvidia.com/embedded/buy/jetson-nano-devkit) is a development board from the graphics card manufacturer Nvidia. Similar to the Coral Dev Board, it is intended for machine learning prototyping.

  ## Arduino MKR WiFi 1010

  The Arduino MKR WiFi 1010 is the successor to the Arduino MKR 1000 WiFi, which combined the functionality of the Arduino Zero with a Wi-Fi shield, and therefore lowered the entry barrier to creating internet-connected projects. Being an official Arduino product, getting started with it is really easy. You have to install the board, load the example sketch, and enter your router username and password, and your device is online. If you have ever worked with an Arduino Wi-Fi shield before, you probably do not have the best of memories as there were many things that could go wrong, leading to hours of debugging work. With the MKR series, this all became easier. The MKR 1000 also includes a battery socket, which makes building battery-powered projects even easier.

  The same is true for the Arduino MKR WiFi 1010. It is really easy to set up, has great library support, and brings some extra features. Using the newly added ESP32 chip, the MKR board is now also able to communicate via Bluetooth LE. Charging the battery on the MKR 1010 is done by connecting it to a power source via USB; it will automatically detect this and start charging the battery.

