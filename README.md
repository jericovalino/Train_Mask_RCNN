## Train_Mask_RCNN
A complete instructions on how to train a Mask-RCNN Model on Tensorflow from scratch


#### PC REQUIREMENTS


  -Nvidia GPU(with atleat 3.0 of computing power)</br>
  -Decent Webcam
    
    Note: if your computer don't have a GPU, you can still be able to train and run on tensorflow but it
    will take almost forever to train a model.


  *  Download and Install Git from [here](https://git-scm.com/downloads).
  *  Install VS 2015 C++ Build tools.<br/>
  *  Download and Install CUDA 9.0<br/>
   for windows 10 x64 machine, you can download the installer named "cuda_9.0.176_win10.exe" (1.4GB) [here](https://developer.nvidia.com/cuda-90-download-archive).<br/>
  *  Click [here](https://developer.nvidia.com/rdp/cudnn-archive) and click "Download cuDNN v7.4.1 (Nov 8, 2018), for CUDA 9.0".<br/>
  *  After downloading, decompress the .zip file to path "C:\tools".<br/>
  *  Add the Git, CUDA Toolkit and Library to Windows Environment Variable Path by clicking your way thru the following: 
> This PC>>Properties>>Advanced System Settings>>Environment Variables>>System Variables>>Path>>Edit 

    Then click "NEW" to add each:
    C:\Program Files\Git\bin\git.exe
    C:\Program Files\Git\cmd
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\libnvvp
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\extras\CUPTI\libx64
    C:\tools\cuda\bin
   
  *  Download Pixel Annotation Tool [here](https://github.com/abreheret/PixelAnnotationTool). <br/>
  *  Download LabelImg [here](https://tzutalin.github.io/labelImg/).
  <br/>
  
-----------------------------------------------------------------------------------------------------------------

#### #Setting Things Up<br/>

#### 1. Install Python 3.6.8
Download the Windows x86-64 executable installer from the [Python website](https://www.python.org/downloads/release/python-368/). <br/>
Note that we need this specific Python release since the version 3.7.x is having issues downloading the tensorflow package! <br/>
To make it easier to add in the Windows Environment Variables install Python on "C:\Python36\" directory. 

Add Python to Windows Environment Variable Path by clicking your way thru the following: <br/>
> This PC>>Properties>>Advanced System Settings>>Environment Variables>>System Variables>>Path>>Edit 
    
    Then click "NEW" to add each:
    C:\Python36
    C:\Python36\Scripts
    
To test Python, open up a CMD console and type: `python --version`. 

#### 2. Creating a Python Virtual Environment

Install virtualenv by issuing `pip install virtualenv` on cmd. 

Using a CMD line, go to the c:\ root directory by issuing `cd c:\` <br/>
Create a virtual environment using python by issuing c:\\>`virtualenv -p python ./Train_Mask_RCNN` <br/>
You should see a newly created folder in C:\ named "Train_Mask_RCNN" <br/>
Activate the virtual environment by issuing c:\\>`/Train_Mask_RCNN/Scripts/activate` <br/>
Once activated, you should be able to see the console prompt to have "(Train_Mask_RCNN)".

#### 3. Installing all the Modules and Packages needed inside the Virtual Environment

In this repository, download "requirements.txt" and place it inside Train_Mask_RCNN folder. <br/>
Using a CMD line, go to \Train_Mask_RCNN directory by issuing (Train_Mask_RCNN) c:\\>`cd Train_Mask_RCNN` <br/>
Install the requirements by entering (Train_Mask_RCNN) c:\Train_Mask_RCNN>`pip install -r requirements.txt` <br/>

Install COCO API(Clone).<br/>
Use pip to install the package: <br/>
(Train_Mask_RCNN) c:\Train_Mask_RCNN>`pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI` <br/>
Or visit this repository for more details: https://github.com/philferriere/cocoapi <br/> 
** Make sure that you have "vs c++ 2015 build tool" already installed on your computer otherwise you'll get an error while cloning.
  <br/>
  <br/>

-----------------------------------------------------------------------------------------------------------------

#### #Generating Project Resources<br/>

#### 1. Setup Tensorflow Models Repository

Now it's time when we will start using Tensorflow object detection API so go ahead and clone it by issuing the following command. <br/>
(Train_Mask_RCNN) c:\Train_Mask_RCNN>`git clone https://github.com/tensorflow/models.git` <br/>
Once you have cloned this repository, change your present working directory to \models\research and add it to your python path. If you want to add it permanently then you will have to make the change in your .bashrc file or you could add it temporarily for current session using the following command: <br/>

(Train_Mask_RCNN) c:\Train_Mask_RCNN>`set PYTHONPATH=C:\Train_Mask_RCNN\models;C:\Train_Mask_RCNN\models\research;C:\Train_Mask_RCNN\models\research\slim;`

#### 2. Compile Protobufs

Next, compile the Protobuf files, which are used by TensorFlow to configure model and training parameters. Unfortunately, the short protoc compilation command posted on TensorFlow’s Object Detection API installation page does not work on Windows. Every .proto file in the \object_detection\protos directory must be called out individually by the command.

In the CMD , change directories to \models\research. Copy and paste the following into the command line and press Enter:

(Train_Mask_RCNN) c:\Train_Mask_RCNN\models\research>`protoc --python_out=. .\object_detection\protos\anchor_generator.proto .\object_detection\protos\argmax_matcher.proto .\object_detection\protos\bipartite_matcher.proto .\object_detection\protos\box_coder.proto .\object_detection\protos\box_predictor.proto .\object_detection\protos\eval.proto .\object_detection\protos\faster_rcnn.proto .\object_detection\protos\faster_rcnn_box_coder.proto .\object_detection\protos\grid_anchor_generator.proto .\object_detection\protos\hyperparams.proto .\object_detection\protos\image_resizer.proto .\object_detection\protos\input_reader.proto .\object_detection\protos\losses.proto .\object_detection\protos\matcher.proto .\object_detection\protos\mean_stddev_box_coder.proto .\object_detection\protos\model.proto .\object_detection\protos\optimizer.proto .\object_detection\protos\pipeline.proto .\object_detection\protos\post_processing.proto .\object_detection\protos\preprocessor.proto .\object_detection\protos\region_similarity_calculator.proto .\object_detection\protos\square_box_coder.proto .\object_detection\protos\ssd.proto .\object_detection\protos\ssd_anchor_generator.proto .\object_detection\protos\string_int_label_map.proto .\object_detection\protos\train.proto .\object_detection\protos\keypoint_box_coder.proto .\object_detection\protos\multiscale_anchor_generator.proto .\object_detection\protos\graph_rewriter.proto`

This creates a name_pb2.py file from every name.proto file in the \object_detection\protos folder.
Note: TensorFlow occassionally adds new .proto files to the \protos folder. If you get an error saying ImportError: cannot import name 'something_something_pb2' , you may need to update the protoc command to include the new .proto files.

#### 3. Creating Project Folders
Create folders in path C:/ according to the following folder structure bellow:
   *  Tensorflow_API-Custom_Mask_RCNN <br/>
      *  pre_trained_models <br/>
      *  dataset
         *  Annotations
            *  xmls
         *  JPEGImages
         *  testImages 
      *  IG 
      *  CP

#### 4. Collecting and Gathering Data
In this project, we will train a mask rcnn model to detect 3 things(pencil, stappler and scissors). I took a lot of pictures of them in ramdom distance, ligthings, background and angles. All in all I collected 118 pictures(resize images to the size of "512 x 384"(doesn't need to be exact) so your PC won't run out of memory in training process). Then, move the 80% of the images to JPEGImages folder while other 20% will go to  testImages folder.

Here are some of the pictures I have collected:
![alt text](https://raw.githubusercontent.com/jericovalino/Train_Mask_RCNN/master/extra/images.PNG)
  <br/>
  <br/>
  
------------------------------------------------------------------------------------------------------------------

#### #Annotation to Training<br/>

#### 1. Annotating Images
Now here comes the fun part, We will now annotate images in JPEGImages folder using Pixel Annotation Tool. Watch [this](https://www.youtube.com/watch?v=tX-xcg5wY4U) youtube video on how to use this annotation tool(Annation process will take a while, so be patient). After the process, you will see 3 newly created files for every each of pictures in JPEGImages folder: <br/>
   -imageName_color_mask.png <br/>
   -imageName_mask.png <br/>
   -imageName_watershed_mask.png <br/>
Take all imageName_color_mask.png and place it in the dataset/Annotations folder and then rename it from imageName_color_mask.png to imageName.png <br/>
imageName_color_mask.png will look like this: <br/>
![alt text](https://raw.githubusercontent.com/jericovalino/Train_Mask_RCNN/master/extra/annotated_images.PNG)

#### 2. Generating Tensorflow record format
In order to use Tensorflow API, We need to feed data in Tensorflow record format. The script create_pet_tf_record.py given by tensorflow is modified to make it work in this project. You can get the modified script named create_mask_rcnn_tf_record.py in this repository inside the extra folder. All you need to do is to take this script and place it in the models/research/object_detection/dataset_tools. <br/>

    Note: create_mask_rcnn_tf_record.py is modified in such a way that given a mask image, it should found bounding box around
    objects on it owns and hence you don't need to spend extra time annotating bounding boxes but it comes at a cost, if mask
    image has multiple objects of same class then it will not be able to find bounding box for each object of the same class
    rather it will take a bounding box encompassing all objects of that class.
    
If you have multiple objects of the same class in some images then use labelImg to generate xml files with bounding boxes and then place all the xml file generated from labelImg under Annotations/xmls folder. once you have bounding box annotation in xml files use create_mask_rcnn_tf_record_multi.py to convert the data to tensorflow record format. <br/>

Open LabelImg, then select JPEGImages directory by clicking on Open Dir and change the save directory to Annotations/xmls by clicking on Change Save Dir. Now all you need to do is to draw rectangles around the object you are planning to detect. You will need to click on Create RectBox and then you will get the cursor to label the objects. After drawing rectangles around objects, give the name for the label and save it so that Annotations will get saved as the .xml file in Annotations/xmls folder. <br/>

![alt text](https://raw.githubusercontent.com/jericovalino/Train_Mask_RCNN/master/extra/label_img.PNG)

One additional thing you need to do is to edit the dictionary in the create_mask_rcnn_tf_record_multi.py script at line 57. You need to the give name of the classes as key and the value of pixel for the colour of mask you have chosen for respective class while masking the classobjects using pisxelAnnotationTool as value(you can check the pixel value of the color you used by running Check_pixel_values.ipynb in jupyter notebook...The pixel values of in my project are: "192" for pencil = yellow, "26" for stappler = blue, and "76" for scissors = red). After doing above, one last thing is still remaining before we get our Tensorflow record file. You need to create a file for label map, in this repo its label.pbtxt, with the dictionary of the label and the id of objects. Check label.pbtxt given in the repository to understand the format, its pretty simple (Note: name of the label should be same as class names you had given in the dictionary). Now it time to create record file. From models/research as present working directory run the following command to create Tensorflow record:


