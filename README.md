# homebridge-raspberry-camera-modul
How to build and configure a cheap HomeKit enabled camera  

You can find a lot of instructions in the internet about how to build and set up a cheap HomeKit enabled camera.  
But for me I found all these were incomplete or faulty.  
So I decided to share my knowledge into this repository.  
The following steps presuppose that you have a working HomeKit setup and a running instance of Homebridge.  
In my case my Homebridge instance is running on a RaspberryPi 3b+.  
As HomeKit hub i use an Apple TV 4.  
I will not explain how to set up Homebridge since there are a lot of tutorials in the internet.  

All you need is the official RaspberryPi camera modul.  
Connect the cam modul to your pi.  
It depends on your Homebridge installation if homebridge-camera-ffmpg is already installed.  
If it's installed you should edit your config.json.  
In my case the config.json is located under /root/.homebridge/config.json.  
You can edit the file through a ssh connection to your pi.  
Just type sudo nano /root/.homebridge/config.json into the console or terminal window.  
In the nano editor add the following lines:  

{
  "platform" : "Camera-ffmpeg",
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
  "name" : "Camera Plugin"
}

