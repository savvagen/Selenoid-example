## Run with Docker

1. Pull Docker images of: ` selenoid ` , ` selenoid_ui ` , ` selenoid/video-recorder ` and ` vnc_browsers/(fierfox, chrome, opera) ` images from docker-hub
2. Run Selenoid and Selenoid-UI with docker-compose: 
```
docker-compose up -d
```

## Run with Configuration Manager
1. Run and download Configuration Manager using command:
```
curl -s aerokube.com/cm/bash | bash && ./cm selenoid start --vnc
```

## Video Recording

```  
  1. Add capability - "enableVideo = true" to enable video recording.
  2. video will be recorded (according to command flag -video-output-dir) into: "/opt/selenoid/video" folder
     To apply this you need to comment "- OVERRIDE_VIDEO_OUTPUT_DIR" environment variable in docker-compose file.
  3. Use additional "OVERRIDE_VIDEO_OUTPUT_DIR" env. variable for video recording to specific folder.
   
```
Use link: `http://localhost:4444/video/` to watch all recorded video-files.

 Java code example(using Selenide):
 ```
 DesiredCapabilities dc = DesiredCapabilities.firefox();
        dc.setBrowserName("chrome");
        dc.setVersion("63.0");
        dc.setCapability("enableVNC", true);
        dc.setCapability("enableVideo", true);
        dc.setCapability("screenResolution", "1960x1280x24");
        dc.setCapability(CapabilityType.TAKES_SCREENSHOT, true);
        //More capabilities:
        // "videoName":"selenoid851e3f5f21e59a0eb5640b9c0c9a702c.mp4",
        // "videoScreenSize":"1960x1280",
        // "videoFrameRate":0,
        // "name":"",
        // "timeZone":""
        dc.setPlatform(Platform.LINUX);
        dc.setJavascriptEnabled(true);
        setWebDriver(new RemoteWebDriver(new URL("http://localhost:4444/wd/hub"), dc));
        getWebDriver().manage().window().setSize(new Dimension(1920, 1080));

```

Links to documentation:
```
http://aerokube.com/selenoid-ui/latest/
http://aerokube.com/cm/latest/
http://aerokube.com/selenoid/latest/
```