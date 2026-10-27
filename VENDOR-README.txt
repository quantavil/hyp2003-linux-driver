Copyright (C) 2023 Hypersecu Information Systems.
https://www.hypersecu.com/india-support

HyperPKI Manager for HYP2003 SDK For Linux
-------------------------------

	This package contains HyperPKI Manager for HYP2003 SDK with Cryptoki (PKCS#11) for Linux. HyperPKI Manager now supports HYP2003 Standard and HYP2003 Auto.


How to use it
-------------

	- No installation is required for the software contained in this package. Copy it to a system library dir or any location you want.

	- For a non-root user to communicate with the USB key, you must change the mode of the USB key's device file. There are two shell scripts to do this. Go to root and execute "sh config.sh" when first running the SDK before inserting the USB key. If you are not using the SDK, then simply execute "sh unconfig.sh".

	- If your system has selinux enabled, execute "chcon -t texrel_shlib_t libcastle_v2.so.1.0.0"

	- This support max 256 USB key

	- For Mozilla Firefox or Thunderbird Mail:
		1. Run Firefox
		2. In the Firefox main menu, select Options --> Advanced --> Certificates
		3. Click Security Devices and add "/your path/libcastle_v2.so.1.0.0" 
	 
	OR

	If your Firefox or Thunderbird's install directory is /usr/lib, then do the following:
		- For Firefox, enter the directory redist/NSS_Firefox_register
			To add a module, sh  register_Firefox.sh  A moduleName
			To delete a module, sh register_Firefox.sh  D moduleName.
	
		-For Thunderbird, enter the directory redist/NSS_Thunderbird_register
			- To add a module, sh register_Thunderbird.sh A moduleName 
			- To delete a module, sh register_Thunderbird.sh  D moduleName.
	

File List
---------

	config: This dir includes two shell files to change the USB device's file mode.
		config.sh: 	Change the system configuration
		unconfig.sh: 	Undo the system configuration

	readme: this file
	redist: Contains library file and user manager tool.
		libcastle_v2.so.1.0.0: 	HyperPKI Linux PKCS#11 library.
		HyperPKIMgr: 	HyperPKI Manager for HYP2003 (User Version)
		


