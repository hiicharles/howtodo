Howtodo - Ubuntu1604 - Fix Android Virtual Device Graphics
==========================================================


#### Error
----

    11:39 PM	Emulator: libGL error: unable to load driver: radeonsi_dri.so
    11:39 PM	Emulator: libGL error: driver pointer missing
    11:39 PM	Emulator: libGL error: failed to load driver: radeonsi
    11:39 PM	Emulator: libGL error: unable to load driver: swrast_dri.so
    11:39 PM	Emulator: libGL error: failed to load driver: swrast
    11:39 PM	Emulator: X Error of failed request:  BadValue (integer parameter out of range for operation)
    11:39 PM	Emulator: Major opcode of failed request:  154 (GLX)
    11:39 PM	Emulator: Minor opcode of failed request:  24 (X_GLXCreateNewContext)
    11:39 PM	Emulator: Value in failed request:  0x0
    11:39 PM	Emulator: Serial number of failed request:  58
    11:39 PM	Emulator: Current serial number in output stream:  59
    11:39 PM	Emulator: Process finished with exit code 1


#### Cause
----

    The library file libstdc++.so.6 came with Android SDK has issue.


#### Solution 1 : Change to Software GLES
----

	Tools -> AVD Manager -> Edit the selected AVD
    Change Graphics to Software - GLES 1.1


#### Solution 2 : Replace libstdc++.so.6 with system.
----

    $ sudo su

    [Find the file]
	# locate libstdc++.so.6
        /root/Android/Sdk/emulator/lib/libstdc++/libstdc++.so.6
        /root/Android/Sdk/emulator/lib/libstdc++/libstdc++.so.6.0.19
        /root/Android/Sdk/emulator/lib64/libstdc++/libstdc++.so.6
        /root/Android/Sdk/emulator/lib64/libstdc++/libstdc++.so.6.0.19
        /usr/lib/x86_64-linux-gnu/libstdc++.so.6
        /usr/lib/x86_64-linux-gnu/libstdc++.so.6.0.21
        /usr/share/gdb/auto-load/usr/lib/x86_64-linux-gnu/libstdc++.so.6.0.21-gdb.py
    
    [Backup]
	# cd /root/Android/Sdk/emulator/lib64/libstdc++/
    # mv libstdc++/libstdc++.so.6 libstdc++/libstdc++.so.6.bak

    [Use system]
	# cp /usr/lib/x86_64-linux-gnu/libstdc++.so.6 /root/Android/Sdk/emulator/lib64/libstdc++/ 

    [Restart Android Studio]
    Tools -> AVD Manager -> Edit the selected AVD
    Graphics : Hardware  Software - GLES 2.0
    Restart Android Studio



#### Source
----
[Cannot launch emulator on Linux (Ubuntu 15.10)
Ask Question](https://stackoverflow.com/questions/35911302/cannot-launch-emulator-on-linux-ubuntu-15-10/36625175)


