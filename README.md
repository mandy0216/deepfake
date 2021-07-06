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
6. Run 
