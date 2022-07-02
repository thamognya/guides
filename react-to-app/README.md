# Convert react web app to ios and andriod apps

## Resources 

- https://stackoverflow.com/questions/35463547/what-is-the-quickest-way-to-convert-a-react-app-to-react-native


## Steps

- download npm, npx, cordova 

follow the stack overflow answer:

As others have mentioned there's no quick way to convert react to react-native.

A possible alternative if you want your react app to run on a mobile device without rewriting your codebase is to use Cordova.  For fun I ported a react-web app into a mobile app using Cordova in just a few minutes.  There are some drawbacks to this method, but the benefit is that you can have a working mobile app in very little time.

Below are the steps if anyone is interested in a Cordova workaround alternative:

REACT SETUP (done in command line)
````
>1. npx create-react-app my-app
>2. cd my-app
>3. npm start
````
DEPLOY TO STATIC:
````
>1. Update your package.json file from your my-app directory to add "homepage":"." (see below)

  "name": "my-app",
  "version": "0.1.0",
  "private": true,
  "homepage":".",
  "dependencies": {
````
```` 
>2. Build (in command line) npm run build
````
CORDOVA INTEGRATION (in command line)
````
>1.  cd ../ (change to wherever you want the project created, don't do this inside your existing react app folder)
>2.  npm install -g cordova (only if you already don't have Cordova installed)
>3.  cordova create MyApp 
>4.  cd MyApp
>5.  cordova platform add ios //or android or browser
````
ADD A COUPLE STEPS FOR INCLUDING YOUR REACT PROJECT
````
>1. Open your Cordova MyApp www folder, delete all files and folders in it except for the 'js' folder
>2. Back in your react build folder update the index file to add two cordova scripts:
````
````
<script type="text/javascript" src="cordova.js"></script>
<script type="text/javascript" src="js/index.js"></script>
````
````
>3. copy all your files from the react build folder into the Cordova www folder (replacing everything except the js folder)
````
BUILD REACT-CORDOVA APP (in command line, inside your Cordova project)
````
>1. cordova build ios //or android or browser
````
TEST OR DEPLOY TO STORE ETC.
````
>1. Use xcode to open open your react-cordova .xcodeproject, this can be found in the MyApp/Platforms/ios/
>2. Select your simulator and run.  Enjoy your new mobile app!
 
do 

cordova run ios # or andriod
````
TWEAK
There are some minor tweaks you'll need to do (like remove the tap delay...etc) 
-I think this is why people think Cordova apps are slow, but it's an easy fix...



