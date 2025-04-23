
----------------------------------------------------------------------------------------------------------------
#   Fraunhofer upHear VQE - Voice Quality Enhancement
##  UROC delivery readme

    (C) 2015 - 2021 by Fraunhofer IIS
    $Id: uroc_delivery_readme.md 10286 2021-04-29 12:07:12Z mlo $
----------------------------------------------------------------------------------------------------------------

  This readme file contains information about the Fraunhofer UROC - Unified RObust Communicator delivery.
  UROC is part of the Fraunhofer upHear VQE - Voice Quality Enhancement product family.
  For package content and build information please refer to the dedicated sections for Linux, Darwin (macOS) and Windows.
  Additionally, a platform independent description of contents and usage is given.

----------------------------------------------------------------------------------------------------------------
###  General information on package types
----------------------------------------------------------------------------------------------------------------

  + Evaluation package:
    In the case of an evaluation package the UROC library is built with an 'eval beep'.
    A 'beep' of length 3 seconds is inserted into the output signal after every 5 minutes.
  
  + Release package:
    In the case of a release package the UROC library has no restrictions for the supported configurations.

    Use urocCmdl -version to retrieve library build information. See below "Building test command line application".
  
----------------------------------------------------------------------------------------------------------------
###  Contents - LINUX and DARWIN
----------------------------------------------------------------------------------------------------------------

  + uroc_for_delivery

        - urocCmdl
          - make: Makefile_deliver
          - src : uroc_main_deliver.c

        - uroclib
          - include : uroc_api.h
          - lib     : liburoc.a

        - inputData : sim1_ucap_7mic_4.25cm_16000.wav, sim1_ula_2mic_7cm_16000.wav ref_sim1_1spk_16000.wav
  
        - outputData : empty folder for default wav output file

        - tinywave
            - include : tinywavein_c.h, tinywaveout_c.h

----------------------------------------------------------------------------------------------------------------
###  Building test command line application - LINUX, DARWIN and ANDROID
----------------------------------------------------------------------------------------------------------------

  + cd to folder hosting makefile:
    cd urocCmdl/make

  + Build UROC binary:
    make -f Makefile_deliver
    Builds urocCmdl and intermediate files in the same folder.

  + Execute urocCmdl -h for options.

  + Executing urocCmdl -version retrieves build information about the linked UROC library.
    A library built as evaluation package shows the identifier (eval) for UROC library.
  
----------------------------------------------------------------------------------------------------------------
###  Build information - LINUX
----------------------------------------------------------------------------------------------------------------

  + Linux x86_64
  + gcc (Debian 6.3.0-18+deb9u1) 6.3.0 20170516
  + prebuilt static libraries: x86_64

----------------------------------------------------------------------------------------------------------------
###  Build information - LINUX armv7 (cortexhf)
----------------------------------------------------------------------------------------------------------------

  + cross-compiled on Linux x86_64
  + clang 8.0.1 with arm-linux-gnueabihf-gcc 4.9.1
  + prebuilt static library 32 bit
  
----------------------------------------------------------------------------------------------------------------
###  Build information - DARWIN
----------------------------------------------------------------------------------------------------------------

  + Darwin x86_64
  + Apple clang version 11.0.0 (clang-1100.0.33.17)
  + prebuilt static libraries: x86_64
  
----------------------------------------------------------------------------------------------------------------
###  Build information - ANDROID armv7
----------------------------------------------------------------------------------------------------------------

  + cross-compiled on Linux x86_64
  + arm-linux-androideabi-clang 6.0.2
  + prebuilt static library

----------------------------------------------------------------------------------------------------------------
###  Build information - ANDROID armv8
----------------------------------------------------------------------------------------------------------------

  + cross-compiled on Linux x86_64
  + aarch64-linux-android-clang 6.0.2
  + prebuilt static library

----------------------------------------------------------------------------------------------------------------
###  Contents - WINDOWS
----------------------------------------------------------------------------------------------------------------

  + uroc_for_delivery

        - urocCmdl
          - make: urocCmdlDeliverVS2015.sln, urocCmdlDeliverVS2015.vcxproj (Visual Studio 2015)
          - src : uroc_main_deliver.c

        - uroclib
          - include : uroc_api.h
          - lib     : uroclib.lib

        - inputData : sim1_ucap_7mic_4.25cm_16000.wav, sim1_ula_2mic_7cm_16000.wav ref_sim1_1spk_16000.wav
  
        - outputData : empty folder

        - tinywave
          - include : tinywavein_c.h, tinywaveout_c.h

