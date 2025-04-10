TOP=../..

include $(TOP)/configure/CONFIG
#----------------------------------------
#  ADD MACRO DEFINITIONS AFTER THIS LINE
#=============================

#=============================
# Build the IOC application

PROD_IOC = sr-cfcE
# sr-cfcE.dbd will be created and installed
DBD += sr-cfcE.dbd

# sr-cfcE.dbd will be made up from these files:
sr-cfcE_DBD += base.dbd

# Include dbd files from all support applications:
sr-cfcE_DBD += menuScan.dbd
sr-cfcE_DBD += system.dbd
sr-cfcE_DBD += asyn.dbd
sr-cfcE_DBD += calcSupport.dbd
sr-cfcE_DBD += okSupport.dbd
sr-cfcE_DBD += asSupport.dbd
sr-cfcE_DBD += stdSupport.dbd
sr-cfcE_DBD += devFileWaveform.dbd
sr-cfcE_DBD += devIocStats.dbd
sr-cfcE_DBD += okSNoASub.dbd
sr-cfcE_DBD += caPutLog.dbd
sr-cfcE_DBD += reccaster.dbd

USR_CPPFLAGS += -I$(OK)  -D_X86_64_ -DUNIX -DLINUX

# Add all the support libraries needed by this IOC
sr-cfcE_LIBS += llrfapp asyn autosave devIocStats calc sscan std caPutLog seq pv reccaster pvDatabase qsrv pvaClient pvAccessIOC pvAccess pvAccessCA nt pvData

sr-cfcE_SYS_LIBS += okFrontPanel

USR_LDFLAGS += -L$(OK)

# sr-cfcE_registerRecordDeviceDriver.cpp derives from sr-cfcE.dbd
sr-cfcE_SRCS += sr-cfcE_registerRecordDeviceDriver.cpp

# Build the main IOC entry point on workstation OSs.
sr-cfcE_SRCS_DEFAULT += sr-cfcEMain.cpp
sr-cfcE_SRCS_vxWorks += -nil-

# Add support from base/src/vxWorks if needed
#sr-cfcE_OBJS_vxWorks += $(EPICS_BASE_BIN)/vxComLibrary

LIBRARY_IOC += llrfapp

llrfapp_SRCS += okiface.cpp
llrfapp_SRCS += llrfPort.cpp
llrfapp_SRCS += calc.c
llrfapp_SRCS += devFileWaveform.c
llrfapp_SRCS += devFileWaveform0.c
llrfapp_SRCS += okSNoASub.c

# Link QSRV (pvAccess Server) if available
ifdef EPICS_QSRV_MAJOR_VERSION
    sr-cfcE_LIBS += qsrv
    sr-cfcE_LIBS += $(EPICS_BASE_PVA_CORE_LIBS)
    sr-cfcE_DBD  += PVAServerRegister.dbd
    sr-cfcE_DBD  += qsrv.dbd
endif

# Finally link to the EPICS Base libraries
sr-cfcE_LIBS += $(EPICS_BASE_IOC_LIBS)

#===========================

include $(TOP)/configure/RULES
#----------------------------------------
#  ADD RULES AFTER THIS LINE

