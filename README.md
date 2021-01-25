
# FreeDV-JATE [Just Another TNC Experiment]

## 002_HIGHSNR_PING_PONG

### INSTALL TEST SUITE
#### Install prerequierements
```
sudo apt update
sudo apt upgrade
sudo apt install git cmake build-essential python3-pip portaudio19-dev python3-pyaudio
pip3 install crcengine
pip3 install threading
```

Go into a directory of your choice
Run the following commands --> They will download and compile the latest codec2 ( dr-packet ) files and LPCNet as well into the directory of your choice
```
wget https://raw.githubusercontent.com/DJ2LS/FreeDV-JATE/002_HIGHSNR_PING_PONG/install_test_suite.sh
chmod +x install_test_suite.sh
./install_test_suite.sh
```



### PARAMETERS
| parameter | description | side
|--|--|--|
| - -mode 12 | set the mode for FreeDV ( 10,11,12 ) | TX & RX
| - -delay 1 | set the delay between burst | TX
| - -frames 1 | set the number of frames per burst | TX & RX
| - -bursts 1 | set the number of bursts | TX & RX
| - -input "audio" | if set, program switches to audio instead of stdin | RX
| - -audioinput 2 | set the audio device | RX
| - -output "audio" | if set, program switches to audio instead of stdout | TX
| - -audiooutput 1 | set the audio device | TX
| - -debug | if used, print additional debugging output | RX
  	



### AUDIO TESTS VIA VIRTUAL AUDIO DEVICE

 #### Create audio sinkhole and subdevices
 Note: This command needs to be run again after every reboot
 ```
sudo modprobe snd-aloop index=1,2 enable=1,1 pcm_substreams=1,1 id=CHAT1,CHAT2 
```
check if devices have been created



    aplay -l
Output should be like this:


    Karte 0: Intel [HDA Intel], Gerät 0: Generic Analog [Generic Analog]
      Sub-Geräte: 1/1
      Sub-Gerät #0: subdevice #0
    Karte 1: CHAT1 [Loopback], Gerät 0: Loopback PCM [Loopback PCM]
      Sub-Geräte: 1/1
      Sub-Gerät #0: subdevice #0
    Karte 1: CHAT1 [Loopback], Gerät 1: Loopback PCM [Loopback PCM]
      Sub-Geräte: 1/1
      Sub-Gerät #0: subdevice #0
    Karte 2: CHAT2 [Loopback], Gerät 0: Loopback PCM [Loopback PCM]
      Sub-Geräte: 1/1
      Sub-Gerät #0: subdevice #0
    Karte 2: CHAT2 [Loopback], Gerät 1: Loopback PCM [Loopback PCM]
      Sub-Geräte: 1/1
      Sub-Gerät #0: subdevice #0

#### Run tests:
tbc

##### PING side

    python3 PING.py --mode 12 --audioinput 1 --audiooutput 1 --frames 10 --bursts 1
    
##### TX side

    python3 PONG.py --mode 12 --audioinput 2 --audiooutput 2


