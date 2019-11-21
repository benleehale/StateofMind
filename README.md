# StateofMind
Stand alone three js renderer for esp32 HEG device. 
## Getting Started
### 1: Add Code to HEG Esp 32
This Repo is designed to work with the HEG Arduino device, whose code you [can find here](https://github.com/moothyknight/HEG_ESP32).
To make the device communicate with State of Mind, you must add one line to the onboard code.
Open webDemo.h in your arduino editor, and go to line 243, where the code is pushing incoming data to its array.

```
        s.AI.push(parseFloat(dataArray[6]));
        g.ms = s.ms;
```

Now paste the line 

```
parent.postMessage( s.ratio[s.ratio.length-1], "*");
```

right after 243, such that the new code looks like

```
        s.AI.push(parseFloat(dataArray[6]));
        parent.postMessage( s.ratio[s.ratio.length-1], "*");
        g.ms = s.ms;
```
After you have flashed this minor change onto the device's onboard code, you're ready to run State of Mind.
### 2: Run Local Webserver
Clone this repo, and cd into that file using your favorite command line.
Run your local webserver of choice, I prefer to use python's stock server.
If you already have python, the command is *python -m http-server*.

### 3: Using State of Mind
Go to http://localhost:8000/SCSA.html
under the tab, connect, enter the URL of your HEG device. This will display the onboard UI for the HEG in an Iframe below. Click on WebDemo, and then click on Start HEG. After you've connected and started your HEG, the data will be fed to our three js renderer under the Play tab. Here you can see your brain activity influence procedurely generated 3d animations! I developed this method so I could create games for the HEG in plain Javascript and Three.js, and then load them within a webapp frame work (such as react or angular.! This is just a demonstration of the method and its performance. 

Enjoy!



