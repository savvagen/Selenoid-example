# How to run

1. Pull:  ` selenoid ` , ` selenoid_ui ` , ` selenoid/video-recorder ` and ` vnc_browsers/(fierfox, chrome, opera) ` images from docker-hub
2. Run Selenoid containers with command: 
```
docker-compose up -d
```
3. Run and download Configuration Manager using command:
```
curl -s aerokube.com/cm/bash | bash && ./cm selenoid start --vnc
```
4. run your tests.

```
Video recording:
  
  1. video will be recorded to the directoru /opt/selenoid/video (using flag -video-output-dir)
     To apply this you need to comment "- OVERRIDE_VIDEO_OUTPUT_DIR" environment variable.
  2. Uncoment and use environmant variable - OVERRIDE_VIDEO_OUTPUT_DIR   - to recordvideo to specific folder.
  3. Add capability - "enableVideo = true" in your test configuraitions
   
```
Use link: `http://localhost:4444/video/` to watch all recorded video-files. Click on video - to run.

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