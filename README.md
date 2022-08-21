# Stop-Arm Violation Detection

Children crossing streets are at risk of being met with an accident. School bus stop-arm cameras are a new way out. They are being deployed by school districts and law enforcement organizations to prevent drivers from passing stopped school buses. When the stop-arm is extended, the stop-arm camera normally records video of vehicles and/or drivers passing school buses. When a vehicle passes a school bus with a stop-arm deployed, our Smart Stop AI solution employs the latest Artificial Intelligence technology to detect and report stop-arm violations by capturing violating vehicle information (image and license plate). In this paper, we propose to use YoloV3 with the integration of EasyOCR to detect the license plate from the stop-arm violation video. We perform Gaussian Blur with an optimized kernel on the frames of the video and a spatial variant of the Structural Similarity algorithm to compute the difference between images is employed. We track the center point, height, and width of the images to find the moving vehicle and its presence in the violated zone. On the resulting license plate image, image localization, segmentation, and optical character recognition are applied to get the vehicle number and other details. These details would then be stored in the Azure cloud platform for further actions by Government Agencies.

## Datasets and Models

We have used pre-trained COCO dataset available in internet for our project. The MS COCO dataset (Microsoft Common Objects in Context) is a large-scale dataset for object detection, segmentation, key-point detection, and captioning, which is freely available for all. And used Yolov3 model for vehicle detection, our proposed method consists of various steps
Our proposed method consists of various steps
A. Detecting the vehicle object
B. Extracting Frame Difference
C. Automatic License Plate Recognition

## Getting started with the project
***
* Clone the Repository "https://github.com/Pradeep-Nagaraj/COMP5800-Stop-Arm-Violation"
* Download the model, yolov3.weights file and copy it into the same directory
* Make sure all files are in same directory.
* Run the code from [Final.ipynb](https://github.com/Pradeep-Nagaraj/COMP5800-Stop-Arm-Violation/blob/main/Final.ipynb) file.



## Data Storage in CLoud

Azure Blob storage is Microsoft’s object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data.  AzCopy is an easy-to-use command-line tool for Windows and Linux that copies data to and from Blob storage, across containers, or across storage accounts.

We have created a storage account name, vehicle information, and a container to upload our output images. 

Step-1: Command to create container in Azure

azcopy make "https://vehicleinfo.blob.core.windows.net/vehicleviolatedinfo?sv=2021-06-08&ss=bfqt&srt=sco&sp=rwdlacupiytfx&se=2022-09-01T10:17:27Z&st=2022-08-15T02:17:27Z&spr=https&sig=LZxi3Kcg3QLGe1kZyyOfXo%2BjBc%2Bi5yuxpr9lDei9U7M%3D"

From the command line, we can run the script to move the data from our local drive to the cloud. 

Step-2: Command to copy files to Azure container

azcopy copy "C:\Users\prade\miniconda3\MyProject\Final-Code\Result/*" "https://vehicleinfo.blob.core.windows.net/vehicleviolatedinfo?sv=2021-06-08&ss=bfqt&srt=sco&sp=rwdlacupiytfx&se=2022-09-01T10:17:27Z&st=2022-08-15T02:17:27Z&spr=https&sig=LZxi3Kcg3QLGe1kZyyOfXo%2BjBc%2Bi5yuxpr9lDei9U7M%3D"

To automate the process, we have scheduled the task in MS Task Scheduler using batch file, which will run every day at 12pm to transfer all the violated vehicle images to the cloud.
