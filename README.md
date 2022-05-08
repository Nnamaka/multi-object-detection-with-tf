# Multi-Object-Detection-with-tf(Tensorflow)
A walk through of multi object detection with the Tensorflow object detection API on colab

<i><b>Note</b>: the full code is contained in the jupyter notebook hosted here in this repo</i>
<div>
 <span align="left">
  <img width="600" heigt="300" src="https://github.com/Nnamaka/multi-object-detection-with-tf/blob/main/catdog.png">
</span>

 #
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

 <b>Step 2.</b>
 
 Setup the project folder structure
 <pre>
 paths = {
    'WORKSPACE_PATH': os.path.join('Tensorflow', 'workspace'),
    'SCRIPTS_PATH': os.path.join('Tensorflow','scripts'),
    'APIMODEL_PATH': os.path.join('Tensorflow','models'),
    'ANNOTATION_PATH': os.path.join('Tensorflow', 'workspace','annotations'),
    'IMAGE_PATH': os.path.join('Tensorflow', 'workspace','images'),
    'MODEL_PATH': os.path.join('Tensorflow', 'workspace','models'),
    'PRETRAINED_MODEL_PATH': os.path.join('Tensorflow', 'workspace','pre-trained-models'),
    'CHECKPOINT_PATH': os.path.join('Tensorflow', 'workspace','models',CUSTOM_MODEL_NAME), 
    'OUTPUT_PATH': os.path.join('Tensorflow', 'workspace','models',CUSTOM_MODEL_NAME, 'export'), 
    'TFJS_PATH':os.path.join('Tensorflow', 'workspace','models',CUSTOM_MODEL_NAME, 'tfjsexport'), 
    'TFLITE_PATH':os.path.join('Tensorflow', 'workspace','models',CUSTOM_MODEL_NAME, 'tfliteexport'), 
    'PROTOC_PATH':os.path.join('Tensorflow','protoc')
 }
 </pre>

 
 <b>Step 2.</b>
 
 Download pretrained models from Tensorflow model zoo
 <pre>
 if not os.path.exists(os.path.join(paths['APIMODEL_PATH'], 'research', 'object_detection')):
    !git clone https://github.com/tensorflow/models {paths['APIMODEL_PATH']}
 </pre>
 
 
Install the TFOD API
<pre>
import wget
if os.name=='posix':  
    !apt-get install protobuf-compiler
    !cd Tensorflow/models/research && protoc object_detection/protos/*.proto --python_out=. && cp object_detection/packages/tf2/setup.py . && python -m pip install . 
    
if os.name=='nt':
    url="https://github.com/protocolbuffers/protobuf/releases/download/v3.15.6/protoc-3.15.6-win64.zip"
    wget.download(url)
    !move protoc-3.15.6-win64.zip {paths['PROTOC_PATH']}
    !cd {paths['PROTOC_PATH']} && tar -xf protoc-3.15.6-win64.zip
    os.environ['PATH'] += os.pathsep + os.path.abspath(os.path.join(paths['PROTOC_PATH'], 'bin'))   
    !cd Tensorflow/models/research && protoc object_detection/protos/*.proto --python_out=. && copy object_detection\\packages\\tf2\\setup.py setup.py && python    setup.py build && python setup.py install
    !cd Tensorflow/models/research/slim && pip install -e . 
 </pre>
 
 `nt` refers to windows while `posix` is for linux based system
 
 
  <b>Step 3.</b>
 
 Create Label map
 <pre>
 labels = [{'name':'ThumbsUp', 'id':1}, {'name':'ThumbsDown', 'id':2}, {'name':'ThankYou', 'id':3}, {'name':'LiveLong', 'id':4}]

with open(files['LABELMAP'], 'w') as f:
    for label in labels:
        f.write('item { \n')
        f.write('\tname:\'{}\'\n'.format(label['name']))
        f.write('\tid:{}\n'.format(label['id']))
        f.write('}\n')
 </pre>
