How to build and configure a cheap HomeKit enabled camera  
  
You can find a lot of instructions in the internet about how to build and set up a cheap HomeKit enabled camera.  
But for me I found all these were incomplete or faulty.  
So I decided to share my knowledge into this repository.  
The most annoying thing was the stillImage didn't refresh because of wrong configuration.  
The config I'm sharing with you gives a stillImage which refreshes every 10 seconds.  
The following steps presuppose that you have a working HomeKit setup and a running instance of Homebridge.  
In my case my Homebridge instance is running on a RaspberryPi 3b+.  
As HomeKit hub i use an Apple TV 4.  
I will not explain how to set up Homebridge since there are a lot of tutorials in the internet.  
  
All you need is the official RaspberryPi camera modul:  
https://www.amazon.de/LABISTS-Offizielle-Raspberry-V2-0-Kamera-Modul/dp/B07VRJKYYB  
  
How to connect the cam modul to your pi:  
https://projects.raspberrypi.org/en/projects/getting-started-with-picamera  
  
Additionally you can put both the pi and the camera into a case like this: 
https://ameridroid.com/collections/cases/products/smoothcam-raspberry-pi-camera-case-3d-printed-abs  
  
It depends on your Homebridge installation if homebridge-camera-ffmpeg is already installed.  
If it's not installed you should do so:  
https://github.com/KhaosT/homebridge-camera-ffmpeg  

After installation you should edit your config.json.  
In my case the config.json is located under /root/.homebridge/config.json.  
You can edit the file through a ssh connection to your pi.  
Just type ```sudo nano /root/.homebridge/config.json``` into the console or terminal window.  
In the nano editor add the following lines (for more information check the sample.config.json within this repo):  
  
```
{   
  "platform" : "Camera-ffmpeg",  
  "name" : "Homebridge-Camera-Ffmpeg Plugin" 
  "cameras" : [  
    {  
      "name" : "Camera",  
      "motion" : true,  
      "videoConfig" : {  
        "vcodec" : "h264_omx",  
        "source" : "-f v4l2 -r 30 -s 1280x720 -i /dev/video0",  
        "maxFPS" : 15,  
        "maxHeight" : 720,  
        "maxStreams" : 6,  
        "maxWidth" : 1280,  
        "stillImageSource" : "-re -f video4linux2 -ss 0.9 -i /dev/video0 -vframes 1"  
      }  
    }  
  ]   
}
```  

