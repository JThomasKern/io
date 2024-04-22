# Kalliope requirements Updated for Debian Bullseye

Originally for Kalliope requirements for Debian Jessie/Stretch

## Debian packages requirements

Edit `/etc/apt/sources.list` and check that you have `contrib` and `non-free` are enabled:

Install some required system libraries and softwares:
Note: I've broken these down into subsections to make it easier to identify broken ones.

```bash
sudo apt update
sudo apt install -y git python3-dev libpython3-dev libsmpeg0 libttspico-utils flac \
sudo apt install -y libffi-dev libssl-dev portaudio19-dev build-essential \
sudo apt install -y libatlas3-base mplayer wget vim sudo locales \
sudo apt install -y pulseaudio-utils libasound2-plugins python3-pyaudio libasound-dev \
sudo apt install -y libportaudio2 libportaudiocpp0 ffmpeg
```

Let's install the last release of python-pip (this may be incorrect)
```bash
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
```

Then, with pip, the last release of setuptools
```bash
sudo pip3 install -U setuptools
```
## Kalliope installation

{!installation/manual_installation_common.md!}

{!installation/check_env.md!}
