# Rfid-Interfacing

![Screenshot (787)](https://user-images.githubusercontent.com/118633170/209288759-a6117c57-8858-4664-ac8f-84bb00f0d23d.png)


If you have hard-time 3d printing stuff and other materials which i have provided in this project please refer the professionals for the help, [JLCPCB](https://jlcpcb.com/RNA) is one of the best company from shenzhen china they provide, PCB manufacturing, PCBA and 3D printing services to people in need, they provide good quality products in all sectors

[JLCPCB](https://jlcpcb.com/RNA)


Please use the following link to register an account in [JLCPCB](https://jlcpcb.com/RNA)

https://jlcpcb.com/RNA


Pcb Manufacturing

----------

2 layers

4 layers

6 layers

jlcpcb.com/RNA



PCBA Services

[JLCPCB](https://jlcpcb.com/RNA) have 350k+ Components In-stock. You don’t have to worry about parts sourcing, this helps you to save time and hassle, also keeps your costs down.

Moreover, you can pre-order parts and hold the inventory at [JLCPCB](https://jlcpcb.com/RNA), giving you peace-of-mind that you won't run into any last minute part shortages. jlcpcb.com/RNA


3d printing

-------------------

SLA -- MJF --SLM -- FDM -- & SLS. easy order and fast shipping makes [JLCPCB](https://jlcpcb.com/RNA) better companion among other manufactures try out [JLCPCB](https://jlcpcb.com/RNA) 3D Printing servies

[JLCPCB](https://jlcpcb.com/RNA) 3D Printing starts at $1 &Get $54 Coupons for new users


![Screenshot (821)](https://user-images.githubusercontent.com/118633170/209288783-50085524-0dda-47c2-b24f-49c825414fa9.png)


An RFID or radio frequency identification system consists of two main components, a tag attached to the object to be identified, and a reader that reads the tag.

A reader consists of a radio frequency module and an antenna that generates a high frequency electromagnetic field. Whereas the tag is usually a passive device (it does not have a battery). It consists of a microchip that stores and processes information, and an antenna for receiving and transmitting a signal.

Let’s take a look at the getID() custom function. First it checks whether there is a new tag placed near the reader and if so we will continue to the “for” loop which will get the UID of the tag. The tags that we are using have 4 byte UID number so that’s why we need to do 4 iterations with this loop, and using the concat() function we add the 4 bytes into a single String variable. We also set all characters of the string to upper cases and the end we stop the reading.

uint8_t getID() {
  // Getting ready for Reading PICCs
  if ( ! mfrc522.PICC_IsNewCardPresent()) { //If a new PICC placed to RFID reader continue
    return 0;
  }
  if ( ! mfrc522.PICC_ReadCardSerial()) {   //Since a PICC placed get Serial and continue
    return 0;
  }
  tagID = "";
  for ( uint8_t i = 0; i < 4; i++) {  // The MIFARE PICCs that we use have 4 byte UID
    readCard[i] = mfrc522.uid.uidByte[i];
    tagID.concat(String(mfrc522.uid.uidByte[i], HEX)); // Adds the 4 bytes in a single String variable
  }
  tagID.toUpperCase();
  mfrc522.PICC_HaltA(); // Stop reading
  return 1;
}
efore we enter the main loop, at the end of the setup section, we also call the printNormalModeMessage() custom function which prints the “Access Control” message on the display.

void printNormalModeMessage() {
  delay(1500);
  lcd.clear();
  lcd.print("-Access Control-");
  lcd.setCursor(0, 1);
  lcd.print(" Scan Your Tag!");
}

Now, before typing out the necessary code, you need to download the necessary library for this sensor from this repository.

Extract the contents from the zip folder "rfid-master" and add this library folder under the existing libraries of Arduino.

After doing so, restart your ArduinoIDE.

Now, our Arduino is ready to take commands and execute accordingly.

![Screenshot (804)](https://user-images.githubusercontent.com/118633170/209288847-72bec18c-0eb1-489c-bcd4-ddd81505ea20.png)

The Arduino Code has been uploaded at the end of this tutorial. Compile the code and eliminate "typo" errors (if any).

Now, its time to connect our Arduino with the RFID reader. Refer to the PIN wiring below,as well as the Connection schematic diagram for easy reference.

This is the information that you can read from the card, including the card UID that is highlighted in yellow. The information is stored in the memory that is divided into segments and blocks as you can see in the previous picture.

You have 1024 bytes of data storage divided into 16 sectors and each sector is protected by two different keys, A and B.

Write down your UID card because you’ll need it later.

Upload the Arduino code that has been suffixed here.

Demonstration

![Screenshot (819)](https://user-images.githubusercontent.com/118633170/209288873-257d1f54-9532-47a8-952d-691a6b8d2843.png)


Approximate the card you’ve chosen to give access and you’ll see:

The RFID reader consist of a radio frequency module, a control unit and an antenna coil which generates high frequency electromagnetic field. On the other hand, the tag is usually a passive component, which consist of just an antenna and an electronic microchip, so when it gets near the electromagnetic field of the transceiver, due to induction, a voltage is generated in its antenna coil and this voltage serves as power for the microchip.

Now as the tag is powered it can extract the transmitted message from the reader, and for sending message back to the reader, it uses a technique called load manipulation. Switching on and off a load at the antenna of the tag will affect the power consumption of the reader’s antenna which can be measured as voltage drop. This changes in the voltage will be captured as ones and zeros and that’s the way the data is transferred from the tag to the reader.

There’s also another way of data transfer between the reader and the tag, called backscattered coupling. In this case, the tag uses part of the received power for generating another electromagnetic field which will be picked up by the reader’s antenna.

Once we connect the module we need to download the MFRC522 library from GitHub. The library comes with several good examples from which we can learn how to use the module.

First we can upload the “DumpInfo” example and test whether our system works properly. Now if we run the Serial Monitor and bring the tag near the module, the reader will start reading the tag and all information from the tag will be displayed on the serial monitor.

The project has the following workflow: First we have to set a master tag and then the system goes into normal mode. If we scan an unknown tag the access will be denied, but if we scan the master we will enter a program mode from where we can add and authorize the unknown tag. So now if we scan the tag again the access will be granted so we can open the door.

Upload the code above and you should now see the RFID tag serial number on the serial monitor every time you tap the RFID tag.

And then I want to make a sample code if a serial tag with a certain number will make a buzzer blink three times and if the wrong tag is tapped it will trigger the long sound of the buzzer. This will simulate if we want to make for example RFID door lock or another project.

Add a 5V buzzer and connect the positive to pin 8 of Arduino and the ground pin to the ground of Arduino.

In this example, we will use a tag with the serial number “119 38 185 95” as the right tag. Or the key. You can edit this serial number in the code below.

The RC522 RFID module based on the MFRC522 IC from NXP is one of the cheapest RFID options you can get online for less than four dollars. It usually comes with an RFID card tag and a key fob tag with 1KB of memory. And the best part is that it can write a tag that means you can store any message in it.

![Screenshot (790)](https://user-images.githubusercontent.com/118633170/209288911-a8e08d9f-a15e-456c-b244-5dd158af5b02.png)


The RC522 RFID reader module is designed to create a 13.56MHz electromagnetic field and communicate with RFID tags (ISO 14443A standard tags).

The reader can communicate with a microcontroller over a 4-pin SPI with a maximum data rate of 10 Mbps. It also supports communication over I2C and UART protocols.

The RC522 RFID module can be programmed to generate an interrupt, allowing the module to alert us when a tag approaches it, instead of constantly asking the module “Is there a card nearby?”.

The module’s operating voltage ranges from 2.5 to 3.3V, but the good news is that the logic pins are 5-volt tolerant, so we can easily connect it to an Arduino or any 5V logic microcontroller without using a logic level converter.

![Screenshot (821)](https://user-images.githubusercontent.com/118633170/209288947-6fb09803-422c-4362-8fbc-61c244c98658.png)

