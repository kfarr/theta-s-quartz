# CamTwist Effect Plugin to Convert Theta-S Live Video from Fisheye to Equirectangular via Quartz
An experiment to use OS X Quartz Composer to transform Ricoh Theta S live feed dual fisheye to equirectangular.

# Deprecated
JUN 2016: Ricoh has since released native OS drivers to accomplish this: https://theta360.com/en/support/download/

Goal is to create a Quartz composition that can be used in camtwist or other live video streaming software to adjust live the output of the theta-s to be suitable for using in a 360' web panorama plugin. The flow will be something like this:
* Theta S via USB or HDMI > Computer
* Computer to use this Quartz composition from within Camtwist > Media encoder > HLS (via cloud encoding service) > web front-end
* Web front-end needs equirectangular image, see this example: https://aframe.io/examples/showcase/sky/

## Current state - Proof of concept works
* theta-fish2sphere.qtz - this "routes" camtwist through Paul Bourke's custom quartz patch project (see references below)
* @kosso modified version added : theta-fish2sphere_K.qtz with reference images to play with. 
* @justibro modified version with blended edges added : theta-fish2sphere_blending.qtz

### Reference Input Image

<img src="https://github.com/kosso/theta-s-quartz/blob/master/THETAS_DUALFISH_REF_1280_720.png?raw=true" alt="Reference Input Image" />

### Test Output Snapshot

<img src="https://github.com/kosso/theta-s-quartz/blob/master/OUTPUT.png?raw=true" alt="Example Output Image .. so far" />


### Example images: 
* Sample input file (raw dual fisheye from theta-s): https://github.com/kfarr/theta-s-quartz/blob/master/theta-s-raw-Frame-01-03-2016-02-00-34.jpg
* Example of desired output (this is post-processed by theta-s software, but not available for live streaming): https://github.com/kfarr/theta-s-quartz/blob/master/desired-output-R0010093.jpg

## To use:
* Download camtwist http://camtwiststudio.com/, install to applications
* Add theta-fish2sphere.qtz (or other qtz files you want to try) to Applications > CamTwist > Effects
* Open CamTwist
* Step 1: View > Main Window, Double click "Webcam" and choose RICOH THETA S
* Step 2: Choose filter theta-fish2sphere
* Step 3: Modify settings if you'd like, not sure it'll make much of a difference yet. Make sure to press enter after you enter new values.

## How to modify:
* Download quartz composer from Apple's developer site http://developer.apple.com/downloads by searching for "Graphics Tools for Xcode"
* Open theta-fish2sphere.qtz file in quartz composer
* Change input image source to theta s on USB or HDMI input live stream, or use sample image from this git project's root dir

## Dev notes for Quartz Composer
* For testing / developing in QC, you'll need to unhook the "Image (Required)" patch and use instead the image patch "image-example of 720p theta-s stream"
* Ideally in QC during dev one could use video input patch to use as reference for modifying settings, but it is not consistent with behavior when ran inside of camtwist

## Some helpful docs
* Paul Bourke - Converting a fisheye image into a panoramic or perspective projection - http://paulbourke.net/dome/fish2/
* Another attempt using opencv instead of quartz: https://github.com/kscottz/dewarp/blob/master/fisheye/defish.py
* Another attempt use processing.org PDE: https://github.com/theta360developers/THETA-S-LiveViewer-P5
* Another nice blog post: http://www.kscottz.com/fish-eye-lens-dewarping-and-panorama-stiching/
* Theta-S camera: https://theta360.com/en/about/theta/s.html