----------------------------------------------------------------------------------------------------------------
###  Build information - WINDOWS
----------------------------------------------------------------------------------------------------------------

  + Microsoft Visual Studio 2015
  + prebuilt static libraries: x64

----------------------------------------------------------------------------------------------------------------
###  Building test command line application - WINDOWS
----------------------------------------------------------------------------------------------------------------

  + cd to folder hosting VS project:
    cd urocCmdl/make

  + Start urocCmdlDeliverVS2015.sln and select Config Release.
  + Build urocCmdlDeliverVS2015.sln:
    Builds urocCmdlDeliverVS2015.exe and intermediate files in urocCmdl/x64_Release.

  + Execute urocCmdlDeliverVS2015.exe -h for options.

  + Executing urocCmdlDeliverVS2015.exe -version retrieves build information about the linked UROC library.
    A library built as evaluation package shows the identifier (eval) for UROC library.
      
----------------------------------------------------------------------------------------------------------------
###  Description of contents
----------------------------------------------------------------------------------------------------------------

  The UROC package contains the UROC static library liburoc.a, uroclib.lib, resp.
  and associated API header uroc_api.h .
  The API header file provides documentation of the API functions.  
  
  For testing the library, a main source file is given with uroc_main_deliver.c .
  It shows an exemplary integration of the library into a command line application.
  
  Further, two simulated test WAV files are supplied.
  A seven channel microphone array signal, having six uniformly spaced mics on a circle and a center microphone,
  with a radius of 4.25 cm,
  as well as a single-channel reference speaker signal.
  Both have a sampling rate of 16 kHz and a bit depth of 16 bits.
  
----------------------------------------------------------------------------------------------------------------
###  Description of usage of command line application urocSimpleCmdl
----------------------------------------------------------------------------------------------------------------
 
  The command line application gives a complete integration example for the UROC library.
  
  Calling the command line application, here urocSimpleCmdl, with parameter -help displays help/usage:
      urocCmdl -help

  This library is customized, which means the library's functionality is tailored
  to the customer's requirements and use-cases.
  The customization is defined by a customer specific identifier (UROC ID). 
  Each UROC ID is associated with a particular device and a process mode.
  
  To get a list of all supported UROC IDs call the commandline application with parameter -idlist.
  
  The following UROC ID(s) is (are) enabled in this build:
  
      101    Yandex.Station 1 in ASR mode.
      102    LG WK7 in ASR mode.
      103    Yandex.Station 2 in COM mode.
      104    Yandex.Station 2 in ASR mode.
      105    Yandex.Station 2 in ASR mode with Residual Echo Reduction version 1   
      106    Yandex.Station 2 in ASR mode with Residual Echo Reduction version 2   
      107    Yandex.Station 2 in ASR mode with Residual Echo Reduction version 3   
      131    Yandex Audio Device Test for AEC.
      132    Yandex Audio Device Test for Beamformer.    
        
  A UROC ID can be selected with parameter -id of the command line application.
  
----------------------------------------------------------------------------------------------------------------
###  Example of usage of command line application urocSimpleCmdl
----------------------------------------------------------------------------------------------------------------
      
  Execute the binary, here urocSimpleCmdl, with the example test file as follows:

  Yandex Station 1 in ASR mode:
  
       ./urocSimpleCmdl -m ../../inputData/sim1_ucap_7mic_4.25cm_16000.wav \
                        -s ../../inputData/ref_sim1_1spk_16000.wav \
                        -o ../../outputData/uroc_out_1.wav \
                        -id 101

  LG WK7 in ASR mode:
  
       ./urocSimpleCmdl -m ../../inputData/sim1_ula_2mic_7cm_16000.wav \
                        -s ../../inputData/ref_sim1_1spk_16000.wav \
                        -o ../../outputData/uroc_out_1.wav \
                        -id 102
    
  Yandex Station 2 in COM mode:
  
       ./urocSimpleCmdl -m ../../inputData/sim1_ucap_7mic_4.25cm_16000.wav \
                        -s ../../inputData/ref_sim1_1spk_16000.wav \
                        -o ../../outputData/uroc_out_1.wav \
                        -id 103

  Yandex Station 2 in ASR mode:
  
      ./urocSimpleCmdl -m ../../inputData/sim1_ucap_7mic_4.25cm_16000.wav \
                       -s ../../inputData/ref_sim1_1spk_16000.wav \
                       -o ../../outputData/uroc_out_1.wav \
                       -id 104
  
  It writes an output WAV file in default directory outputData.

  The application reads and writes WAV files, using given tinywavein_c.h and tinywaveout_c.h.
  
