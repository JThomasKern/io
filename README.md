# Welcome to Io, the Kalliope for Debian Bullseye

Io is built on Kalliope

To activate Kalliope after installation:
```bash
source venv/bin/activate
```

Check that the service is ok
```
sudo systemctl status kalliope
```

# From the Kalliope README:
## Summary
Create the brain of your assistant by:
attaching an input **signal** (vocal order, scheduled event, MQTT message, GPIO event, etc..) to one or multiple actions called **neurons**.
- [Kalliope Documentation](https://kalliope-project.github.io/kalliope/)
- [Kalliope website](https://kalliope-project.github.io/)
- [Kallioe Neurons Marketplace](https://kalliope-project.github.io/neurons_marketplace.html)

## License
Copyright (c) 2018. All rights reserved. Kalliope is covered by the  GNU GENERAL PUBLIC LICENSE v3.0. Permissions of this strong copyleft license are conditioned on making available complete source code of licensed works and modifications, which include larger works using a licensed work, under the same license. Copyright and license notices must be preserved. Contributors provide an express grant of patent rights. For the full license text see the [LICENSE.md](LICENSE.md) file.


# Install requirements Updated for Debian Bullseye

Originally "Kalliope requirements for Debian Jessie/Stretch"

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

# Install Io

Install the `python-virtualenv` package:
```bash
sudo pip3 install virtualenv
```

Clone the project:
```bash
git clone https://github.com/kalliope-project/kalliope.git
cd kalliope
```

Generate a local python3 virtual environment:
```bash
virtualenv venv -p /usr/bin/python3
```

Activate the local environment:
```bash
source venv/bin/activate
```

Install using pip
```bash
python3 -m pip install .
```

# Test your installation (Updated for Bullseye)

## Check your microphone and speaker configuration

To ensure that you can record your voice, run the following command to capture audio input from your microphone:
```bash
arecord 123.wav
```

Press CTRL-C after capturing a sample of your voice.

Then play the recorded audio file
```bash
mplayer 123.wav
```

Your installation is now complete, let's take a look now to the [getting started documentation](../getting-started.md) to learn how to use Kalliope.

## (Optional) Start Kalliope automatically after a reboot

If you want to start Kalliope automatically:

Place the script bellow in `/etc/systemd/system/kalliope.service`.

Update the path `<my_config_path>` with the path where you've placed your `brain.yml` and `settings.yml`.

Update the `<username>` with a non root user. For example, on Raspbian you can set `pi`.

```bash
[Unit]
Description=Kalliope
After=pulseaudio.service

[Service]
WorkingDirectory=<my_config_path>

Environment='STDOUT=/var/log/kalliope.log'
Environment='STDERR=/var/log/kalliope.err.log'
ExecStart=/bin/bash -c "/usr/local/bin/kalliope start > ${STDOUT} 2> ${STDERR}"
User=<username>

[Install]
WantedBy=multi-user.target
```

E.g
```bash
[Unit]
Description=Kalliope
After=pulseaudio.service

[Service]
WorkingDirectory=/home/pi/my_kalliope_config

Environment='STDOUT=/var/log/kalliope.log'
Environment='STDERR=/var/log/kalliope.err.log'
ExecStart=/bin/bash -c "/usr/local/bin/kalliope start > ${STDOUT} 2> ${STDERR}"
User=pi

[Install]
WantedBy=multi-user.target
```

Create both log files and give rights to you user
```bash
sudo touch /var/log/kalliope.log
sudo touch /var/log/kalliope.err.log
sudo chown pi:pi /var/log/kalliope*
```

Then, reload systemctl, start the service and enable it at startup
```bash
sudo systemctl daemon-reload
sudo systemctl start kalliope
sudo systemctl enable kalliope
```

Check that the service is ok
```
sudo systemctl status kalliope
```
