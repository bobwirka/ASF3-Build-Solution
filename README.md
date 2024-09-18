# ASF3-Build-Solution
The example projects in AFS3 include many that can't be built either in Atmel Studio or with the latest avr toolchain download. When you execute a Makefile in ASF3, you'll get many undefined symbol errors.

This is because many "ioxxx.h" header files changed between builds 3.6.2.1759 and 3.6.2.1778. I've been unable to find a download for the 1759 avr toolchain, but the available 3.6.1.1752 toolchain has the header files you nee to build these demos.

I've been working with the xmega series of processors, but a diff of the avr "io" headers shows that many files are different. Quite a few differences are in the boilerplate text at the top, but the xmega file iox32e5.h, for instance, has differences that make compilation impossible.

The solution is to add the 1752 build version of the required header file to the toolchain you're using and modify io.h to choose one or the other depending on a compiler "-D" flag. I copied the 1752 version of iox32e5.h as iox32e5-1752.h to the 3.7.0.1778 avr folder and modifie io.h to include an "#ifdef USE_1752" statement that included the 1752 header if defined.

If you're building one of the affected xmega projects, you include "-D USE_1752" in the compiler directives, and you're good to go.

In Atmel Studio, you add this compiler flag in the project preferences. In the ASF3 projects, you add it to the CCFLAGS entry in the gcc Makefile.
