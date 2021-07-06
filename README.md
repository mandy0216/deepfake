# deepfake
Instructions to run the code for Training and Testing the proposed method on Google Cloud Platform's DeepLearningVM:
An account needs to be set up in Google Cloud Platform to access their GPU servers. Once the DeepLearningVM is created 
and deployed successfully, follow the following steps:
1. Open the Colab notebook from: https://colab.research.google.com/drive/1fCyd5XghutNS2vRIqa-dFCCBBHvRdZ_6#scrollTo=zlp-f0dDgWbj
   From the little arrow on the top right side of the tab, where it says 'Connect', select 'connect to a local runtime'. A window will pop up.
   Type "http://localhost:8080/" where it asks for a local backend and save. This should establish the connection between your machine and the 
   GCP's virtual machine and a Green checkmark will appear along with 'Connected (local)' on the top right corner.
2. Run the first cell under the header 'Another Implementation' to get the correct cuda libraries in order to run the code on the GPU.
3. Run the next three cells to install tensorflow-gpu, tensorflow latest version and keras upgrade.
4. Clone the git repository by running the next cell.
5. Change the working directory to deepfake-detection.
## Datasets and Preprocessing
Deepfake TIMIT
https://www.idiap.ch/dataset/deepfaketimit

deepfakeTIMIT dataset consists of videos. So, to split video by frame, run this command.

imgdir : image directory for saving split image.

viddir : directory which has deepfakeTIMIT dataset.

python TIMIT_data_process.py --imgdir /root/data/deepfakeTIMIT --viddir /root/rawData/DeepfakeTIMIT --split True
Finally, to make csv file, run this command.

imgdir : image directory which has split images.

csvdir : directory for saving csv file. (our csvdir has 2 subdirectory train, val)

python TIMIT_data_process.py --imgdir /root/data/deepfakeTIMIT --csvdir /root/csv

UADFV
https://drive.google.com/drive/u/0/folders/1GEk1DSxmlV_61JtpEGzC9Fo_BffvyxpH

This dataset contains 98 videos, which having 49 real videos and 49 fake videos respectively.

To split video into frame, create UADFV folder in /root/data and create fake, real folder in it. and to save split image, and you have to run below command.

python spliter.py _ /root/data/UADFV/fake True /root/rawData/UADFV/fake
python spliter.py _ /root/data/UADFV/real True /root/rawData/UADFV/real
To make csv file, run this command.

dir : image directory which has split images.

python UADFV_data_process.py --dir /root/data/UADFV

Usage
Train
In the command shown at below, you can add arguments before the 'csv' to control the training condition and add arguments after the 'csv' to handle the data that you want to use for training. Since there are too much arguments for control training condition, several necessary arguments will be introduced here.

Controlling training condition

model: Model name, set as resnet50 as default. To add other models for training, you should make model in "deepfake-detection/models" directory.
snapshot: The pretrained model's directory used for resume training from the save point of previous experiments.
tensorboard-dir: log directory for tensorboard outputs. Set as './logs' as default.
handling data for training

The first argument after 'csv' is training csv file directory for training which are usually placed in 'csv/train' directory. Also, argument 'val-annotations' is validation csv file directory used in training which are usually placed in 'csv/val' directry.

Test
You can load some pretrained model and check the accuracy for that pretrained model to test thee performance of trained model.

Since our data processing part don't support high-resolution image, the recommended input images' width and height should be less than 700px. Followings are several arguments that can be changed by training conditions and evaluation condition.

model: Model name, set as resnet50 as default.
batch-size: Size of batches used for data processing.
gpu: Id of the GPU to use as reported by nvidia-smi.
multi-gpu: Number of GPUs to use for parallel processing, integer number.
multi-gpu-force: Extra flag needed to enable experimental multi-gpu-support
config: path to a configuration parameters .ini file.
These seven arguments should be added in front of csv in below code and these are set with default values.

The two arguments after csv in below code are evaluation csv data path and pretrained weight at certain epoch, respectively.

python evaluate.py csv /root/csv/val/validation.csv /root/deepfake-detection/deepfake-detection/bin/snapshots/resnet50_csv_40.h5


python -u train.py --model vgg16 csv /root/csv/train/train.csv --val-annotations=/root/csv/val/validation.csv >> vgg16.log
