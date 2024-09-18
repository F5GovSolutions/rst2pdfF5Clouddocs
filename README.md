# rst2pdfF5Clouddocs

This repo is just this doc detailing how to take F5 Clouddocs guides and turn them into a pdf for situations such as closed networks

This guide details instructions for Ubuntu, it should be similar to other distros if not very close for apt based distros

This will install the rst2pdf command, this requires internet access.
Commands to be executed in bold.

Ensure python3 and pip3 (python package installer) are installed

**sudoapt-get update
**sudo apt-get upgrade
sudo apt-get install
sudo apt-get install python3
sudo apt-get install python3-pip
sudo apt-get install git



**sudo pip3 install rst2pdf[aafiguresupport,mathsupport,plantumlsupport,rawhtmlsupport,sphinx,svgsupport]****
pip3 install f5_sphinx_theme
pip3 install sphinxcontrib-blockdiag
pip3 install sphinx-copybutton
pip3 install sphinxcontrib-nwdiag
https://clouddocs.f5.com/training/community/rseries-training/html/#planning-for-rseries-guide
Find the appropriate repo here
https://github.com/f5devcentral/

git clone https://github.com/f5devcentral/f5-rseries-training
sphinx-build -b pdf f5-rseries-training/docs/  build/pdf
