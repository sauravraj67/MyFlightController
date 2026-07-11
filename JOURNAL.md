### Schematic<br>

## Making the Schematics for Flight Controller (Part-1)
Hours- 4 hr <br>

I started with the Schematics part . I added USB-C Symbol and added the necessary resistors (33R for data lines and 50K for CC )and I added the label to it . I made sure that the Data label are named as _D+/_D- for not having an issuer While routing differential pair.

<img width="530" height="526" alt="Screenshot 2026-07-05 113458" src="https://github.com/user-attachments/assets/b3a0514d-ac7e-4a08-a569-df2a73efd6d1" />

then I added a connector for Battery Connection (I will be using a 12V battery here) and a switch button to switch the Power connection between USB-C and the battery as per the need (USB-C for firmware update and Battery for flying).

<img width="665" height="132" alt="Screenshot 2026-07-05 113532" src="https://github.com/user-attachments/assets/40eda1a5-3f2d-4a1e-9d8c-51dba7f9099a" />


. We Receive voltages at 5V from USB-C line and 12 V from battery but the MCU that we will be using (STM32) needs voltage at a constant 3.3V . So I need to add a 3.3V Voltage regulator so for that I choose AP63203WU as it fit's our needs the best then for extra Security / precaution (because power form it will go to the IMU and main sensors) , I added a reverse polarity filter using (AO3401A ) and added Pi-Filter then I added the respective capacitors as required by the circuit and added a fusion and an LED for detection and at the end added the respective labels. So this is how it looks

<img width="1303" height="276" alt="Screenshot 2026-07-05 113521" src="https://github.com/user-attachments/assets/cd7953d2-c92b-4336-9ac0-734ad53e9a22" />

then I need to add a 5v Buck converter for powering the servos , receiver and the ESC's . So for that I choose (L7805). It has a very basic circuit SO I made it and added the respective capacitors of the needed values and added the label .
<img width="1025" height="342" alt="Screenshot 2026-07-05 120840" src="https://github.com/user-attachments/assets/3f885e95-8392-433a-9e24-4af18793969e" />

