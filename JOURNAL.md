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
