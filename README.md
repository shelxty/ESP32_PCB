# ESP32-C3 USB-C Devboard 

This is a custom 4-layer ESP32-C3 devboard built from scratch in KiCad, built around the ESP32-C3-WROOM-02. It's my second devboard (if a regulator can be counted as a devboard) with a full breakout of GPIOs and reset/boot buttons.

## Motivation 
This is my second-ever PCB; I built it to follow up on my first project. I've been interested in how ESP32s work so I thought this would be the best way to explore it! This would be an actual useful, purposeful tool that I'd be able to use in built projects as well. It also pushed me to learn new skills, like ESD protection and multi-layer board design (well, multi-layer as in 4 instead of 2). 

## How the Components Work 

| **Designator** | **Part** | **Purpose** | 
|----------------|----------|-------------|
| U3 | ESP32-C3-WROOM-02 | The brain of the board basically (it's a RISC-V microcontroller module that has integrated WiFi & bluetooth, along with an antenna) | 
| J1 | 16-pin USB-C receptacle | Power entry (it takes in 5V) | 
| J2, J3 | 8-pin headers on the left & right side, respectively | Breaks out the GPIO pins | 
| U1 | USBLC6-2SC6 | Dual line ESD protection IC that suppresses voltage spikes before they reach the microcontroller | 
| D1 | PESD5V0L1ULD | A TVS diode that protects the voltage line (5V) from any ESD/transient voltage spikes that enter from the USB receptacle | 
| R3 | 0Ω resistor | Basically a routing jumper so that I don't have to remove a trace | 
| U2 | AP2112K-3.3 | Fixed 3.3V, 600mA LDO regulator (it basically takes the 5V input and regulates it into a stable 3.3V rail) | 
| C1, C2 | 4.7uF capacitors | These are input and output capacitors built around the regulator that smooths the 5V input and the regulated 3.3V output | 
| C3, C4, C5 | 4.7uF capacitors | Other decoupline capacitors except these around the module's power pins, so the supply is stable even during WiFi bursts | 
| C9, C10 | 100nF capacitors | These are high-frequency decoupling capacitors that are placed close to the regulator's pins (they filter out noise) | 
| R5 | 10kΩ resistor | This is a pull-up resistor that supports the enable (EN) line | 
| R7, R8 | 10kΩ resistor | These are two other pull-up resistors except they support different GPIO lines | 
| R1, R2 | 5.1kΩ resistor | Resistors on the RESET and BOOT button lines, respectively | 
| SW1 | "RESET" Push Button | Basically just... resets the chip... yeah. | 
| SW2 | "BOOT" Push Button | Pulls IO9 (the strapping pin that selects boot mode, as opposed to UART download mode) low when it's pressed | 
| R9 | 10kΩ resistor | This one is another pull-up resistor but it specifically works on the IO9 boot/strapping line (so the chip should boot normally if the BOOT button isn't being pressed | 
| Y1 | Crystal | An external crystal that provides a precise clock reference | 


**Hardware**
- Tool: KiCad 10
- Board: 4-layer PCB (F.Cu / In1.Cu / In2.Cu / B.Cu)
- Microcontroller: ESP32-C3-WROOM-02 RISC-V, WiFi + Bluetooth
- Regulator: AP2112K-3.3, 600mA LDO
- USB protection: USBLC6-2SC6 (data line ESD) + PESD5V0L1ULD (VBUS TVS diode)
- Power input: USB-C (5V)
- GPIOs: 16 pins broken out across two 8-pin 2.54mm headers (J2, J3)
- Controls: Reset button (SW1), Boot button (SW2)

## PCB Design 
<img width="1498" height="853" alt="image" src="https://github.com/user-attachments/assets/514717f6-bff0-470a-ad63-4f9fabcfe0cb" />

_Schematic of the board -- I made sure to add comments & my own personal text for beginners like me_

<img width="545" height="796" alt="image" src="https://github.com/user-attachments/assets/747161ee-0904-4692-93ec-34f81beccd7b" />

_PCB design_


<img width="1082" height="690" alt="image" src="https://github.com/user-attachments/assets/a5166ac8-f290-44b5-a05f-a8a495e2bc12" />

_A 3D view of the actual thing_



## Bill of Materials 
| **Item** |	**Description** |	**Reference** |	**Qty** |	**MOQ** |	**Value** |	**Per Unit Price ($)** |	**Total Price ($)** |	**Footprint** |	**MPN** |	**URL** | 
|------|--------------|-----------|-----|-----|-------|--------------------|------------------|-----------|-----|-----|
| 4u7 Capacitor |	Unpolarized capacitor |	C1,C2,C3,C4,C5 |	5 |	10 |	4u7 |	0.0505 |	0.51 |	Capacitor_SMD:C_0805_2012Metric |	CL21A475KBQNNNE |	[Link](https://www.lcsc.com/product-detail/C98192.html?s_z=s_c_Ceramic%2520Capacitors&spm=wm.fly.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFeXl1XRlNeXzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktTRk8GEwkK) |
| 100n Capacitor |	Unpolarized capacitor |	C6,C9,C10 |	3 |	10 |	100n |	0.0192 |	0.19 |	Capacitor_SMD:C_0201_0603Metric |	0805B104K500CT |	[Link](https://www.lcsc.com/product-detail/C83055.html?s_z=s_c_Ceramic%2520Capacitors&spm=wm.fly.bg.3.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFeXl1XRlNeXzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktTRk8GEwkK) |
| Capacitor |	Unpolarized capacitor |	C7,C8,R4 |	3 |	100 |	0n |	0.0052 |	0.52 |	Capacitor_SMD:C_0201_0603Metric |	TCC0805X7R501K500DT |	[Link](https://www.lcsc.com/product-detail/C5375938.html?spm=wm.fly.bg.3.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1ZVTlNXVzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktXRlVcSQwSGg0%3D) |
| ESD Diode |	Low capacitance unidirectional ESD protection diode, 5V, SOD-882D |	D1 |	1 |	5 |	PESD5V0L1ULD |	0.0978 |	0.49 |	Diode_SMD:D_SOD-882D |	PESD5V0L1ULD,315 |	[Link](https://www.lcsc.com/product-detail/C552557.html?s_z=s_p_PESD5V0L1ULD%252C315&spm=wm.fly.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1dXRVBfUDsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D) | 
| USB-C Receptacle |	USB 2.0-only 16P Type-C Receptacle connector |	J1 |	1 |	5 |	USB_C_Receptacle_USB2.0_16P |	0.099 |	0.5 |	Connector_USB:USB_C_Receptacle_G-Switch_GT-USB-7010ASV |	USB-TYPE-C-016 |	[Link](https://www.lcsc.com/product-detail/C2927036.html?s_z=s_p_USB-TYPE-C-016&spm=wm.fly.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1BWRlFcVTsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D) |
| 1x08 Connector |	Generic connector, single row, 01x08 |	J2,J3 |	2 |	5 |	Conn_01x08_Pin |	0.558 |	2.79 |	Connector_PinHeader_2.54mm:PinHeader_1x08_P2.54mm_Vertical |	N/A |	[Link](https://www.aliexpress.us/item/3256807202794047.html?spm=a2g0o.detail.pcDetailTopMoreOtherSeller.3.5ee0z10vz10vCf&gps-id=pcDetailTopMoreOtherSeller&scm=1007.40050.354490.0&scm_id=1007.40050.354490.0&scm-url=1007.40050.354490.0&pvid=f02ca764-02d9-42b0-aa3a-38bc3d3eef3d&_t=gps-id%3ApcDetailTopMoreOtherSeller%2Cscm-url%3A1007.40050.354490.0%2Cpvid%3Af02ca764-02d9-42b0-aa3a-38bc3d3eef3d%2Ctpp_buckets%3A668%232846%238111%231996&pdp_ext_f=%7B%22order%22%3A%2215779%22%2C%22eval%22%3A%221%22%2C%22sceneId%22%3A%2230050%22%2C%22fromPage%22%3A%22recommend%22%7D&pdp_npi=6%40dis%21USD%211.66%211.64%21%21%211.66%211.64%21%402103128917820104935402726e66ac%2112000040551940967%21rec%21US%217756416958%21X%211%210%21n_tag%3A-29911%3Bd%3A882c3b75%3Bm03_new_user%3A-29895&utparam-url=scene%3ApcDetailTopMoreOtherSeller%7Cquery_from%3A%7Cx_object_id%3A1005007389108799%7C_p_origin_prod%3A) | 
| Resistor |	Resistor |	R1,R2 |	2 |	100 |	5k1 |	0.0022 |	0.22 |	Resistor_SMD:R_0805_2012Metric |	FRC0805J512TS |	[Link](https://www.lcsc.com/product-detail/C2930296.html?s_z=s_q_t_RESISTOR&spm=wm.fly.bg.1.xh___wm.ssy.tc.0.tz&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1JWT1RdVDsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktRR1NADxALGw%3D%3D) |
| Resistor |	Resistor |	R3 |	1 |	100 |	0R |	0.003 |	0.3 |	Resistor_SMD:R_0805_2012Metric |	0805W8F0000T5E |	[Link](https://www.lcsc.com/product-detail/C17477.html?s_z=s_q_t_RESISTOR&spm=wm.fly.bg.0.xh___wm.ssy.tc.0.tz&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1JWT1RdVDsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktRR1NADxALGw%3D%3D) |
| Resistor |	Resistor |	R5,R7,R8,R9 |	4 |	100 |	10k |	0.0031 |	0.31 |	Capacitor_SMD:C_0201_0603Metric |	FRC0805J103TS |	[Link](https://www.lcsc.com/product-detail/C2930231.html?s_z=s_q_t_RESISTOR&spm=wm.fly.bg.1.xh___wm.ssy.tc.0.tz&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1JWT1RdVDsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktRR1NADxALGw%3D%3D) | 
| Resistor |	Resistor |	R4, R6 |	2 |	100 |	100R |	0.0031 |	0.31 |	Capacitor_SMD:C_0201_0603Metric |	FRC0805J101 TS |	[Link](https://www.lcsc.com/product-detail/C2907294.html?spm=wm.fly.bg.1.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1xeTlRYUDsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktXRlhXSQwSGg0%3D) | 
| Push Button |	Push button switch, generic, two pins |	SW1,SW2 |	2 |	10 |	SW_Push |	0.053 |	0.53 |	Button_Switch_SMD:SW_SPST_B3U-1000P |	TS-1088-AR02016 |	[Link](https://www.lcsc.com/product-detail/C720477.html?s_z=s_q_p_PUSH%2520BUTTON%2520SWITCH&spm=wm.ssy.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFeVVRfQVlaXzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktfQVlADxALGw%3D%3D) | 
| ESD Diode |	Very low capacitance ESD protection diode, 2 data-line, SOT-23-6 |	U1 |	1 |	10 |	USBLC6-2SC6 |	0.041 |	0.41 |	Package_TO_SOT_SMD:SOT-23-6 |	USBLC6-2SC6 |	[Link](https://www.lcsc.com/product-detail/C2827654.html?s_z=s_p_USBLC6-2SC6&spm=wm.fly.bg.1.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfVlRVQFJeVTsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D) | 
| Linear Regulator |	600mA low dropout linear regulator, with enable pin, 3.8V-6V input voltage range, 3.3V fixed positive output, SOT-23-5 |	U2 |	1 |	5 |	AP2112K-3.3 |	0.1093 |	0.55 |	Package_TO_SOT_SMD:SOT-23-5 |	AP2112K-3.3TRG1 |	[Link](https://www.lcsc.com/product-detail/C23380830.html?s_z=s_q_AP2112K-3.3&spm=wm.fly.bg.1.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfVlReQ1BZXjsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D) | 
| ESP32-C3 |	802.11 b/g/n WiÂ­Fi and Bluetooth 5 module, ESP32Â­C3 SoC, RISCÂ­V microprocessor, On-board antenna |	U3 |	1 |	1 |	ESP32-C3-WROOM-02 |	3.33 |	3.33 |	RF_Module:ESP32-C3-WROOM-02 |	ESP32-C3-WROOM-02-H4 |	[Link](https://www.lcsc.com/product-detail/C2944070.html?s_z=n_q_ESP32-C3-WROOM-02&spm=wm.fly.bg.1.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfVlVSQFZYXzsOAxUeFF5JWBYZEEoKFBINSQcJGk4eFQsCAgIaSgADAwAHC0slRVJdX1ReRFFADxALGw%3D%3D) | 
| Crystal |	Two pin crystal |	Y1 |	1 |	5 |	32.768kHz |	0.2461 |	1.23 |	Crystal:Crystal_SMD_3215-2Pin_3.2x1.5mm |	3608S-32.768DTTLLL-R35L |	[Link](https://www.lcsc.com/product-detail/C42392410.html?s_z=n_q_t_crystal&spm=wm.fly.bg.4.xh___wm.ssy.tc.0.tz&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfVlZUQ1VYUjsOAxUeFF5JWBYZEEoKFBINSQcJGk4eFQsCAgIaSgADAwAHC0slRVhaU1RRR08GEwkK) | 
| **Total** | | | 	**30** |	**566** | | |		**12.19**			| 



<img width="1410" height="2000" alt="ESP32 Custom Devboard - Shelley Ma - Fallout Zine" src="https://github.com/user-attachments/assets/604187e0-e11a-415a-94c8-b94df5f6fb93" />

