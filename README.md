# JET PRESENTATION
> A Presentation Rehearsal Partner for Everyone!

Authors: Patara Trirat (patara.t@kaist.ac.kr), Sakonporn Noree (sakonporn.n@kaist.ac.kr)

![](https://i.ibb.co/RgFQvFb/Screen-Shot-2020-07-03-at-20-48-05.png "Jet Presentation")


The Azkaban Prison inspired exterior!

### Showcase Video
<a href="https://www.youtube.com/watch?v=ybabXxc5N_U" target="blank"><img src="http://img.youtube.com/vi/ybabXxc5N_U/0.jpg" 
alt="Jet Presentation: the showcase video" width="640" height="360" border="0" /></a>

### Project Details
<a href="http://tiny.cc/jet-presentation-slides" target="blank"><img src="https://i.ibb.co/QYFVtn5/Screen-Shot-2020-07-03-at-21-26-53.png" alt="Jet Presentation: the slides deck" width="640" height="360" border="0" /></a>

## Prerequisites
### Hardwares
1. Jetson Nano
<img src="https://cdn.sparkfun.com//assets/parts/1/4/9/4/6/16271-NVIDIA_Jetson_Nano_Developer_Kit__V3_-01.jpg" alt="jetson nano" width="200"/>

2. 5 Colored 8mm LEDs with 3-Color Socket Jumper Cable
<img src="https://www.devicemart.co.kr/data/collect_img/kind_0/goods/large/1383859.jpg" alt="colored LED" width="200"/>
<img src="https://www.devicemart.co.kr/data/collect_img/kind_0/goods/large/201103071836420.jpg" alt="cable" width="200"/>

3. Raspberry Pi Camera Module V2, 8MP
<img src="https://www.devicemart.co.kr/data/collect_img/kind_0/goods/large/1077951.jpg" alt="camera" width="200"/>

 
### Softwares (Modules, Frameworks, and Libraries)

#### For Jetson Nano
1. python 3.7
2. firebase-admin 4.3.0
3. requests 2.24
4. google-cloud 0.34.0
5. matplotlib 3.2.2 
6. numpy 1.18

#### For Web Application
1. react.js 16.13 (with create-react-app )
2. ant design 4.4
3. axios 0.19.2
4. html2canvas 1.0.0
5. react-google-charts 3.0.15


### Cloud Services (Optional)
#### For Flask Server
this server is served for image classification
1. pytorch 1.5.1
2. tensorflow 2.2.0
3. auto-keras 1.0.3
4. dlib 19.20.0
5. opencv-python 4.2.0.34
6. pandas 1.0.5
7. numpy 1.18
8. matplotlib 3.2.2 
9. Flask 1.1.2
10. Pillow 7.2.0
11. colour 0.1.5
12. scikit-learn 0.23.1 (use for gesture model training)

#### For Node.js Server (Cloud Functions for Firebase)
this server is served for data manipulation
1. express 4.17.1
2. cors 2.8.5
3. firebase-admin 8.13
4. node 10

***BIG REMARK*** you can simply run all the classification models (eye, face, and gesture) on the Jetson or even store the classified data, if your device's capability is enough.

## Project Structure
* **APIs**
  * **flask**
    * **data** (related data for eye contact detection)
    * *model.py* (static model for eye contact detection model)
    * *gesture_model.h5* (Trained gesture model can be downloaded here: [gesture_model.h5](https://drive.google.com/file/d/1-1GZzEfHPyuaVlE1dfETx991zTMXfeRI/view?usp=sharing))
    * *predictor.py* (main application file for running flask server)
  * **functions** (cloud functions)
    * *firebase.js* (initialize firebase instance for the project)
    * *index.js* (main route for the services)
    * *package.js* (package dependencies)
    * *services.js* (main services file for data manipulation (e.g., update current status and load report data)
* **Jetson Nano**
  * *Data Collection.ipynb* (notebook file for collecting train data set)
  * *eye.py* 
  * *face.py*
  * *gesture.py*
  * *jet-presentation-firebase-adminsdk.json* (firebase admin **service account** key, please use yours.)
  * *main.py* (main application for Jetson Nano receiving current status from the server and making image snapshot from user)

* **Web Application** (can be generated by [create-react-app](https://reactjs.org/docs/create-a-new-react-app.html))
  * **public** (public folder for public resource files *generated by create-react-app*)
  * **src**
    * *App.css* (CSS file for App.js)
    * *App.js* (Main component for the web application)
    * *ConnectButton.js* (Button component)
    * *Report.js* (Report component for the final summary reports)
    * *Status.js* (Connection status component)
    * *index.js* (Main application page for rendering)
    * *utils.js* (Utility functions (e.g., API calls and report generation)
* **datasets** (from 4,680 samples 1,980 samples are provided due to privacy concerns)



## Running the Project!
### If you are using cloud services (optional), please make sure...
1. Get your **subscription key**  from Microsoft Azure service *AND* Get your **service account key** from firebase service.
2. Run your flask server ([see](https://docs.microsoft.com/en-us/azure-stack/user/azure-stack-dev-start-howto-vm-python?view=azs-2002)) and deploy your firebase functions ([see](https://firebase.google.com/docs/functions/get-started)).
3. Update your `base_url` variable value in `eye.py` and `gesture.py` to your path.
4. Update your service url of the API call function in `utils.js` to your path.
 
### Main Application (Jetson Nano)
1. Locate your current directory to **Jetson Nano** directory.
2. Run `python3 main.py` in your terminal.
3. Wait for the connection status.


### Main Application (Web Application)
1. Locate your current directory to **Web Application** directory.
2. Run `yarn install` or `npm install` to install all dependencies.
3. Run `yarn start` or `npm start` to make your web available on your **localhost:3000**. or run `yarn build` to make the build files and resources then upload them into your own server or cloud services.
