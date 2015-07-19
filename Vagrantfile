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
  [ "${l_pkg_to_install}" ] && sudo apt-get install -y $l_pkg_to_install || return 0
}

pushd /vagrant
#base packages
f_apt_get curl wget htop

SCRIPT

$toolchain=<<SCRIPT
pushd /vagrant
#for c++11 we need g++-4.8
sudo apt-get install -y software-properties-common python-software-properties
sudo add-apt-repository ppa:ubuntu-toolchain-r/test 2>/dev/null
sudo apt-get update
sudo apt-get install -y gcc-4.8 g++-4.8

#remove default gcc alternative, add 4.8
sudo update-alternatives --remove-all gcc 2>/dev/null
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 40 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8

#cmake-3.2
if [ -d cmake-3.2.3-Linux-x86_64 ]; then
  echo "cmake found"
else
  [ -f cmake-3.2.3-Linux-x86_64.sh ] || curl -o cmake-3.2.3-Linux-x86_64.sh http://www.cmake.org/files/v3.2/cmake-3.2.3-Linux-x86_64.sh
  sh cmake-3.2.3-Linux-x86_64.sh --skip-license --include-subdir
fi

SCRIPT

$code=<<SCRIPT
TEMPDIR="`mktemp -d`"
[ -d $TEMPDIR ] || exit 1
cp /vagrant/CMakeLists.txt /vagrant/main.cpp $TEMPDIR
pushd $TEMPDIR
/vagrant/cmake-3.2.3-Linux-x86_64/bin/cmake .
make
./HelloWorld
popd
[ -d $TEMPDIR ] && rm -fr $TEMPDIR

SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.provision "shell", inline: $base
  config.vm.provision "shell", inline: $toolchain
  config.vm.provision "code", type: "shell", privileged: false, inline: $code
end
