virtual-memory-exhausted--Cannot-allocate-memory
================================================

This problem happened when gcc was compiling a C file named loci.c in Indigo Virtual Switch (IVS) project. My gcc version is 4.8.1. and there is 4GB of swap memory in /dev/sda5 partition.

Here is the log of my compilation:

hon@ubuntu:/home/project/ivs$ sudo make clean
make -C targets/ivs clean
make[1]: Entering directory `/home/project/ivs/targets/ivs'
Cleaning Files
Cleaning Directories
make[1]: Leaving directory `/home/project/ivs/targets/ivs'
make -C targets/ivs-ctl clean
make[1]: Entering directory `/home/project/ivs/targets/ivs-ctl'
Cleaning Files
Cleaning Directories
make[1]: Leaving directory `/home/project/ivs/targets/ivs-ctl'
# The build system creates these even during make clean
rm -f modules/OVSDriver/OVSDriver.mk targets/ivs-ctl/IVSCtl.mk targets/ivs/Manifest.mk targets/ivs/IVS.mk targets/ivs/dependmodules.x
(cd indigo; rm -f modules/AIM/AIM.mk modules/BigData/BigList/BigList.mk modules/ELS/ELS.mk modules/FME/FME.mk modules/IOF/IOF.mk modules/IVS/IVS.mk modules/Indigo/OFConnectionManager/OFConnectionManager.mk modules/Indigo/OFStateManager/OFStateManager.mk modules/Indigo/SocketManager/SocketManager.mk modules/Indigo/indigo/indigo.mk modules/NSS/NSS.mk modules/PPE/PPE.mk modules/loci/loci.mk modules/murmur/murmur.mk modules/uCli/uCli.mk)
/bin/sh: 1: cd: can't cd to indigo
hon@ubuntu:/home/project/ivs$ sudo make
make -C targets/ivs
make[1]: Entering directory `/home/project/ivs/targets/ivs'
    Compiling[release]: IVSMain::main.c
    Creating Library: build/gcc-local/lib/IVSMain.a
    Compiling[release]: SocketManager::socketmanager.c
    Compiling[release]: SocketManager::socketmanager_config.c
    Compiling[release]: SocketManager::socketmanager_enums.c
    Compiling[release]: SocketManager::socketmanager_log.c
    Compiling[release]: SocketManager::socketmanager_module.c
    Compiling[release]: SocketManager::socketmanager_ucli.c
    Creating Library: build/gcc-local/lib/SocketManager.a
    Compiling[release]: OFConnectionManager::cxn_instance.c
    Compiling[release]: OFConnectionManager::ofconnectionmanager.c
    Compiling[release]: OFConnectionManager::ofconnectionmanager_config.c
    Compiling[release]: OFConnectionManager::ofconnectionmanager_enums.c
    Compiling[release]: OFConnectionManager::ofconnectionmanager_log.c
    Compiling[release]: OFConnectionManager::ofconnectionmanager_module.c
    Compiling[release]: OFConnectionManager::ofconnectionmanager_ucli.c
    Creating Library: build/gcc-local/lib/OFConnectionManager.a
    Compiling[release]: OFStateManager::bsn_counter_handlers.c
    Compiling[release]: OFStateManager::expiration.c
    Compiling[release]: OFStateManager::ft.c
    Compiling[release]: OFStateManager::group_handlers.c
    Compiling[release]: OFStateManager::handlers.c
    Compiling[release]: OFStateManager::listener.c
    Compiling[release]: OFStateManager::ofstatemanager.c
    Compiling[release]: OFStateManager::ofstatemanager_config.c
    Compiling[release]: OFStateManager::ofstatemanager_enums.c
    Compiling[release]: OFStateManager::ofstatemanager_log.c
    Compiling[release]: OFStateManager::ofstatemanager_module.c
    Compiling[release]: OFStateManager::ofstatemanager_ucli.c
    Compiling[release]: OFStateManager::weak.c
    Creating Library: build/gcc-local/lib/OFStateManager.a
    Compiling[release]: OVSDriver::bh.c
    Compiling[release]: OVSDriver::dump.c
    Compiling[release]: OVSDriver::experimenter.c
    Compiling[release]: OVSDriver::fwd.c
    Compiling[release]: OVSDriver::groups.c
    Compiling[release]: OVSDriver::kflow.c
    Compiling[release]: OVSDriver::multicast.c
    Compiling[release]: OVSDriver::ovs_driver.c
    Compiling[release]: OVSDriver::pipeline.c
    Compiling[release]: OVSDriver::translate_actions.c
    Compiling[release]: OVSDriver::translate_match.c
    Compiling[release]: OVSDriver::upcall.c
    Compiling[release]: OVSDriver::util.c
    Compiling[release]: OVSDriver::vport.c
    Creating Library: build/gcc-local/lib/OVSDriver.a
    Compiling[release]: Configuration::configuration.c
    Compiling[release]: Configuration::configuration_config.c
    Compiling[release]: Configuration::configuration_enums.c
    Compiling[release]: Configuration::configuration_log.c
    Compiling[release]: Configuration::configuration_module.c
    Compiling[release]: Configuration::configuration_ucli.c
    Compiling[release]: Configuration::sighup.c
    Creating Library: build/gcc-local/lib/Configuration.a
    Compiling[release]: loci::loci.c
virtual memory exhausted: Cannot allocate memory
make[1]: *** [build/gcc-local/obj//home/project/ivs/submodules/loxigen-artifacts/loci/src/loci.o] Error 1
make[1]: Leaving directory `/home/project/ivs/targets/ivs'
make: *** [all] Error 2
hon@ubuntu:/home/project/ivs$ gcc --version
gcc (Ubuntu 4.8.1-2ubuntu1~12.04) 4.8.1
Copyright (C) 2013 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

hon@ubuntu:/home/project/ivs$ cat /proc/swaps
Filename				Type		Size	Used	Priority
/dev/sda5                               partition	4991996	0	-1
hon@ubuntu:/home/project/ivs$ 
