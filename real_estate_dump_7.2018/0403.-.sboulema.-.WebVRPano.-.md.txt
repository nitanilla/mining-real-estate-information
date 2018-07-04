# WebVRPano
Using WebVR to look at real estate

# Running the WebVRPano server
    docker run -p 5000:5000 -d sboulema/webvr:latest

# Using WebVRPano
How to use WebVRPano combined with a virtual reality solution

Have a look at the instructions at [WebVR Info](https://webvr.info/) or scroll down for detailed instructions

## Google Cardboard
1. Use Google Chrome and browse to the WebVRPano server
2. Insert TinyId
3. Place phone in Google Cardboard

## Samsung Gear VR (Google Chrome)
1. Use [Gear VR Cardboard](https://play.google.com/store/apps/details?id=com.bartslab.gearvrcardboard) to switch to developer mode and disable the Gear VR Service
2. Use Google Chrome and browse to the WebVRPano server
3. Insert TinyId
4. Place phone in Samsung Gear VR

## Samung Gear VR (Samsung Internet)
1. Place phone in Samsung Gear VR
2. Use Samsung Internet and browse to `internet://webvr-enable`
3. Browse to the WebVRPano server
4. Insert TinyId

## Oculus Rift (DK2)
1. Install [Oculus Home](https://www3.oculus.com/en-us/setup/)
2. Ignore any incompatibility [warnings](https://forums.oculus.com/developer/discussion/33228/dk2-setup-on-windows-10#latest)
3. Install [Chromium WebVR](https://webvr.info/get-chrome/)
4. Enable the Chromium WebVR flag by browsing to `chrome://flags/#enable-webvr`
5. Browse to the WebVRPano server
6. Insert TinyId