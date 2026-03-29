Android Auto for Raspberry Pi Zero 2W

C++ implementation of Android Auto on RPiZero2W that can run on low current wirelessly and with autostart.

!!!This is not available for ditribution yet. Code parts and other small details are missing - this is why is not posted on GitHub!!!

The requirement for this project is to have a Carlinkit dongle: CPC200 - CCPA Mic

Commands used:

sudo apt install build-essential xxd libsdl2-dev libsdl2-ttf-dev libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libusb-1.0-0-dev libssl-dev

sudo apt install ffmpeg libsdl2-2.0-0 libsdl2-ttf-2.0-0 libusb-1.0-0 libssl3

lsusb #for usb permission

Search for it: Bus 001 Device 053: ID 1314:1521 Magic Communication Tec. Auto Box

echo 'SUBSYSTEMS=="usb", ATTRS{idVendor}=="1314", ATTRS{idProduct}=="1521", GROUP="plugdev", MODE="0660"' | sudo tee /etc/udev/rules.d/50-carlinkit.rules

make clean
make release
mkdir ./conf
cp ./settings.txt ./conf
./out/app ./conf/settings.txt #move the file for easier settings and troubleshooting - remember to remove "#" wherever is necessasry to do so

[Unit]
Description=FastCarPlay Autostart
After=network.target sound.target graphical.target

[Service]
ExecStart=/home/adminadmin/Desktop/FastCarPlay-main/out/app /home/adminadmin/Desktop/FastCarPlay-main/conf/settings.txt
WorkingDirectory=/home/adminadmin/Desktop/FastCarPlay-main
StandardOutput=journal
StandardError=journal
Restart=on-failure
User=adminadmin
Environment=DISPLAY=:0

[Install]
WantedBy=default.target

other settings and scripts to lower the power consumtion and optimisations.

ref: https://github.com/harrylepotter/carplay-receiver
