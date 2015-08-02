### Basic Hello World

Testing [CLion](https://www.jetbrains.com/clion) from [JetBrains](https://www.jetbrains.com/)

Will use this [CLion](https://www.jetbrains.com/clion) software for my study of the book [Programming: Principles and Practice Using C++ (2nd Edition)](http://www.amazon.com/Programming-Principles-Practice-Using-2nd/dp/0321992784/ref=sr_1_1?ie=UTF8&qid=1437274549&sr=8-1&keywords=bjarne&pebp=1437274553256&perid=1QMN2V5D6QK30NXBAK61)

From the book:

```cpp
#include <iostream>

using namespace std;

int main() {
    cout << "Hello, World!\n" ;
    return 0;
}
```

![CLion](https://www.dropbox.com/s/bloq05domxtftva/Screenshot%202015-07-19%2016.18.15.png?dl=1)

### Vagrantfile

This example include a `Vagrantfile` that will setup a linux VM using Vagrant

In this example, the script will create a temp dir inside the VM, and compile and run the code in the virtual machine

The script will find the executable file created, and will run it. On this project is `./HelloWorld`

On first run, do `vagrant up`

At the moment of this writing, this Vagrantfile will start 3 VMs
- precise64
- trusty64
- vivid64

```bash
$ vagrant status
Current machine states:

precise64                 running (virtualbox)
trusty64                  running (virtualbox)
vivid64                   running (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state.
$
```

After code modification, you can trigger a new run of the code as `vagrant provision` to run all the scripts.

On this project, the script that test the code is called `code`, so you can use `vagrant provision --provision-with code`

ie:

```bash
$ vagrant provision --provision-with code
==> precise64: Running provisioner: code (shell)...
    precise64: Running: inline script
==> precise64: /tmp/tmp.mxfYnIAfbm ~
==> precise64: -- The C compiler identification is GNU 4.8.1
==> precise64: -- The CXX compiler identification is GNU 4.8.1
==> precise64: -- Check for working C compiler: /usr/bin/cc
==> precise64: -- Check for working C compiler: /usr/bin/cc -- works
==> precise64: -- Detecting C compiler ABI info
==> precise64: -- Detecting C compiler ABI info - done
==> precise64: -- Detecting C compile features
==> precise64: -- Detecting C compile features - done
==> precise64: -- Check for working CXX compiler: /usr/bin/g++
==> precise64: -- Check for working CXX compiler: /usr/bin/g++ -- works
==> precise64: -- Detecting CXX compiler ABI info
==> precise64: -- Detecting CXX compiler ABI info - done
==> precise64: -- Detecting CXX compile features
==> precise64: -- Detecting CXX compile features - done
==> precise64: -- Configuring done
==> precise64: -- Generating done
==> precise64: -- Build files have been written to: /tmp/tmp.mxfYnIAfbm
==> precise64: Scanning dependencies of target HelloWorld
==> precise64: [ 50%] Building CXX object CMakeFiles/HelloWorld.dir/main.cpp.o
==> precise64: [100%] Linking CXX executable HelloWorld
==> precise64: [100%] Built target HelloWorld
==> precise64: Hello, World, line 1 !
==> precise64: Hello, World, line 2 !

==> trusty64: Running provisioner: code (shell)...
    trusty64: Running: inline script
==> trusty64: /tmp/tmp.ACKLPCta7b ~
==> trusty64: -- The C compiler identification is GNU 5.1.0
==> trusty64: -- The CXX compiler identification is GNU 5.1.0
==> trusty64: -- Check for working C compiler: /usr/bin/cc
==> trusty64: -- Check for working C compiler: /usr/bin/cc -- works
==> trusty64: -- Detecting C compiler ABI info
==> trusty64: -- Detecting C compiler ABI info - done
==> trusty64: -- Detecting C compile features
==> trusty64: -- Detecting C compile features - done
==> trusty64: -- Check for working CXX compiler: /usr/bin/g++
==> trusty64: -- Check for working CXX compiler: /usr/bin/g++ -- works
==> trusty64: -- Detecting CXX compiler ABI info
==> trusty64: -- Detecting CXX compiler ABI info - done
==> trusty64: -- Detecting CXX compile features
==> trusty64: -- Detecting CXX compile features - done
==> trusty64: -- Configuring done
==> trusty64: -- Generating done
==> trusty64: -- Build files have been written to: /tmp/tmp.ACKLPCta7b
==> trusty64: Scanning dependencies of target HelloWorld
==> trusty64: [ 50%] Building CXX object CMakeFiles/HelloWorld.dir/main.cpp.o
==> trusty64: [100%] Linking CXX executable HelloWorld
==> trusty64: [100%] Built target HelloWorld
==> trusty64: Hello, World, line 1 !
==> trusty64: Hello, World, line 2 !

==> vivid64: Running provisioner: code (shell)...
    vivid64: Running: inline script
==> vivid64: /tmp/tmp.xPA6mRmD3G ~
==> vivid64: -- The C compiler identification is GNU 5.1.1
==> vivid64: -- The CXX compiler identification is GNU 5.1.1
==> vivid64: -- Check for working C compiler: /usr/bin/cc
==> vivid64: -- Check for working C compiler: /usr/bin/cc -- works
==> vivid64: -- Detecting C compiler ABI info
==> vivid64: -- Detecting C compiler ABI info - done
==> vivid64: -- Detecting C compile features
==> vivid64: -- Detecting C compile features - done
==> vivid64: -- Check for working CXX compiler: /usr/bin/g++
==> vivid64: -- Check for working CXX compiler: /usr/bin/g++ -- works
==> vivid64: -- Detecting CXX compiler ABI info
==> vivid64: -- Detecting CXX compiler ABI info - done
==> vivid64: -- Detecting CXX compile features
==> vivid64: -- Detecting CXX compile features - done
==> vivid64: -- Configuring done
==> vivid64: -- Generating done
==> vivid64: -- Build files have been written to: /tmp/tmp.xPA6mRmD3G
==> vivid64: Scanning dependencies of target HelloWorld
==> vivid64: [ 50%] Building CXX object CMakeFiles/HelloWorld.dir/main.cpp.o
==> vivid64: [100%] Linking CXX executable HelloWorld
==> vivid64: [100%] Built target HelloWorld
==> vivid64: Hello, World, line 1 !
==> vivid64: Hello, World, line 2 !
$ 
```
### ChangeLog

Added more OS

### TODO
