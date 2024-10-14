# Frequently asked questions
&copy; Dr. Richard D. Zinck




## Which microphone to use ?
It really depends on a persons preferences and requirements. For me, I want an inexpensive mic that can record bats and birds. The bats in my area can go up to maybe 130kHz so that should be detectable in the upper end. I want to run it 24/7 and need a protective casing.

At this time my favorite is the Audiomoth v1.2 in USB version. The Wildlife acoustics models struggle more with the background noise from the electric surroundings. The audiomoth is noisier, but kind of covers that type of electrical background noise up with its own noise. It works well for detecting the local bats as well as birds. Also, it comes with a good protective casing and I can buy almost two for the price of one EMT 2.

I do enjoy the EMT 2 models, however, yet for a different purpose. I like to use them on the go with my android phone. I have the phone with me anyway to adding an EMT 2 allows me to ID bats on the go/spontaneously. Great for that together with their app.

The EMT 2 pro has significantly less noise than the audiomoth or regular EMT 2. If you want to have clear recordings this would be the go to. It also records the noises made by the Pi, transformer etc well. So you will have to filter out this electrical background noise in some way. or they will be prominent in the recordings.

The pro makes sense if you require low noise to signal ratio and a good resolution at the upper end of a call around say 180kHz to differentiate e.g. between Myotis species or if you record horsehoe bats. That would be the case if you do a professional survey or live close to a horsehoe bat population. Other users will not have a large benefit from the added 'pro' capabilities.

So at this time I use the audiomoth v1.2 usb with casing for the BattyBirdNET-Pi, the EMT 2 on hikes for spontaneous ID of bats and the EMT 2 pro if I need to make the best possible recordings e.g. for the machine learning data set or to ID a tricky bat species. The audiomoth v1.2 with the battery pack and that casing is great to leave it for three days/nights at a place and the check the recordings for bats with e.g the BattyBirdNET-Analyzer.

There are likely more options from e.g. dodotronic that you could check out, or the PiPipistrelle which you can solder yourself.


## Which Raspberry Pi to use ?

The Pi 5 with 4 or 8GB is more powerful and would be my general recommendation. This performance is noticeable when running the system at 384kHz sampling rate as well as in snappier UX responses.

The Pi 4 with 4 or 8GB runs well also however. It can does not require an active cooler (fan) and hence might be a better choice in circumstances where that is important. It can get stuck/on a delay once in a while if run at 384kHz sampling rate if there are many calls recorded. This has not occurred for me if run with e.g. 256kHz. 

Pis with less than 4Gb memory will run into trouble. I have not tested with Pi 3s. That might work as long as there is enough memory (4GB+).


## Where are the log files ?
You can check logs with
```sh
journalctl -eu birdnet_analysis -u birdnet_server -u batnet_server | sudo tee -a /var/log/syslog
cat /var/log/syslog  | grep error
/usr/local/bin/print_diagnostic_info.sh
```
The installation log is in the file  'installation-$(date +%F).txt'.

## Can I run my own classifier ?
Yes, as long as it is made with [BattyBirdNET-Analyzer](https://github.com/rdz-oss/BattyBirdNET-Analyzer). Check for instructions on that page.

The default option for integration of your bespoke classifier is via the file manager ('Tools'-'Filemanager'). Navigate to
BattyBirdNET-Analyzer/checkpoints/bats/v1.0/ and replace the CUSTOM-BAT-256kHz.tflite and CUSTOM-BAT-256kHz_Labels.txt with those
of your own classifier. They need to be called the same to be found by the system later, so make sure the files of your classifier are named 
CUSTOM-BAT-256kHz.tflite and CUSTOM-BAT-256kHz_Labels.txt as well! For a bird classifier, replace the corresponding 'BIRD' versions.

Next, set the Bat or Bird classifier to use it by settings 'Tools - Settings - Advanced Settings - Bat Classifier Settings - Bat Classifier - CUSTOM_BAT or CUSTOM_BIRD'.
Now, the system will be using your bespoke (fine tuned bird or transfer learned bat) classifier!

## Network settings

You can change the settings in a shell via the command sudo raspi-config. You can edit the files as root (use sudo) directly under /etc/NetworkManager/system-connections .

## How can I contribute ?
Collaborators are very welcome! Write about that in the github form, branch the repository and when ready make a pull request.
