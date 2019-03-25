## Train_Mask_RCNN
A complete instructions on how to train a Mask-RCNN Model on Tensorflow from scratch


#### PC REQUIREMENTS


  -Nvidia GPU(with atleat 3.0 of computing power)</br>
    Gtx 1050ti is the one used in this project
    
    Note: if your computer don't have a GPU, you can still be able to train and run on tensorflow but it
    will take almost forever to train a model.

#### Preparing Your Computer<br/>
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

Using a CMD line, go to the C:\ root directory by issuing `cd C:\` <br/>
Create a virtual environment using python by issuing `virtualenv -p python ./Train_Mask_RCNN` <br/>
You should see a newly created folder in C:/ named "Train_Mask_RCNN" <br/>
Activate the virtual environment by running `/Train_Mask_RCNN/Scripts/activate` <br/>
Once activated, you should be able to see the console prompt to have "(Train_Mask_RCNN)".

#### 3. Installing all the Modules and Packages needed inside the Virtual Environment

In this repository, download "requirements.txt" and place it inside Train_Mask_RCNN folder. <br/>
Using a CMD line, go to the C:\Train_Mask_RCNN directory by issuing `cd C:\Train_Mask_RCNN` <br/>
Install the requirements by entering `(Train_Mask_RCNN) c:\Train_Mask_RCNN>pip install - requirements.txt` <br/>

Install COCO API(Clone).<br/>
Use pip to install the package: <br/>
`(Train_Mask_RCNN) c:\Train_Mask_RCNN>pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI` <br/>
Or visit this repository for more details: https://github.com/philferriere/cocoapi <br/> 
** Make sure that you have "vs c++ 2015 build tool" already installed on your computer otherwise you'll get an error while cloning.

#### 4. Setup Tensorflow Models Repository

Now it's time when we will start using Tensorflow object detection API so go ahead and clone it by using the following command. <br/>
`(Train_Mask_RCNN) c:\Train_Mask_RCNN>git clone https://github.com/tensorflow/models.git` <br/>
Once you have cloned this repository, change your present working directory to models/research/ and add it to your python path. If you want to add it permanently then you will have to make the change in your .bashrc file or you could add it temporarily for current session using the following command: <br/>

`(Train_Mask_RCNN) c:\Train_Mask_RCNN\models\research>set PYTHONPATH=C:\Train_Mask_RCNN\models;C:\Train_Mask_RCNN\models\research;C:\Train_Mask_RCNN\models\research\slim;`



