BootStrap: shub
From: mafreitas/singularity-openms:contrib

%environment
PATH=/usr/local/openms_thirdparty/All/:$PATH
PATH=/usr/local/openms_thirdparty/All/LuciPHOr2:$PATH
PATH=/usr/local/openms_thirdparty/All/MSGFPlus:$PATH
PATH=/usr/local/openms_thirdparty/All/Sirius:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Comet:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Fido:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/MyriMatch:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/OMSSA:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Percolator:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/Sirius:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/SpectraST:$PATH
PATH=/usr/local/openms_thirdparty/Linux/64bit/XTandem:$PATH
PATH=/usr/local/bin/:$PATH
LD_LIBRARY_PATH=/usr/local/lib/:$LD_LIBRARY_PATH

%post
cd $HOME
git clone https://github.com/OpenMS/OpenMS.git
cd OpenMS
git checkout tags/Release2.3.0
hash=`git log | head -n 1 | cut -f 2 -d ' '`
sed -i "s/OPENMS_GIT_SHA1/\"$hash\"/" src/openms/source/CONCEPT/VersionInfo.cpp
rm -rf .git/ share/OpenMS/examples/

cd /usr/local/

git clone https://github.com/OpenMS/THIRDPARTY.git openms_thirdparty
cd openms_thirdparty
rm -rf .git Windows MacOS Linux/32bit

cd $HOME
mkdir openms-build
cd openms-build

cmake -DCMAKE_PREFIX_PATH="$HOME/contrib-build/;/usr/;/usr/local" \
        -DCMAKE_INSTALL_PREFIX=/usr/local/ \
        -DBOOST_USE_STATIC=OFF \
        -DHAS_XSERVER=Off ../OpenMS
make TOPP -j6
make UTILS -j6
make install -j6
rm -rf src doc CMakeFiles

cd $HOME
rm -rf contrib contrib-build openms-build
