- 👋 Hi, I’m @carlospercegona1
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
carlospercegona1/carlospercegona1 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# SPDX-License-Identifier: GPL-2.0
menu "Android"

config ANDROID
	bool "Android Drivers"
	help
	  Enable support for various drivers needed on the Android platform

if ANDROID

config ANDROID_BINDER_IPC
	bool "Android Binder IPC Driver"
	depends on MMU
	default n
	help
	  Binder is used in Android for both communication between processes,
	  and remote method invocation.

	  This means one Android process can call a method/routine in another
	  Android process, using Binder to identify, invoke and pass arguments
	  between said processes.

config ANDROID_BINDERFS
	bool "Android Binderfs filesystem"
	depends on ANDROID_BINDER_IPC
	default n
	help
	  Binderfs is a pseudo-filesystem for the Android Binder IPC driver
	  which can be mounted per-ipc namespace allowing to run multiple
	  instances of Android.
	  Each binderfs mount initially only contains a binder-control device.
	  It can be used to dynamically allocate new binder IPC devices via
	  ioctls.

config ANDROID_BINDER_DEVICES
	string "Android Binder devices"
	depends on ANDROID_BINDER_IPC
	default "binder,hwbinder,vndbinder"
	help
	  Default value for the binder.devices parameter.

	  The binder.devices parameter is a comma-separated list of strings
	  that specifies the names of the binder device nodes that will be
	  created. Each binder device has its own context manager, and is
	  therefore logically separated from the other devices.

config ANDROID_BINDER_IPC_SELFTEST
	bool "Android Binder IPC Driver Selftest"
	depends on ANDROID_BINDER_IPC
	help
	  This feature allows binder selftest to run.

	  Binder selftest checks the allocation and free of binder buffers
	  exhaustively with combinations of various buffer sizes and
	  alignments.

endif # if ANDROID

endmenu
