# Fuses

0x00 WDTCFG WINDOW[3:0] PERIOD[3:0] 
0x01 BODCFG LVL[2:0] SAMPFREQ ACTIVE[1:0] SLEEP[1:0]
0x02 OSCCFG OSCLK NA[4:0] FREQSEL[1:0]
0x03 reserved
0x04 reserved
0x05 SYSCFG0 CRCSRC[1:0] NA TOUTDIS RSTPINCFG[1:0] NA EESAVE
0x06 SYSCFG1 NA[4:0] SUT[2:0]
0x07 APPEND APPEND[7:0]
0x08 BOOTEND BOOTEND[7:0]


## Watchdog Configuration WDTCFG

Bits 7:4 – WINDOW[3:0] Watchdog Window Time-out Period
This value is loaded into the WINDOW bit field of the Watchdog Control A (WDT.CTRLA) register during reset.
Bits 3:0 – PERIOD[3:0] Watchdog Time-out Period
This value is loaded into the PERIOD bit field of the Watchdog Control A (WDT.CTRLA) register during reset.


## Brown Out Detect (BOD) Configuration BODCFG

### Bits 7:5 - LVL[2:0] BOD Level

0x0
BODLEVEL0
1.8V
0x1
BODLEVEL1
2.15V
0x2
BODLEVEL2
2.60V
0x3
BODLEVEL3
2.95V
0x4
BODLEVEL4
3.30V
0x5
BODLEVEL5
3.70V
0x6
BODLEVEL6
4.00V
0x7
BODLEVEL7
4.30V

### Bit 4 - SAMPFREQ BOD Sample Frequency
This value is loaded into the SAMPFREQ bit of the BOD Control A (BOD.CTRLA) register during Reset.
Value
Description
0x0
The sample frequency is 1 kHz
0x1
The sample frequency is 125 Hz


### Bits 3:2 – ACTIVE[1:0] BOD Operation Mode in Active and Idle
This value is loaded into the ACTIVE bit field of the BOD Control A (BOD.CTRLA) register during Reset.
Value
Description
0x0
Disabled
0x1
Enabled
0x2
Sampled
0x3
Enabled with wake-up halted until BOD is ready


### Bits 1:0 – SLEEP[1:0] BOD Operation Mode in Sleep
This value is loaded into the SLEEP bit field of the BOD Control A (BOD.CTRLA) register during Reset.
Value
Description
0x0
Disabled
0x1
Enabled
0x2
Sampled
0x3
Reserved


## Oscillator Configuration OSCCFG

### Bit 7 – OSCLOCK Oscillator Lock
This fuse bit is loaded to LOCK in CLKCTRL.OSC20MCALIBB during reset.
Value
Description
0
Calibration registers of the 20 MHz oscillator are accessible
1
Calibration registers of the 20 MHz oscillator are locked

### Bits 1:0 – FREQSEL[1:0] Frequency Select

These bits select the operation frequency of the 20 MHz internal oscillator (OSC20M) and determine the respective
factory calibration values to be written to CAL20M in CLKCTRL.OSC20MCALIBA and TEMPCAL20M in
CLKCTRL.OSC20MCALIBB.
Value
Description
0x0
Reserved
0x1
Run at 16 MHz
0x2
Run at 20 MHz
0x3
Reserved


## System Configuration 0 SYSCFG0

### Bits 7:6 – CRCSRC[1:0] CRC Source
See the CRC description for more information about the functionality.
Value
Name
Description
0x0
FLASH
CRC of full Flash (boot, application code and application data)
0x1
BOOT
CRC of the boot section
0x2
BOOTAPP
CRC of application code and boot sections
0x3
NOCRC
No CRC

### Bit 4 – TOUTDIS Time-Out Disable
This bit can disable the blocking of NVM writes after POR.
When the TOUTDIS bit in FUSE.SYSCFG0 is ‘0’ and the RSTPINCFG bit field in FUSE.SYSCFG0 is configured to
GPIO or RESET, there will be a time-out period after POR that blocks NVM writes.
The NVM write block will last for 768 OSC32K cycles after POR. The EEBUSY and FBUSY bits in the
NVMCTRL.STATUS register must read ‘0’ before the page buffer can be filled or NVM commands can be issued.
Value
Description
0
NVM write block is enabled
1
NVM write block is disabled

### Bits 3:2 – RSTPINCFG[1:0] Reset Pin Configuration
This bit selects the pin configuration for the Reset pin.
Note: When configuring the Reset pin as GPIO, there is a potential conflict between the GPIO actively driving the
output, and a high-voltage UPDI enable sequence initiation. To avoid this, the GPIO output driver is disabled for 768
OSC32K cycles after a System Reset. Enable any interrupts for this pin only after this period.
Value
0x0
0x1
0x2
0x3
Description
GPIO
UPDI
RESET
UPDI w/alternate RESET pin

### Bit 0 – EESAVE EEPROM Save Across Chip Erase
This bit controls if the EEPROM is being erased during a Chip Erase. If enabled, only the Flash memory will be
erased by the Chip Erase. If the device is locked, the EEPROM is always erased by a Chip Erase regardless of this


## System Configuration 1 SYSCFG1

### Bits 2:0 – SUT[2:0] Start-up Time Setting
These bits select the start-up time between power-on and code execution.
Value
Description
0x0
0 ms
0x1
1 ms
0x2
2 ms
0x3
4 ms
0x4
8 ms
0x5
16 ms
0x6
32 ms
0x7
64 ms
bit.
Value
Description
0
EEPROM erased during Chip Erase
1
EEPROM not erased under Chip Erase


## Application Code End APPEND
The default value given in this fuse description is the factory-programmed value, and should not be mistaken for the
Reset value.
Bit

### Bits 7:0 – APPEND[7:0] Application Code Section End
This bit field controls the combined size of the Boot Code section and Application Code section in blocks of 256
bytes. For more details, refer to the Nonvolatile Memory Controller section.
Note: If FUSE.BOOTEND is 0x00, the entire Flash is the Boot Code section.

## Boot End BOOTEND

### Bits 7:0 – BOOTEND[7:0] Boot Section End
This bit field controls the size of the boot section in blocks of 256 bytes. A value of 0x00 defines the entire Flash as
Boot Code section.
For more details, refer to the Nonvolatile Memory Controller section.


