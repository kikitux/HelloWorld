$script=<<SCRIPT
#!/bin/bash
pushd /vagrant
for x in curl wget htop gcc++ ; do
  which $x 2>/dev/null
  if [ $? -ne 0 ]; then
  if [ ! $isAptUptodate ]; then
    sudo apt-get update
    isAptUptodate="true"
  fi
  sudo apt-get install -y $x
done


if [ -d cmake-3.2.3-Linux-x86_64 ]; then
  echo "cmake found"
else
  [ -f cmake-3.2.3-Linux-x86_64.sh ] || curl -O cmake-3.2.3-Linux-x86_64.sh http://www.cmake.org/files/v3.2/cmake-3.2.3-Linux-x86_64.sh
  sh cmake-3.2.3-Linux-x86_64.sh --skip-license --include-subdir
fi

SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"
end
