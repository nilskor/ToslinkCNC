# ToslinkCNC

CNC machine is usually controlled via parallel bus, containing six signals. For each of the three axes there are two signals: STEP and DIR. At each positive edge of the STEP signal, the corresponding stepper motor moves into direction set by DIR signal. In addition to these six signals, there can also be other general purpose control signals.

Parallel bus on longer distances and in noisy environment can be susceptible to electromagnetic interferences. Because of this we decided to design an interface to transport these parallel signals via an optical link. For successful transfer via optical fiber the first thing that must be done is to convert parallel data to serial bit stream. Moreover, because of the inherent design of optical transmitters and receivers, serial data must also be Manchester encoded.

Our design is based on [Serializer / Deserializer for Audio Fiber Optic](http://opencores.org/project,parallel_io_through_fiber) project published on Open Cores. We used Xilinx XC9572XL CPLD to implement the necessary logic for protocol conversion. A single CPLD can hold both the serializer for parallel to serial conversion and the deserializer for serial to parallel conversion.

We created universal PCB which can be used as a stand-alone stepper motor controller or as a shield attached to Arduino Uno. PCB consists of one CPLD, three optical transmitters, three optical receivers, headers for Arduino Uno and connectors for Pololu�s DRV8825 stepper motor driver carrier and for PoLabs� PoStep25-32 driver.