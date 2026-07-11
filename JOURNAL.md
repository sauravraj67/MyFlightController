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
