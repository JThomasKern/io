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