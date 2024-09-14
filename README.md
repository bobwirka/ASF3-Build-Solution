# ASF3-Build-Solution
The example projects in AFS3 include many that can't be built either in Atmel Studio or with the latest avr toolchain download. When you execute a Makefile in ASF3, you'll get many undefined symbol errors.

This is because the "ioxxx.h" header files changed between builds 3.6.2.1759 and 3.6.2.1778. I've been unable to find a download for the 1759 avr toolchain, but the 3.6.1.1752 toolchain has the header files you nee to build these demos.

The solution is to add the 1752 version of the required header file to the current toolchain and modify io.h to choose one or the other depending on a "-D"
