# Environment Setup

## Step 1. Install Miniconda

Start by downloading the Miniconda release compiled for arm64, you can download this at the link below:

https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh

Once downloaded run the script, if you need to upgrade the version add the -u option

### **_New Install_**

`zsh Miniforge3-MacOSX-arm64.sh`

### **_Upgrade install_**

`zsh Miniforge3-MacOSX-arm64.sh -u`

### **_Post install_**

If you don't want the base environment to be activate when the console starts run the command below, which is also printed out in the console.

`conda config --set auto_activate_base false`

---

## Step 2. Create a new Virtual Environment

(Mini)Conda makes managing virtual environments quite simple, so lets create a new Python 3.8 environment using the command:

`conda create --name deepLearning python=3.8`

---

## Step 3. Install TensorFlow

Now we can install the Apple Silicon fork of Tensor Flow from the github repo, since this is under active development its best to get the latest version. To do this go to the Github page below and select the latest version, at the time of writing it was v0.1 alpha1

https://github.com/apple/tensorflow_macos/releases

Download the .tar.gz file which can be found by expanding the 'Assets' button.

Once downloaded we need to add some environment vars to the downloaded location and python environment, replace USERNAME with your own username and run the commands in the terminal.

- `export libs=/Users/USERNAME/Downloads/tensorflow_macos/arm64`
- `export env=/Users/USERNAME/miniforge3/envs/deepLearning`

Now the terminal and python environment should be configured for the install of TensorFlow. Unpackage the downloaded archive but don't run the default script since this does not work smoothly with anaconda. I use anaconda as it provides a nice set of packages and makes managing environments quite easy. What we want to do instead is install the downloaded packages manually along with some other packages we will need.

- `conda activate deepLearning`
- `pip install cached-property six`
- `conda upgrade -c conda-forge pip setuptools`
- `pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/grpcio-1.33.2-cp38-cp38-macosx_11_0_arm64.whl"`
- `pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/h5py-2.10.0-cp38-cp38-macosx_11_0_arm64.whl"`
- `pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/tensorflow_addons-0.11.2+mlcompute-cp38-cp38-macosx_11_0_arm64.whl"`
- `conda install -c conda-forge -y absl-py astunparse gast opt_einsum termcolor typing_extensions wheel typeguard`
- `pip install tensorboard`
- `pip install wrapt flatbuffers tensorflow_estimator google_pasta keras_preprocessing protobuf`
- `pip install --upgrade -t "$env/lib/python3.8/site-packages/" --no-dependencies --force "$libs/tensorflow_macos-0.1a1-cp38-cp38-macosx_11_0_arm64.whl"`
- `conda install -y -c conda-forge notebook pandas`
- `conda install -y pillow SciPy matplotlib`
