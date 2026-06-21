# ESP32-C3 USB-C Devboard 

This is a custom 4-layer ESP32-C3 devboard built from scratch in KiCad, built around the ESP32-C3-WROOM-02. It's my second devboard (if a regulator can be counted as a devboard) with a full breakout of GPIOs and reset/boot buttons.

## Motivation 
This is my second-ever PCB; I built it to follow up on my first project. I've been interested in how ESP32s work so I thought this would be the best way to explore it! 

## How the Components Work 

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


<img width="545" height="796" alt="image" src="https://github.com/user-attachments/assets/747161ee-0904-4692-93ec-34f81beccd7b" />


<img width="1082" height="690" alt="image" src="https://github.com/user-attachments/assets/a5166ac8-f290-44b5-a05f-a8a495e2bc12" />



## Bill of Materials 
| Item |	Description |	Reference |	Qty |	MOQ |	Value |	Per Unit Price ($) |	Total Price ($) |	Footprint |	MPN |	URL | 
|------|--------------|-----------|-----|-----|-------|--------------------|------------------|-----------|-----|-----|
| 4u7 Capacitor |	Unpolarized capacitor |	C1,C2,C3,C4,C5 |	5 |	10 |	4u7 |	0.0505 |	0.51 |	Capacitor_SMD:C_0805_2012Metric |	CL21A475KBQNNNE |	[Link](https://www.lcsc.com/product-detail/C98192.html?s_z=s_c_Ceramic%2520Capacitors&spm=wm.fly.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFeXl1XRlNeXzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktTRk8GEwkK) |
| 100n Capacitor |	Unpolarized capacitor |	C6,C9,C10 |	3 |	10 |	100n |	0.0192 |	0.19 |	Capacitor_SMD:C_0201_0603Metric |	0805B104K500CT |	[Link](https://www.lcsc.com/product-detail/C83055.html?s_z=s_c_Ceramic%2520Capacitors&spm=wm.fly.bg.3.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFeXl1XRlNeXzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktTRk8GEwkK) |
| Capacitor |	Unpolarized capacitor |	C7,C8,R4 |	3 |	100 |	0n |	0.0052 |	0.52 |	Capacitor_SMD:C_0201_0603Metric |	TCC0805X7R501K500DT |	[Link](https://www.lcsc.com/product-detail/C5375938.html?spm=wm.fly.bg.3.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1ZVTlNXVzsOAxUeFF5JWBYZEEoKFBINSQcJGk4NBhADEA4cHktXRlVcSQwSGg0%3D) |
| ESD Diode |	Low capacitance unidirectional ESD protection diode, 5V, SOD-882D |	D1 |	1 |	5 |	PESD5V0L1ULD |	0.0978 |	0.49 |	Diode_SMD:D_SOD-882D |	PESD5V0L1ULD,315 |	[Link](https://www.lcsc.com/product-detail/C552557.html?s_z=s_p_PESD5V0L1ULD%252C315&spm=wm.fly.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1dXRVBfUDsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D) | 
| USB-C Receptacle |	USB 2.0-only 16P Type-C Receptacle connector |	J1 |	1 |	5 |	USB_C_Receptacle_USB2.0_16P |	0.099 |	0.5 |	Connector_USB:USB_C_Receptacle_G-Switch_GT-USB-7010ASV |	USB-TYPE-C-016 |	[Link](https://www.lcsc.com/product-detail/C2927036.html?s_z=s_p_USB-TYPE-C-016&spm=wm.fly.bg.0.xh&lcsc_vid=QQVaAVJeTlJdUVBVE1hcBVFWEwcNBVxeQwAPA1YHFQMxVlNeRVFfV1BWRlFcVTsOAxUeFF5JWBYZEEoKFBINSQcJGk4dAgUUFAk%3D) |
| 1x08 Connector |	Generic connector, single row, 01x08 |	J2,J3 |	2 |	5 |	Conn_01x08_Pin |	0.558 |	2.79 |	Connector_PinHeader_2.54mm:PinHeader_1x08_P2.54mm_Vertical |	N/A |	[Link](https://www.aliexpress.us/item/3256807202794047.html?spm=a2g0o.detail.pcDetailTopMoreOtherSeller.3.5ee0z10vz10vCf&gps-id=pcDetailTopMoreOtherSeller&scm=1007.40050.354490.0&scm_id=1007.40050.354490.0&scm-url=1007.40050.354490.0&pvid=f02ca764-02d9-42b0-aa3a-38bc3d3eef3d&_t=gps-id%3ApcDetailTopMoreOtherSeller%2Cscm-url%3A1007.40050.354490.0%2Cpvid%3Af02ca764-02d9-42b0-aa3a-38bc3d3eef3d%2Ctpp_buckets%3A668%232846%238111%231996&pdp_ext_f=%7B%22order%22%3A%2215779%22%2C%22eval%22%3A%221%22%2C%22sceneId%22%3A%2230050%22%2C%22fromPage%22%3A%22recommend%22%7D&pdp_npi=6%40dis%21USD%211.66%211.64%21%21%211.66%211.64%21%402103128917820104935402726e66ac%2112000040551940967%21rec%21US%217756416958%21X%211%210%21n_tag%3A-29911%3Bd%3A882c3b75%3Bm03_new_user%3A-29895&utparam-url=scene%3ApcDetailTopMoreOtherSeller%7Cquery_from%3A%7Cx_object_id%3A1005007389108799%7C_p_origin_prod%3A) | 


<img width="1410" height="2000" alt="ESP32 Custom Devboard - Shelley Ma - Fallout Zine" src="https://github.com/user-attachments/assets/604187e0-e11a-415a-94c8-b94df5f6fb93" />

