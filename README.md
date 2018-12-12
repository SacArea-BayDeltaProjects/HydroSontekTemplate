# SontekTemplate
## [CR1000 and CR6 Datalogger template for SonTek Argonaut ADCPs]

*This program is designed for use with the updated station electronics board only.*

Update datalogger operating system to most current version. UPDATING OPERATING SYSTEM WIPES ALL MEMORY FROM DATALOGGER! DO NOT ATTEMPT REMOTE OS UPDATE UNLESS YOU'VE DISCUSSED WITH TV.

If this is a PROGRAM UPDATE to an existing station with new electronics board, verify whether parameters need updating or not. If parameters (startbin/endbin/offsets/ratings, etc). need to be updated, you must DELETE THE FILE IN THE USR DRIVE OF THE DATALOGGER. Otherwise, previous settings will be loaded (This is used if there is an outage at a station it will reboot with most recent parameters).

**Argonaut Settings:**

  - Needs to be set to Defaults (*DEF*). Write down setup parameters first.
  - Set to 55 second Average Interval
  - Set to 60 second Sample Interval
  - Set OutFormat = English
  - Set OutMode = Auto
  - Set AutoSleep = No
  - Set Coordinate System = ENU (East,North,Up)
  - Save Settings (SSU)

Open "SonTekTemplateMaster.dld" with CRBasic Editor.

**Before Compiling/Sending to Datalogger:**

  1. Use "Tools" menu to set .dld datalogger type for the target datalogger. (CR6 or CR1000). (Tools>Set .DLD Datalogger Type. OR Ctrl+E)
  
  2. Select proper constants in Customize Constants menu. (Tools>Customize Constants)
     
     Description of Constants:
    
     - **WqBaud:** If sonde is present, select baud rate for serial communications. Most likely, 38400 is correct.
     - **IsWqMax232:** If sonde is present, is there a Max232 chip present in the communication system?
        - *Max232 board IS NECESSARY for sondes on CR1000 C-ports and CR6 U-ports*
     - **IsVmMax232:** Is there a Max232 chip present in the communication system for the velocity meter?
        - *Not necessary on either set of ports, but should probably be used for CR6 U-ports or long RS232 cable runs.*
     - **IsTltMax232:** If external tilt sensor is present, is there a Max232 chip present in the communication system?
     - **WQDeadCntMax:** How many minutes should the datalogger wait to cycle power to sonde if no data are coming in? (intervals of 5min)
     - **VWDeadCntMax:** How many minutes should the datalogger wait to cycle power to ADCP if no data are coming in? (intervals of 5min)
     - **PrimeStageSource:** Select source instrument for primary gage height data.
     - **SecndStageSource:** Select source instrument for backup gage height data.
     - **HasTiltSensor:** Is an external tilt sensor present in the system?
     
   **For further clarification, please talk to TV.**
   
   3. Conditional Compile and Save. (Compile>Conditional Compile and Save) Rename with target station ID and date.
   
   4. In the new file, define which ports the velocity meter and sonde will communicate through. (Easiest way: Scroll to top of program, Ctrl+F for "AdcpPort" to find the proper parameters. **IMPORTANT: If using CR6 ports ComC1 or ComC3, use DevConfig to configure the ports to RS232 (NOT TTL or other).**
   
   *On CR1000, port options are: Com1 or Com2. On CR6: ComC1, ComC3, ComU1. Other ports are currently ressered for SDI12 instruments.*
   
   5. Define station specific parameters. (GoTo>Navigation>Subroutine Section. "GetStartup" is the name of the proper subroutine for these changes.) If it's a sidelooker: Right bank mount, Flowsign = 1, Left bank mount, Flowsign = -1. If it's an uplooker: Theta = compass heading of positive flow direction.
   
   6. Save and Compile program, look for compilation errors (Hopefully none!) (Compile>Save and Compile)
   
   7. If no errors (warnings are generally OK), load file onto datalogger.
