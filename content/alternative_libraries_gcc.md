Title: Build using alternative libraries with GCC
Date:  2013-12-27
Category: learning
Tags: gcc, boost, debian, c++, linux

I’m a debian user, and I like the way it’s stable. For debian stable means really stable, but this has a cost, at the most of the time we don’t have the latest version of a package, which makes debian not really a suitable distribution for development.

But this is not really important, we can always try to build programs from sources at this level we might have another issue. The latest version of the package may require a later version of a library.
Let’s take the example of `boost`.

The program below uses signals from the `boost` library. Signals are quite useful, every time a signal is emitted, it will be handled by the function to which it's connected to.

    :::cpp
    // main.cpp
    #include <iostream>
    #include <boost/signals2.hpp>
    
    void mySlot(){
         std::cout << "I'm a slot " << std::endl;
    }
    int main(int argc, char **argv){
         boost::signals2::signal<void ()> sig;
         sig.connect(mySlot);
         sig();
         return 0;
    }

To build this program we have to install the boost library :

    :::bash
    sudo apt-get install libboost-signals1.49-dev


The actual version of boost available on debian wheezy (7.3) is : `boost-1.49`.

> Make sure you add the `-dev` suffix to install the boost library headers.

This command will download and install the package that contains useful files such as headers (`.hpp` files) and the static and dynamic libraries (respectively `.a` and `.so` files).

The header files will be installed in `/usr/include/boost/`.

and the libraries will be in `/usr/lib/`.

Now all you have to do is to run your compiler command and tell him that you wish to link with the `libboost-signals` library :

    :::bash
    gcc main.cpp -o myProgram -lboost-signals

After translating our program to objects, the final step before the binary become runnable is the linking step, the linker will try to link non user-defined functions with the libraries, so that at run time, our program will find the implementation of theses functions.

The linker will start to look for the libraries (like `libboost-signals`) in the lib directories `/usr/lib and /lib` and link your program.

You can always check with what libraries your program is linked, with the command `ldd`, in this case `ldd myProgram` will return :

    :::bash
    linux-vdso.so.1 =>  (0x00007fffb256f000)
    libboost_signals.so.1.49.0 => /usr/lib/libboost_signals.so.1.49.0 (0x00007f3d3ef7a000)
    libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007f3d3ec73000)
    libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007f3d3ea5c000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f3d3e6d2000)
    librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007f3d3e4ca000)
    libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f3d3e247000)
    libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f3d3e02b000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f3d3efbf000)

We can clearly see that our program is linked with `libboost_signals.so.1.49.0` wich is located at ̀`/usr/lib/libboost_signals.so.1.49.0`.

If it didn't succeed to find in both, it will returns and error `undefined reference to ....`

But what if I want to use the latest version which is `boost-1.55` ? 

You can specify the first path where the linker should look for the libraries by using the `-L` option. 

Let's assume that your new fresh build library is located at `/opt/boost_1_55/`

The new command will be :

    :::bash
    gcc main.cpp -o myProgram -L/opt/boost_1_55/lib/ -lboost_signals

The linker will look for the library in `/opt/boost_1_55/lib` if not it will carry on with the remaining directories mentioned above : and the result of ldd myProgram is now :

    linux-vdso.so.1 =>  (0x00007fffb256f000)
    libboost_signals.so.1.55.0 => /opt/boost_1_55/lib/libboost_signals.so.1.55.0 (0x00007f0592949000)
    libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007f3d3ec73000)
    libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007f3d3ea5c000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f3d3e6d2000)
    librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007f3d3e4ca000)
    libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f3d3e247000)
    libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f3d3e02b000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f3d3efbf000)
