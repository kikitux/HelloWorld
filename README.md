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

At this moment, this is hardcoded to run `./HelloWorld`

First run, do `vagrant up`

After code modification, you can trigger a new run with:

`vagrant provision --provision-with code`

ie:

```bash
$ vagrant provision --provision-with code
==> default: Running provisioner: code (shell)...
    default: Running: inline script
==> default: /tmp/tmp.MqdaCR6715 ~
==> default: -- The C compiler identification is GNU 4.8.1
==> default: -- The CXX compiler identification is GNU 4.8.1
==> default: -- Check for working C compiler: /usr/bin/cc
==> default: -- Check for working C compiler: /usr/bin/cc -- works
==> default: -- Detecting C compiler ABI info
==> default: -- Detecting C compiler ABI info - done
==> default: -- Detecting C compile features
==> default: -- Detecting C compile features - done
==> default: -- Check for working CXX compiler: /usr/bin/c++
==> default: -- Check for working CXX compiler: /usr/bin/c++ -- works
==> default: -- Detecting CXX compiler ABI info
==> default: -- Detecting CXX compiler ABI info - done
==> default: -- Detecting CXX compile features
==> default: -- Detecting CXX compile features - done
==> default: -- Configuring done
==> default: -- Generating done
==> default: -- Build files have been written to: /tmp/tmp.MqdaCR6715
==> default: Scanning dependencies of target HelloWorld
==> default: [100%] 
==> default: Building CXX object CMakeFiles/HelloWorld.dir/main.cpp.o
==> default: Linking CXX executable HelloWorld
==> default: [100%] 
==> default: Built target HelloWorld
==> default: Hello, World, line 1 !
==> default: Hello, World, line 2 !
==> default: ~
$
```

### TODO

Use `docker` to run the code in multiple machines
