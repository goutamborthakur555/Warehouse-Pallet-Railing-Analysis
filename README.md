# Warehouse Pallet Railing Analysis

**Objective:**  To build an end to end automated model where the model will take the input stream of pallet railings from the camera to detect the pallet railing health i.e., to predict the damage and any cracks within the pallet railing itself. Model will be used before start and end of the operations of warehouse to detect the pallet railing health, there by the respective pallet railing can be replaced or repaired.

**Challenges:** Collection of training dataset, annotation, latency and size of the model.

**1. Warehouse Rail Analysis using YOLOv5 with PyTorch: (For first time custom training of the model, follow the below steps)**

(a) Installing the dependencies and cloning yolov5 repository
(Note: Choose GPU in Runtime in Google Colab. Steps: Runtime --> Change Runtime Type --> Hardware accelerator --> GPU --> Save)

(b). Annotation of custom dataset is done using 'Labelme' and uploaded the .json files to the Roboflow for Data Augmentation & Resizing (Data Preprocessing)
For more details: https://www.youtube.com/watch?v=XKJc2YT5-es&t=398s

(c). Copy the correct format of Custom Dataset link from Roboflow
Use the "YOLOv5 PyTorch" format to export the dataset, click on get link, copy the link.
Steps: Export Yor Dataset --> Format(YOLO v5 PyTorch) --> Get Link

(d). Define Model Configuration and Architecture
We will write a yaml script that defines the parameters for our model like the number of classes, anchors, and each layer.

(e). To train on custom dataset for YOLOv5 Detector
Here, we are able to pass a number of arguments:
img: define input image size
batch: determine batch size
epochs: define the number of training epochs. (Note: often, 3000+ are common here!)
data: set the path to our yaml file
cfg: specify our model configuration
weights: specify a custom path to weights. (Note: we can download weights from the Ultralytics Google Drive Folder)
name: result names
nosave: only save the final checkpoint
cache: cache images for faster training

(f). Evaluate the Custom YOLOv5 Detector Performance
Training losses and performance metrics are saved to Tensorboard and also to a logfile defined above with the --name flag when we train. In our case, we named this yolov5s_results. (If no name is given, it defaults saved as results.txt.) The results file is plotted as a png after training completes.
Note: Partially completed results.txt files can be plotted with from utils.utils import plot_results; plot_results().

(g) To visualize our Training Data with Labels
After training completed, view train*.jpg images to see training images, labels and augmentation effects.

(h). Run Inference With Trained Weights
Run inference with a pretrained checkpoint on contents of test/images folder downloaded from Roboflow.

(i). Using the "best.pt" weight to check on the test/unseen dataset

(j). Export Trained Weights for Future Inference
Now, we have trained and tested our custom detector. We can export the best trained weights (best.pt) in Google Drive or in our device for our further use.


**2. Warehouse Rail Analysis using YOLOv5 with PyTorch (To check the result in the saved pre-trained weight from Google Drive)
If we want to check the result for next time, with pre-trained weight, find the steps below.**

(a). Installing the dependencies and cloning yolov5 repository
(Note: Choose GPU in Runtime in Google Colab. Steps: Runtime --> Change Runtime Type --> Hardware accelerator --> GPU --> Save)

(b). Import Trained Weights, images to be test from Google Drive for testing
As we have the saved (best.pt) weight in our Google Drive, we need to import/copy to our VM Google Colab for testing.

(c). To Test on copied images from Google Drive
Use the copied 'best.pt' weight to detect the object and display for the copied images from Google Drive to yolov5 --> inference --> images folder
