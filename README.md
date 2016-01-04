# ToslinkCNC

CNC machine is usually controlled via parallel bus, containing six signals. For each of the three axes there are two signals: STEP and DIR. At each positive edge of the STEP signal, the corresponding stepper motor moves into direction set by DIR signal. In addition to these six signals, there can also be other general purpose control signals.

Parallel bus on longer distances and in noisy environment can be susceptible to electromagnetic interferences. Because of this we decided to design an interface to transport these parallel signals via an optical link. For successful transfer via optical fiber the first thing that must be done is to convert parallel data to serial bit stream. Moreover, because of the inherent design of optical transmitters and receivers, serial data must also be Manchester encoded.

Our design is based on [Serializer / Deserializer for Audio Fiber Optic](http://opencores.org/project,parallel_io_through_fiber) project published on Open Cores. 

We created universal PCB which can be used as a stand-alone stepper motor controller or as a shield attached to Arduino Uno. PCB consists of one CPLD, three optical transmitters, three optical receivers, headers for Arduino Uno and connectors for [Pololu’s DRV8825 stepper motor driver carrier](https://www.pololu.com/product/2133) and for [PoLabs’ PoStep25-32 driver](http://www.poscope.com/PoStep25-32). Shield enables cloning of one of the three axes. The axis to be cloned is set using jumpers Clone STP, Clone DIR and Clone LIMIT. DRV8825 microstepping is being set using jumpers MicroStepJP X, Y, Z and A. Motors are being powered through terminal block J1. Digital part of the circuit can be powered directly using onboard 5V linear regulator if the jumper JP EXT_V is set or through terminal block J2 or Arduino Uno if attached as a shield. Toslink transmitter DLT1111 and toslink receiver DLR1111 were used, which enable data transfer speed up to 16 Mbps. We used Xilinx XC9572XL CPLD to implement the necessary logic for protocol conversion. A single CPLD can hold both the serializer for parallel to serial conversion and the deserializer for serial to parallel conversion.

##Known Isues

 * Footprints for DLT1111 and DLR1111 are wrong - signal pins (VCC, GND, Vin/Vout) should be behind the mounting holes.
 * For PoStep connectors the IDC connectors should be used instead of dual row male headers. 
 * Error pin from PoStep connector should not supposed to be connected to the Limit signal. 
 * Additional headers and the corresponding pull-up resistors for limit switches should be added to the PCB. 
 * Because of huge voltage difference between 24V and 5V two LDOs or a switching regulator should be used instead of TLV1117-5V (the later handles only input voltages lower than 15V).
 
 
---

#### License

All our projects are as usefully open-source as possible.

Hardware including documentation is licensed under [CERN OHL v.1.2. license](http://www.ohwr.org/licenses/cern-ohl/v1.2)

Firmware and software originating from the project is licensed under [GNU GENERAL PUBLIC LICENSE v3](http://www.gnu.org/licenses/gpl-3.0.en.html).

Open data generated by our projects is licensed under [CC0](https://creativecommons.org/publicdomain/zero/1.0/legalcode).

All our websites and additional documentation are licensed under [Creative Commons Attribution-ShareAlike 4 .0 Unported License] (https://creativecommons.org/licenses/by-sa/4.0/legalcode).

What this means is that you can use hardware, firmware, software and documentation without paying a royalty and knowing that you'll be able to use your version forever. You are also free to make changes but if you share these changes then you have to do so on the same conditions that you enjoy.

Koruza, GoodEnoughCNC and IRNAS are all names and marks of Institut IRNAS Rače. 
You may use these names and terms only to attribute the appropriate entity as required by the Open Licences referred to above. You may not use them in any other way and in particular you may not use them to imply endorsement or authorization of any hardware that you design, make or sell.

