$script=<<SCRIPT
pushd /vagrant
sudo apt-get update
for x in curl wget htop ; do
  which $x 2>/dev/null || sudo apt-get install -y $x
done

[ -f cmake-3.2.3-Linux-x86_64.sh ] || curl -O cmake-3.2.3-Linux-x86_64.sh http://www.cmake.org/files/v3.2/cmake-3.2.3-Linux-x86_64.sh

if [ -d cmake-3.2.3-Linux-x86_64 ]; then
  echo "cmake found"
else
  sh cmake-3.2.3-Linux-x86_64.sh --skip-license --include-subdir
fi

SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"
end
