# IScroller

This project consist of two parts:
## 1. IScroller Chrome Extension
This extension is developed using javascript deeplearn.js library. This extension helps the user to scroll the websites using gestures.
###  - Usage
#### - How to install and configure the extension
    1. Install the extension from the Chrome store.
    2 .Upon initial installation, the extension will ask for permission to access the webcam. After granting permission, you can close the welcome page.
    3. Note that the extension keeps your webcam open, but at no point is any information from the webcam ever sent anywhere. All processing happens local to your machine.
    4. Click the Cam Scroller browser action icon next to the address bar. In the popup, you should see a display of what your webcam is   seeing. Click the "Create scrolling gestures" button and follow the on-screen instructions to create your custom scrolling gestures.
    5.You will be asked to train three different poses: one for scrolling down, one for scrolling up, and one for the steady state of not scrolling at all.

From this point on, for any new tab/page you load, scrolling can be controlled by the gestures you trained. You will see a visual scrolling indicator on the right side of the page when scrolling is being controlled by your gestures.

The KNN image classifier weights for the trained gestures are stored in Chrome local storage, so the gestures do not have to be retrained when you close and then relaunch Chrome.

### - Controls available in the extension

If you want to temporarily turn off the Cam Scrolling capability, uncheck the checkbox in the Cam Scroller browser action popup.

If at any time you wish to retrain the gestures, just click the "Create scrolling gestures" button again in the extension popup.
### - Code breakdown

welcome.[html/js] - Page launched on initial extension installation which requests webcam access for the extension.

popup.[html/js] - Browser action popup page. Displays the webcam and has controls for training the scrolling gestures and  enabling/disabling scrolling. Passes messages to the background page to do the actual processing.

background.[html/js] - Contains all the machine learning logic for the extension. Trains the KNN image classifier when in training mode, infers which scrolling gestures are being performed when in inference mode, and sends messages to the content script to perform scrolling.

content.js - Content script running with webpages loaded in Chrome. Calls window.scrollBy to scroll webpages and places visual indicators on the page when scrolling.


## 2. Website Integration
A Flask app is created and integrating the python code with the HTML code we can enable a scroll activity on the basis of gestures. 
Our logic was to first find the farthest point of the fingers i.e their co- ordinates and then check the Y - values of the co-ordinates to determine whether there is scroll up or down activity.
