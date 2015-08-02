$base=<<SCRIPT
#!/bin/bash

f_apt_get(){
  for x in $@ ; do
    which $x 2>/dev/null
    if [ $? -ne 0 ]; then
      if [ ! $isAptUptodate ]; then
        sudo apt-get update
        isAptUptodate="true"
      fi
      l_pkg_to_install="$x $l_pkg_to_install"
    fi
  done
  if [ "${l_pkg_to_install}" ] ; then
    [ -f /vagrant/proxy.env ] && source /vagrant/proxy.env
    sudo apt-get install -y $l_pkg_to_install
  else
    return 0
  fi
}

#base packages
f_apt_get curl wget htop
SCRIPT

$toolchain48=<<SCRIPT
  which g++-4.8 gcc-4.8 g++ gcc make 2>/dev/null
  if [ $? -ne 0 ]; then
    [ -f /vagrant/proxy.env ] && source /vagrant/proxy.env
    #for c++11 we need g++-4.8
    sudo apt-get install -y software-properties-common python-software-properties
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test 2>/dev/null
    sudo apt-get update
    sudo apt-get install -y gcc-4.8 g++-4.8 make
    #remove default gcc alternative, add 4.8
    sudo update-alternatives --remove-all gcc 2>/dev/null
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 40 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8
    hash -r
  fi
SCRIPT

$toolchain5=<<SCRIPT
  which g++-5 gcc-5 g++ gcc make 2>/dev/null
  if [ $? -ne 0 ]; then
    [ -f /vagrant/proxy.env ] && source /vagrant/proxy.env
    sudo apt-get install -y software-properties-common python-software-properties
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test 2>/dev/null
    sudo apt-get update
    sudo apt-get install -y gcc-5 g++-5 make
    #remove default gcc alternative
    sudo update-alternatives --remove-all gcc 2>/dev/null
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 40 --slave /usr/bin/g++ g++ /usr/bin/g++-5
    hash -r
  fi
SCRIPT

$cmake=<<SCRIPT
  #cmake-3.3
  CMAKE="cmake-3.3.0-Linux-x86_64"
  pushd /usr/local
  if [ -d $CMAKE ]; then
    echo "cmake found"
  else
    [ -f /vagrant/proxy.env ] && source /vagrant/proxy.env
    [ -f /vagrant/$CMAKE.sh ] || curl -o /vagrant/$CMAKE.sh http://www.cmake.org/files/v3.3/$CMAKE.sh
    sh /vagrant/$CMAKE.sh --skip-license --include-subdir
  fi
SCRIPT

$code=<<SCRIPT
  #cmake-3.3
  CMAKE="cmake-3.3.0-Linux-x86_64"
  #[ -f /vagrant/proxy.env ] && source /vagrant/proxy.env
  TEMPDIR="`mktemp -d`"
  [ -d $TEMPDIR ] || exit 1
  cp /vagrant/CMakeLists.txt /vagrant/main.cpp $TEMPDIR
  pushd $TEMPDIR
  /usr/local/$CMAKE/bin/cmake .
  make
  FILE="`find . -maxdepth 1 -type f -perm -001`"
  $FILE
  echo $?
  popd
  [ -d $TEMPDIR ] && rm -fr $TEMPDIR
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.provision "shell", inline: $base
  config.vm.provision "shell", inline: $cmake
  config.vm.define "precise64", primary: true do |precise64|
    precise64.vm.box = "hashicorp/precise64"
    precise64.vm.provision "shell", inline: $toolchain48
    precise64.vm.provision "code", type: "shell", privileged: false, inline: $code
  end
  config.vm.define "trusty64", primary: true do |trusty64|
    trusty64.vm.box = "ubuntu/trusty64"
    trusty64.vm.provision "shell", inline: $toolchain5
    trusty64.vm.provision "code", type: "shell", privileged: false, inline: $code
  end
end