----------------------------------------------------------------------------------------------------------------
###  Description of usage of UROC library and API
----------------------------------------------------------------------------------------------------------------
  
  For a complete documentation of the UROC API please refer to API header uroc_api.h .
  This is a high-level description of the most relevant API functions.
  
  Mandatory API functions, which have to be called in exactly this order, are: 
  
    Uroc_OpenPredefined()
    Uroc_Init()
    Uroc_Process()
    Uroc_Close()  

  Uroc_OpenPredefined()
    Has as input parameter a UROC ID,
    if successful, returns a valid handle to a UROC instance.

  Uroc_Init()
    Has as input parameter a valid handle to the UROC instance.

  Uroc_Process()
    Has as parameter a valid handle to the UROC instance.
    Has the audio data buffers as input and output parameters.
    This function has to be called in the frame-wise signal processing loop.    

  Uroc_Close()
    Has as input parameter a valid handle to the UROC instance.
    It deallocates the UROC instance.
  

  Uroc_IdToConfig()  
    Has as input parameter a UROC ID and returns the resulting UROC configuration.
    To retrieve the UROC configuration prior to instantiation and for monitoring purposes.

  Supported UROC IDs can be retrieved with API function Uroc_GetSupportedIds().
  A high-level description for a UROC ID can be retrieved with API function Uroc_GetUrocIdInfo().

  The command line application gives a complete integration example for the UROC library, using
  API functions Uroc_OpenPredefined(), Uroc_Init(), Uroc_Process(), Uroc_Close().
  
  The API function Uroc_Open() is supported in this build but is not recommended to be used.
  Its support might be removed with future updates.
  
----------------------------------------------------------------------------------------------------------------
###  Additional API functions
----------------------------------------------------------------------------------------------------------------

  In addition to the default functions used for the real-time processing, the API header uroc_api.h also
  contains a list of functions used for expert settings and tunings.
  Functions that are not relevant for the enabled processing mode will be disabled.
  
  Please note that any enabled expert function should only be used if it has been discussed
  or recommended by the Fraunhofer VQE team.
  
  List of enabled additional functions:
  
      Uroc_SetNoiseAttenuationLimit_dB()
      Uroc_GetWidebandDoa()
      Uroc_GetNmse_dB()
      Uroc_GetVadFlag()
      Uroc_GetInitDelayApplied()
      Uroc_SetBeamformerMode()
      Uroc_SetAgcActivity()
      Uroc_SetRelativeAgcTarget()
      Uroc_SetResAttenuationLimit_dB()
      Uroc_SetComplexReductionLevel()
      Uroc_SetRecMode()
  
----------------------------------------------------------------------------------------------------------------
###  Changelog
----------------------------------------------------------------------------------------------------------------

  v7.8.0
    - Enabled Residual Echo Cancellation for ASR mode for IDs 105, 106 and 107
    - Enabled Uroc_SetRecMode to change the REC mode(2 options)
    
  v7.7.0
    - Removed lower limit from Uroc_SetResAttenuationLimit_dB() sestter
    - Enabled AGC related setters

  v7.6.0
    - Reduced ASR mode complexity
    
  v7.5.0
    - Enabled support of up to three speaker reference input channels
    - Improved AEC tuning for station 2 IDs
    - Enabled the complexity reduction setter Uroc_SetComplexReductionLevel()
    - Fixed a bug that occured when selecting the IDs for Station 1 or LG WK7
  
  v7.4.0
    - Added DC offset removal.
    - Support for 512 frame-size for ASR mode
    - Support for 1024 frame-size for COM mode

  v7.3.0
    - for the UROC_ID_YANDEX_STATION_2_ASR ID, the residual echo suppression can now be set with API function Uroc_SetResAttenuationLimit_dB()
    - API function Uroc_GetEntropyVadFlag() has been renamed to Uroc_GetVadFlag()
    - API function Uroc_GetNMSE_dB() has been renamed to Uroc_GetNmse_dB()
    - API function Uroc_ForceOmniBeamformer() has been replaced by the Uroc_SetBeamformerMode() setter

  v7.1.0
    - added support of UROC IDs for LG WK7 and Audio Device Test (ADT)
    - added support of API function Uroc_OpenPredefined()
  
  v7.0.0
    - initial delivery of uroclib
  
----------------------------------------------------------------------------------------------------------------

  
