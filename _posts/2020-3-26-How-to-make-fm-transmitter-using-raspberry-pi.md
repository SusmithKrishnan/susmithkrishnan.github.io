---
title: 'How to make a FM transmitter using RaspberryPI'
date: 2020-3-26
permalink: /posts/2016/9/fm-transmitter-using-raspberry-pi/
tags:
  - hardware
  - raspberrypi
---

Raspberry PI's have built in EMI supression functionality for reducing external noise using *Spread Spectrum Clock Signal* (**SSCS**). This signal can be modulated and used as FM transmitter. The frequency range is between 1MHz - 250Mhz and emitted on GPIO pin 4.

Hook a jumper wire or external antenna to GPIO pin 4. That is the only hardware requirement.

shell in to raspberry pi using ssh or direct terminal. 
1. Donload compiling tools and dependencies
```
sudo apt-get install gcc g++ make 
```
2. Dwonlad FM Transmitter program from github
```
sudo git clone https://github.com/markondej/fm_transmitter
```
3. Compile
```
cd fm_transmitter  && make
```
4. Broadcast audio
```
sudo ./fm_transmitter -f 100  -r your_audio.wav
```

Usage format:
    ```sudo ./fm_transmitter -f frequency -r filename```


Where:
* -f frequency - Specifies the frequency in MHz, 100.0 by default if not passed
* acoustic_guitar_duet.wav - Sample WAV file, you can use your own

Other options:
* -d dma_channel - Specifies the DMA channel to be used (0 by default), type 255 to disable DMA transfer, CPU will be used instead
* -b bandwidth - Specifies the bandwidth in kHz, 100 by default
* -r - Loops the playback

After transmission has begun, simply tune an FM receiver to chosen frequency, You should hear the playback.
### Supported audio formats
You can transmitt uncompressed WAV (.wav) files directly or read audio data from stdin, eg.:
```
sudo apt-get install sox
sox star_wars.wav -r 22050 -c 1 -b 16 -t wav - | sudo ./fm_transmitter -f 100.6 -
```
Please note only uncompressed WAV files are supported. If you receive the "corrupted data" error try converting the file, eg. by using SoX:
```
sudo apt-get install sox libsox-fmt-mp3
sox my-audio.mp3 -r 22050 -c 1 -b 16 -t wav my-converted-audio.wav
sudo ./fm_transmitter -f 100.6 my-converted-audio.wav
```
### Microphone support
In order to use a microphone live input use the `arecord` command, eg.:
```
arecord -D hw:1,0 -c1 -d 0 -r 22050 -f S16_LE | sudo ./fm_transmitter -f 100.6 -
```
In cases of a performance drop down use ```plughw:1,0``` instead of ```hw:1,0``` like this:
```
arecord -D plughw:1,0 -c1 -d 0 -r 22050 -f S16_LE | sudo ./fm_transmitter -f 100.6 -
```    
Note: Transmitting on certain frequencies might be illegal in your country. Please verify the allowed frequency before proceeding.