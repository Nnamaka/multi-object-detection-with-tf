# Multi-Object-Detection-with-tf(Tensorflow)
A walk through of multi object detection with the Tensorflow object detection API on colab

<div>
 <span align="left">
  <img width="600" heigt="300" src="https://github.com/Nnamaka/multi-object-detection-with-tf/blob/main/catdog.png">
</span>

 For this project, I will be detecting hand gestures for <b>'livelong'</b>, <b>'thumbsup</b>', <b>'thumbsdown'</b>, <b>'thankyou'</b>.
 Prior to the beginning this project, I had collected and preannoted my image dataset. 
 I used the <a href="https://github.com/tzutalin/labelImg">labellimg</a> tool to label and annotate my images.
 My images were saved in the pascalVOC format which is an acceptable format for object detection when using the TFOD API.

 
 
 # LabelImg
 <p align="center">
  <img src="https://github.com/Nnamaka/multi-object-detection-with-tf/blob/main/annotate%20(2).gif">
</p>

 
 
 ## Steps
 <b>Step 1.</b>
 Install <a href="https://github.com/tzutalin/labelImg">labellimg</a> for annotating your image datatset in the pascalVOC format
 <pre>
 pip3 install labelImg
 </pre>
