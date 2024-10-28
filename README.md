# Binary files of LV2 plugins for  Zynthian oram version
## Surge XT Installation Notes
During `cmake --build` reported that it was missing the `.Surge XT` directory
So I ended up creating it manually. I don't think it's the right way and correct directory.
```
mkdir /root/.Surge\_XT
```
They write on github that there is an error when compiling on Raspberry. I quote:
> "We found Surge XT compiles cleanly with gcc (Debian 10.2.1-6) 10.2.1 20210110, but not with others. Surge XT also compiles with Clang 11. "

I installed `clang` right away
```
sudo apt install clang
```
The rest was a sequence of commands:
```
mkdir src
cd /root/src
git clone https://github.com/surge-synthesizer/surge.git
cd surge
git submodule update --init --recursive
cmake -Bignore/s13clang -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DSURGE_BUILD_LV2=TRUE -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr
cmake --build ignore/s13clang --config Release --parallel 3
sudo cmake --install ignore/s13clang
```

Where the files were subsequently located can be read from the [src/Surge XT/install.log](https://github.com/ToFFmashines/binary_for_zynthian/blob/main/src/Surge%20XT/install.log).

I also added preset factors. You can find them in the file [surge-factory-presets.zip 19 MB](https://github.com/ToFFmashines/binary_for_zynthian/blob/main/src/Surge%20XT/surge-factory-presets.zip)

![Screenshot of GUI with Surge XT About.. screen](surge_xt_gui_01.png)

## GeonKick Installation Notes

First the dependencies, I removed `libjack-dev` and `libsndfile-dev` from the recommended ones (becouse Zynthian that have):
```
apt-get install build-essential cmake rapidjson-dev lv2-dev libcairo2-dev
```
Clone the Geonkick code repository:
```
cd /root/src
git clone https://github.com/Geonkick-Synthesizer/geonkick.git
cd geonkick
git submodule update --init --recursive
```
Compile and install:
```
mkdir geonkick/build
cd geonkick/build
cmake ../
make
make install
```
The final binaries are in [src/GeonKick/lv2](https://github.com/ToFFmashines/binary_for_zynthian/tree/a3f04e10c481957ee0a4e2d1f868623f21f52631/src/GeonKick/lv2) for older Zynthian OS.

New version GeonKick 3.5 (16.10.2024) are in [src/GeonKick-3.5](src/GeonKick-3.5) for Zynthian OS Oram. This files are instaled on Zynthian in /usr/local/lib/lv2/geonkick.lv2/ directory. Preset are instaled in to /usr/local/share/geonkick/presets/.

Remark for Linux compilation - library lv2-dev/stable,now 1.18.4-2 amd64 LV2 audio plugin specification - is working. The library lv2-dev from kxstudio not work -> https://github.com/Geonkick-Synthesizer/geonkick/issues/1


## avldrums.lv2 - AVLinux Drumkits

The procedure was as follows:
```
git clone https://github.com/x42/avldrums.lv2.git
cd avldrums.lv2
git submodule update --init --recursive
make submodules
make
sudo make install PREFIX=/usr
```
The complete contents of the [build directory are here](https://github.com/ToFFmashines/binary_for_zynthian/tree/1a9a7478aa9769e8bed4a2c8a7f24ee7c060e6fd/src/avldrums.lv2). Plus a [log from the installation](https://github.com/ToFFmashines/binary_for_zynthian/blob/1a9a7478aa9769e8bed4a2c8a7f24ee7c060e6fd/src/avldrums.lv2/install_avldrums.log).

The AV Linux Drumkits is available in Oram-Bookworm-64 bit branch now.
