# Train_Mask_RCNN
Instructions on how to train a Mask-RCNN Model on Tensorflow from scracth


<b>PC REQUIREMENTS</b>


  -Nvidia GPU(with atleat 3.0 of computing power)</br>
    Gtx 1050ti is the one used in this project
    
    Note: if your computer don't have a GPU, you can still be able to train and run on tensorflow but it
    will take almost forever to train a model.

<b>Preparing Your Workststation</b><br/>
  -Install VS 2015 C++ Build tools<br/>
  -Download and Install CUDA 9.0<br/>
    for windows 10 x64 machine, you can download the installer named "cuda_9.0.176_win10.exe" (1.4GB) [here](https://developer.nvidia.com/cuda-90-download-archive).<br/>
  -Copy and paste this link on your browser "https://developer.nvidia.com/rdp/cudnn-archive" and click "Download cuDNN v7.4.1 (Nov 8, 2018), for CUDA 9.0".<br/>
  -After downloading, decompress the .zip file to path "C:\tools".<br/>
  -Add the CUDA Toolkit and Library to Windows Environment Variable Path by clicking your way thru the following: 
> This PC>>Properties>>Advanced System Settings>>Environment Variables>>System Variables>>Path>>Edit 

    Then click "NEW" to add each: <br/>
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin <br/>
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\libnvvp <br/> 
    C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\extras\CUPTI\libx64 <br/>
    C:\tools\cuda\bin <br/>