I didn't added any external filter over here because it wasn't much necessary.(As it is just for output devices like ESC's and servos) then It was the time to add an IMU . SO for the first IMU I went with (MPU-6050). as It is widely available and easy to integrate . It needed 3.3V logic so I didn't need to make any extra regulators for it and it will communicate through I2C to the IMU. So I made the respective circuit and added the label to the respective places and this is how it looks

<img width="582" height="647" alt="Screenshot 2026-07-05 122034" src="https://github.com/user-attachments/assets/b09c07b8-767c-4cbe-82c9-a14c417abd44" />

## Making the Schematics for Flight Controller (Part-2)

Hours :- 6.25 hr 

Now I started with adding the Barometer (BMP280). It will help us to determine/hover at an altitude. It too works on 3.3V and will use I2C communication to IMU. SO I added it to the schematics and had a view to the datasheet and made it's circuit with the respected capacitors. then I added the labels and this is how it looks

<img width="382" height="503" alt="Screenshot 2026-07-05 122535" src="https://github.com/user-attachments/assets/b219ea59-7db6-4cc4-adbd-5c8a55636e49" />

. Then it was time to add the second IMU . after some consideration I choose (ICM-20948) for the Job. It too communicates via I2C but one difference was that it worked on 1.8 V . So firstly I had to make a 1.8 V voltage regulator . For that I went with (LD39015M18R) then I made it's circuit and added the labels

<img width="807" height="287" alt="Screenshot 2026-07-05 122913" src="https://github.com/user-attachments/assets/7476d0e9-65bd-4df2-82b9-6877f11b75ff" />

. I didn't used ant external filters like pi/reverse polarity because the connect source for it is 3.3V and it has all of these things from before. After that I moved to make the circuit schematics for the ICM-20948 . I added the labels and this is how it looks

<img width="501" height="576" alt="Screenshot 2026-07-05 122641" src="https://github.com/user-attachments/assets/9d35c26d-1ffa-4ca9-839c-1d8cc2c88c15" />
Then I added two ESC's Connectors to control the brush less motor's. (One on each wing). Each ESC's has 2 set of connection . 3 pin connector (data,power,gnd) this goes onto connecting esc to IMU so that it could read at which speed should it make the motor rotate. and 2 pain (12V, GND) It is basically to power the Brushless Motor. So I added it with the labels and this is how it looks like

<img width="678" height="450" alt="Screenshot 2026-07-05 125356" src="https://github.com/user-attachments/assets/3808ddae-fb07-4d7d-ad69-b51643d7eff1" />
. After that I added 2 Servos connection (one for each wing). So that control the flap angle on each wing (To make the plane hover correctly). It has a single 3 pin connector (Data,Power,Gnd). SO i added them and placed the respective labels After this I went with added connector for the radio receiver. It has 4 Pin (RX,TX,Power,Gnd). RX and TX are for communication to IMU. So I added the connectors for it
<img width="347" height="345" alt="Screenshot 2026-07-05 125500" src="https://github.com/user-attachments/assets/4b1d4a23-2613-4062-8595-981419ce63d9" />
<img width="283" height="210" alt="Screenshot 2026-07-05 125505" src="https://github.com/user-attachments/assets/3855cbc6-ccf8-4005-a5a6-b89bc3d0fcd5" />

 So Now Most of the things were done . Only STM32 connectors are left now So I began with it. First I needed to choose a STM32 Version . For that I went with STM32F401CBUx because it has enough Gpio and can handle the Flight computation . Also a good thing is that I don't need to add any extrenal flash to it becuase it comes with inbuild 128 KB of Flash memory and 64 KB of SRAM . At first I added the boot button and a 24 MHz Crysal oscillator with it's circuit to the MCU .
 <img width="701" height="478" alt="Screenshot 2026-07-05 130209" src="https://github.com/user-attachments/assets/7d985af2-bedc-423b-9783-35a29eec2f7e" />

then I added 6 100pf Decoupling capacitors to the MCU . (2 near each sensors) and attached it to MCU<img width="905" height="480" alt="Screenshot 2026-07-05 130800" src="https://github.com/user-attachments/assets/0572c76c-db3c-4837-943e-d40aa81e8c7f" />

and then at the END I attached all the labels to the MCU (Data, 3 pair of I2C from sensors , 2 pair of ESC's and servos and the 2 connection form the receiver , and rest power Gnd oscillator things ). I made sure that I connected each connection at the right place as er the pin layout  and this is the final look of the schematics <img width="1187" height="657" alt="Screenshot 2026-07-05 131710 (1)" src="https://github.com/user-attachments/assets/8ef4dd77-58cd-4e4f-90d3-fc03179b79e2" />


###  PCB Design<br><br>

## Started with PCB ( Component placement)
hours :- 5.2 hr
So I started with designing the PCB Layout . First I updated the PCB with the schematics and this is how it looked
<img width="547" height="527" alt="Screenshot 2026-07-05 155133" src="https://github.com/user-attachments/assets/384e661f-9ba2-45b4-8c3b-07e4ae0c8444" />

then I started with arranging the main components in a rough manner (MCU , Sensor , USB ,Voltage regulators), then I started arranging the other small components (Like Resistors and capacitors) near to there connection I a proper manner So there would be easy while routing. after I completed that I Started placing all the small circuit clusters onto the board In a standard manner . I wanted the board to hold a rectangular dimension. So I made sure to maintain that shape while placing the components also made sure that there is enough space for routing and components are placed specifically that there rout are clean and short. at the end I placed all the connectors pins for the ESC , receiver and servos. I went for few alteration but ended up with this

<img width="668" height="428" alt="Screenshot 2026-07-05 155422" src="https://github.com/user-attachments/assets/f431c22e-a541-403f-ae12-5520524cc532" />

.after that I added the Holes for connection and them made added the boundary and this is the final look of it then at the end added the text logo and connection guiled for each of the connection.

<img width="732" height="503" alt="Screenshot 2026-07-05 154857" src="https://github.com/user-attachments/assets/2ebbd9af-9869-40cc-a84f-d368dd763c06" />

<img width="1457" height="780" alt="Screenshot 2026-07-05 154851" src="https://github.com/user-attachments/assets/c432514b-5410-49de-919a-8d7630c03d82" />

 ### Routing the PCB (Part-1)
Hours :- 4.1 hr 

So I started with routing the PCB firstly I routed the USB-C and the differential pair for data.

<img width="1446" height="262" alt="Screenshot 2026-07-05 160340" src="https://github.com/user-attachments/assets/d95e29c3-9641-429e-8e08-0e9c46999471" />

then I made connection for the power system

<img width="1446" height="262" alt="Screenshot 2026-07-05 160340" src="https://github.com/user-attachments/assets/28a5d873-7a39-4961-94d6-5c4224d2a5ce" />
after that I started routing the Sensors circuit

<img width="1056" height="632" alt="Screenshot 2026-07-05 161552" src="https://github.com/user-attachments/assets/d5faa8df-b280-4df3-a4cb-dd9a9ca39666" />
after that I made more circuit connections
<img width="1056" height="632" alt="Screenshot 2026-07-05 161552" src="https://github.com/user-attachments/assets/c4ecaf89-5b8f-460b-bf66-f0914cfd6549" />
and then I started joining the SDA and SCL AD connections from Sensores to the MCU. Where wthere wasn't a way to rout I used vias to keep the circuit clean
<img width="297" height="637" alt="Screenshot 2026-07-05 162242" src="https://github.com/user-attachments/assets/7204795b-0b5a-4d7a-aff8-1480a3473413" />
<img width="180" height="305" alt="Screenshot 2026-07-05 162048" src="https://github.com/user-attachments/assets/b247ee7d-793b-488f-8b2b-56ec83a00fa7" />


after all this there were still many connection that I left like the boot pin and the servos So I routed it

<img width="762" height="636" alt="Screenshot 2026-07-05 163229" src="https://github.com/user-attachments/assets/4a5e8e92-7ebe-4481-90eb-c9a5cc6ea834" />

. Many a Places 5V connection was missing to I used vias and routed it . I used Thick Routs for the 12V and 5V connections. again I saw the board and receivers data connections rout were missing anf this is how the PCB looks now 

<img width="672" height="452" alt="Screenshot 2026-07-05 163627" src="https://github.com/user-attachments/assets/0eb974d0-750a-4d08-b062-66392e1f6971" />


SO I started routing it I had a bit of issues as the routs were very close and I wasn't able to make a rout
SO I made few changes in the rout , It took me a bit of time but I was able to rout it through .
<img width="897" height="670" alt="Screenshot 2026-07-05 164201" src="https://github.com/user-attachments/assets/e45bd441-b997-4996-ac16-d6ff2d4746de" />

Some places Power connection were missing SO I needed to rout it


<img width="497" height="612" alt="Screenshot 2026-07-05 164552" src="https://github.com/user-attachments/assets/3938d0e2-bf84-472e-9af9-0cb7fe4fe379" />
I left the GND Connection and 3.3V Connection in major places because I will be using Fillzone of them on top and bottom Layer. So there were some more visual connections left SO I tried to join them all and this is how the PCB Looks now 




<img width="722" height="448" alt="Screenshot 2026-07-05 164735" src="https://github.com/user-attachments/assets/c8c243ac-3dd1-4ddc-b731-a0a3d353e6a3" />
I added  the fill zones (Top layer is 3.3V and bottom layer is GND ) PCB Look after fillzone 

 ### Routing the PCB (Polishing The Rout / Fixing the errors and Disconnection )
Hours :- 3.75 hr 

So there were many not perfect routs on the board

<img width="855" height="117" alt="Screenshot 2026-07-05 171402 (1)" src="https://github.com/user-attachments/assets/bd6c8417-fb7b-4333-bb97-78121831ea4e" />

and the board had many disconnections as well
<img width="601" height="503" alt="Screenshot 2026-07-05 171416" src="https://github.com/user-attachments/assets/6c542174-e291-4fdc-a17b-9685de49b295" />

. So I started solving them one by one . I will start with fixing the connections then I will move to Check things by rule checker and at the end I will polish all the routs . So I Saw multiple disconnection On the PCB and started Solving them one by one . I tried to keep the rout as simple as possible these are few of the 3.3V and GND connections that I solved


<img width="963" height="472" alt="Screenshot 2026-07-05 171922" src="https://github.com/user-attachments/assets/3bc407e2-49e0-4e2a-87e8-b31fb697cd93" />
<img width="643" height="751" alt="Screenshot 2026-07-05 172715" src="https://github.com/user-attachments/assets/f3127f55-b601-49b2-a2ba-7b24f668dbba" />


<img width="680" height="448" alt="Screenshot 2026-07-05 164933" src="https://github.com/user-attachments/assets/235beed2-97cf-4154-a6af-db0151f354fa" />
<img width="697" height="443" alt="Screenshot 2026-07-05 165213" src="https://github.com/user-attachments/assets/d91ec826-cfbf-4137-afad-69d495e719c3" />
