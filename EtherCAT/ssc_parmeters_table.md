
|  Group   | Parameter | AX58100 Default Value | Description |
|----------|----------|----------|----------|
|   Slave Info |||  |
|| VENDOR_ID | 0x00000000  |Object 0x1018 SI1 (Vendor ID).An unique EtherCAT Vendor ID is required.   |
|| VENDOR_NAME    | CHRP.pro   |EtherCAT slave vendor name   |
|| PRODUCT_CODE |   |Object 0x1018 SI2 EtherCAT product code  |
||REVISION_NUMBER||Object 0x1018 SI3 (EtherCAT product revision number)|
||SERIAL_NUMBER||Object 0x1018 SI4 (EtherCAT product serial number)|
||DEVICE_PROFILE_TYPE||Slave device type (Object 0x1000) |
||DEVICE_NAME||Name of the slave device (Object 0x1008)|
||DEVICE_HW_VERSION||Hardware version of the slave device (Object 0x1009)|
||DEVICE_SW_VERSION||Software version of the slave device (Object 0x100A)|
|Generic||||
||SYSTEM_HEADER_FILE||Define include syntax for system header file|
||EXPLICIT_DEVICE_ID|0|If this switch is set Explicit device ID requests are handled. For further information about Explicit Device ID see ETG.1020 specification: www.ethercat.org/MemberArea/download_protocolenhancements.asp|
||ESC_SM_WD_SUPPORTED|1|This switch should be set if the SyncManger watchdog provided by the ESC should be used. If reset the process data watchdog is triggered by a local timer|
||STATIC_OBJECT_DIC|0|If this switch is set, the object dictionary is "build" static (by default only PIC18 objects are added static)|
||ESC_EEPROM_ACCESS_SUPPORT|0|If this switch is set the slave stack provides functions to access the EEPROM|
|Hardware||||
||EL9800_HW|0|Shall be set if the Slave code is executed on the PIC mounted on the EL9800 EtherCAT Evaluation Board.(if the MCI interface provided by EL9800 board should be used MCI_HW shall be set and this define shall be reset).This settings should also be enabled if the ESC is connected via a serial interface and no specific hardware access files are avilable yet.NOTE: The PDI type needs also to be configured in the "ESC_CONFIG_DATA"|
||MCI_HW|0|Shall be set if the MCI of the ESC is connected. This settings should also be enabled if the ESC is connected via a parallel interface and no specific hardware access files are avilable yet. NOTE: The PDI type needs also to be configured in the "ESC_CONFIG_DATA"|
||FC1100_HW|0|Shall be set if the EtherCAT slave controller is located on an FC1100 PCI card.NOTE: The PDI type needs also to be configured in the "ESC_CONFIG_DATA"|
||HW_ACCESS_FILE||Define include syntax for a user specific hardware access file. e.g #include "myhardware.h" (will only be added if no default hardware access is selected) NOTE: The PDI type needs also to be configured in the "ESC_CONFIG_DATA"|
||CONTROLLER_16BIT|1|Shall be set if the host controller is a 16Bit architecture|
||CONTROLLER_32BIT|0|Shall be set if the host controller is a 32Bit architecture|
||_PIC18|0|Microchip PIC18F452 Specific Code This processor is mounted on the Beckhoff Slave Evaluation Board (Hardware version up to EL9800_2)|
||_PIC24|0|Microchip PIC24HJ128GP306 Specific Code. This processor is mounted on the Beckhoff Slave Evaluation Board (Hardware version up to EL9800_4A)|
||ESC_16BIT_ACCESS|1|If the microcontroller only supports 16Bit access to the ESC|
||ESC_32BIT_ACCESS|0|If the microcontroller only supports 32Bit access to the ESC|
||MBX_16BIT_ACCESS|1|If the microcontroller only supports 16Bit access to local mailbox memory(access to ESC DPRAM is controlled by "ESC_16BIT_ACCESS"). If reset 8Bit access is used|
||BIG_ENDIAN_16BIT|0|If the microcontroller always make 16 bit access to external memory, operates in BigEndian format and the switching of the high and low byte is done in hardware|
|| BIG_ENDIAN_FORMAT|0|If the microcontroller works with BigEndian format, then this switch shall be set. In that case all WORD-and DWORD-accesses will make a BYTE- or WORD-swapping, the macros SWAPWORD and SWAPDWORD in ecatslv.h might be adapted. If this switch is set, then BIG_ENDIAN_16BIT shall be reset.|
||EXT_DEBUGER_INTERFACE|0|If this switch is set, the external debugger interface on the EL9800_4A (_PIC24) will be activated. This define will be ignored if _PIC24 is not set.|
||UC_SET_ECAT_LED|0|If set the EtherCAT Run and Error LEDs are set by the uController. If set ESC_SUPPORT_ECAT_LED shall be reset.|
||ESC_SUPPORT_ECAT_LED|0|This switch can be enabled if the connected ESC support Error and Run LED indication. See the ESC datasheet if the LED indication is supported. If set UC_SET_ECAT_LED shall be reset.|
||ESC_EEPROM_EMULATION|0|If this switch is set EEPROM emulation is supported. Not all ESC types support EEPROM emulation. See ESC datasheet for more information.|
||CREATE_EEPROM_CONTENT|0|Set to true if the EEPROM content shall be created and stored in a header file. If EEPROM emulation is enabled this setting should also be enabled (if the ESI file will be modified later on the file can be generated again by the EEPROM programmer (see "Tool" menu)). NOTE: This setting will only be evaluated if EEPROM emulation is active.|
||ESC_EEPROM_SIZE|0x800|Specify the EEPROM size in Bytes of the connected EEPROM or the emulated EEPROM.|
||EEPROM_READ_SIZE|0x8|Only required if EEPROM emulation is active. This value defines the number of bytes which will be read per opertion.|
|EtherCAT State Machine||||
||BOOTSTRAPMODE_SUPPORTED|0|If the firmware update over FoE services should be supported, then this switch shall be set. If this switch is set, then also "FOE_SUPPORTED" shall be set.|
||OP_PD_REQUIRED|1|If this switch is reset the state transition SAFEOP_2_OP will also successful if no process data was received. The watchdog will only be active when first process data was received (bEcatFirstOutputsReceived)|
||PREOPTIMEOUT|0x7d0|Specify timeout value for the state transition from Init to PreOP/Boot.(ESI Value : "PreopTimeout"). NOTE: Within the stack this value - 50ms will be used to react before the master run into the timeout.|
||SAFEOP2OPTIMEOUT|0x2328|Specifiy the timeout from SafeOP to OP. (ESI Value : "SafeopOpTimeout") NOTE: Within the stack this value - 50ms will be used to react before the master run into the timeout.
|Synchronization||||
||AL_EVENT_ENABLED|1|If an interrupt routine shall be called when one of the Events in the AL Event Register (0x220) changes,this switch has to be defined to 1 (synchronous modes are supported).If the AL Event register shall only be polled, this switch has to be defined to 0 (only free run mode is supported).|
||DC_SUPPORTED|1|If distributed clocks should be supported by the slave, then this switch shall be set.If this switch is set, then also AL_EVENT_ENABLED shall be set.NOTE: The DC support needs also be set in the "ESC_CONFIG_DATA" settings.|
||ECAT_TIMER_INT|1| If this switch is set, then the watchdog time for the EtherCAT watchdog will be checked in a timer interrupt routine.
||MIN_PD_CYCLE_TIME|0x7A120|Minimum cycle time in ns the slave is supporting (entry 0x1C32:05 or entry 0x1C33:05)
||MAX_PD_CYCLE_TIME|0xC3500000|Maximum cycle time in ns the slave is supporting
||PD_OUTPUT_DELAY_TIME|0|Minimum output delay time in ns the slave is supporting (entry 0x1C32:09)|
||PD_OUTPUT_CALC_AND_COPY_TIME|0|Output calc+copy time in ns the slave is supporting (entry 0x1C32:06)
||PD_INPUT_CALC_AND_COPY_TIME|0|Input calc+copy time in ns the slave is supporting (entry 0x1C33:06)
||PD_INPUT_DELAY_TIME|0|Input delay time in ns the slave is supporting (entry 0x1C33:09)
|Application||||
||TEST_APPLICATION|READ ONLY|NOTE: THIS SETTING SHALL NOT BE USED TO CREATE A USER SPECIFIC APPLICATION!Select this setting to test the slave stack or a master implementation. For further information about this application see the SSC Application Node.
|Process Data||||
||MIN_PD_WRITE_ADDRESS|0x1000|Minimum address for the process output data (Sync Manager 2)inside the application memory of the EtherCAT Slave Controller which could be set by the master. The setting have to be within the ranges of the user memory of the ESC (this is not checked by the tool).
||DEF_PD_WRITE_ADDRESS|0x1100|Default address for the process output data (Sync Manager 2). The value shall be within the ESC address range.
||MAX_PD_WRITE_ADDRESS|0x2FFF|Maximum address for the process output data (Sync Manager 2)inside the application memory of the EtherCAT Slave Controller which could be set by the master. The setting have to be within the ranges of the user memory of the ESC (this is not checked by the tool).
||MIN_PD_READ_ADDRESS|0x100|Minimum address for the process input data (Sync Manager 3) inside the application memory of the EtherCAT Slave Controller which could be set by the master. The setting have to be within the ranges of the user memory of the ESC (this is not checked by the tool).
||DEF_PD_READ_ADDRESS|0x1400|Default address for the process output data (Sync Manager 3). The value shall be within the ESC address range.
||MAX_PD_READ_ADDRESS|0x2FFF|Maximum address for the process input data (Sync Manager 3) inside the application memory of the EtherCAT Slave Controller which could be set by the master. The setting have to be within the ranges of the user memory of the ESC (this is not checked by the tool).
||MAX_PD_INPUT_SIZE|0x0044|Maximum size of the process input data (Sync Manager 3) for cyclic exchange.
||MAX_PD_OUTPUT_SIZE|0x044|Maximum size of the process output data (Sync Manager 2) for cyclic exchange.
|Mailbox||||
||MAILBOX_QUEUE|1|If this switch is set, the mailbox services will be stored in a queue.With this switch reset only one mailbox service can be processed in parallel.
||AOE_SUPPORTED|0|If the AoE services are supported, then this switch shall be set.
||COE_SUPPORTED|1|If the CoE services are supported, then his switch shall be set.
||COMPLETE_ACCESS_SUPPORTED|1|If the complete SDO access (accessing all entries of an object with one SDO service, then this switch shall be set. Furthermore,COE_SUPPORTED shall be set.
||SEGMENTED_SDO_SUPPORTED|1| If the segmented SDO services should be supported, then this switch shall be set. Furthermore, COE_SUPPORTED shall be set.
||SDO_RES_INTERFACE|1|If a SDO response cannot be generated immediately (e.g. when access over a serial interface is needed), this switch should be set. In that case ABORTIDX_WORKING shall be returned from OBJ_Read or OBJ_Write and the response shall be sent by calling SDOS_SdoRes, when the response is available.
||BACKUP_PARAMETER_SUPPORTED|0|If this switch is set, then the functions in the application example to load and store backup parameter will be compiled. Furthermore, COE_SUPPORTED shall be set.
||STORE_BACKUP_PARAMETER_IMMEDIATELY|0|Objet values will be stored when they are written.This switch is only evaluated if "BACKUP_PARAMETER_SUPPORTED" is set.
||DIAGNOSIS_SUPPORTED|0| If this define is set the slave stack supports diagnosis messages (Object 0x10F3). To support diagnosis messages COE_SUPPORTED shall be enabled and the platform shall support dynamic memory allocation. NOTE: this feature is implemented according to ETG.1020
||MAX_DIAG_MSG|0x14|Number of diagnosis message ringbuffer
||EMERGENCY_SUPPORTED|0|If this define is set the slave stack supports emergency messages. COE_SUPPORTED or SOE_SUPPORTED shall be enabled
||MAX_EMERGENCIES|1|Number of emergencies supported in parallel
||VOE_SUPPORTED|0|If the VoE services should be supported, then this switch shall be set. This means only the calling of the VoE functions in mailbox.c are implemented, but the VoE service functions have to be added. Furthermore, the example code cannot be linked correctly, because these functions are missing.
||SOE_SUPPORTED|0|If the SoE services should be supported, then this switch shall be set. This means only the calling of the SoE functions in mailbox.c are implemented, but the SoE service functions have to be added. Furthermore, the example code cannot be linked correctly, because these functions are missing.|
||EOE_SUPPORTED|0|If the EoE services should be supported, then this switch shall be set.
||STATIC_ETHERNET_BUFFER|0|If this switch is set a static buffer is used to store ethernet frames, otherwise the buffer is allocated on demand
||FOE_SUPPORTED|0|If the FoE services should be supported, then this switch shall be set.
||FOE_SAVE_FILES|0|If set incoming Files are stored in "aFileData" max file size is set by MAX_FILE_SIZE.
||MAX_FILE_SIZE|0x180|Maximum file size
||MAX_MBX_SIZE|0x0100|Maximum mailbox size (Sync Manager 0 and 1) which could be set by the master.
||MIN_MBX_WRITE_ADDRESS|0x1000|Minimum address for the write (receive) mailbox (Sync Manager 0). The setting have to be within the ranges of the user memory of the ESC (this is not checked by the tool).
||DEF_MBX_WRITE_ADDRESS|0x1000|Default address for the process output data (Sync Manager 0). The value shall be within the ESC address range.|
||MAX_MBX_WRITE_ADDRESS|0x2FFF|Maximum address for the write (receive) mailbox (Sync Manager 0). The setting have to be within the ranges of the user memory of the ESC (this is not checked by the tool).
||MIN_MBX_READ_ADDRESS|0x1000| Minimum address for the read (send) mailbox (Sync Manager 1).
||DEF_MBX_READ_ADDRESS|0x1080|Default address for the process output data (Sync Manager 1). The value shall be within the ESC address range and less than the SyncManager 0 range.
||MAX_MBX_READ_ADDRESS|0x2FFF|Maximum address for the read (send) mailbox (Sync Manager 1).