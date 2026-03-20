# Local Setup Instructions

This document provides instructions for setting the environment up locally.

<br>
<br>

## 1. Download and install Miniforge

Download miniforge from the GitHub repository [here](https://github.com/conda-forge/miniforge).

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/download.png" alt="download" width="600px">

Depending on your operating system, this should download either an `.sh` (macOS, Linux) or `.exe` file (Windows).

For the `.sh` file, open your command line terminal and execute the following command

```bash
sh ~/Desktop/Miniforge3-MacOSX-arm64.sh
```

where `Desktop/` is the folder where the Miniforge installer was downloaded to. On your computer, you may have to replace it with `Downloads/`.

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/miniforge-install.png" alt="miniforge-install" width="600px">

Next, step through the download instructions, confirming with "Enter".



If you work with many packages, Conda can be slow because of its thorough but complex dependency resolution process and the handling of large package indexes and metadata. To speed up Conda, you can use the following setting, which switches to a more efficient Rust reimplementation for solving dependencies:

```
conda config --set solver libmamba
```

<br>
<br>


## 2. Create a new virtual environment

After the installation was successfully completed, I recommend creating a new virtual environment called `LLMs`, which you can do by executing

```bash
conda create -n LLMs python=3.10
```

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/new-env.png" alt="new-env" width="600px">

> Many scientific computing libraries do not immediately support the newest version of Python. Therefore, when installing PyTorch, it's advisable to use a version of Python that is one or two releases older. For instance, if the latest version of Python is 3.13, using Python 3.10 or 3.11 is recommended.

Next, activate your new virtual environment (you have to do it every time you open a new terminal window or tab):

```bash
conda activate LLMs
```

<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/01_optional-python-setup-preferences/activate-env.png" alt="activate-env" width="600px">

<br>

## 3. Install required Python libraries

To install these requirements most conveniently, you can use the `requirements.txt` file in the root directory for this code repository and execute the following command:

```bash
pip install -r requirements.txt
```

## 4. Docker environment

The docker environment is copied primaryly from LLMs-from-scratch repository for Sebastian Raschka.

We build a devcontainer to do development under.

Run following commands to build the image and then run the container and Jupyter env within it.
Then start a browser and connect to Jupyter book to do dev work.

```shell
$> cd .devcontainer
$> docker build -f ./Dockerfile -t llmscratch.local .
# run the container on the HOST network, so its easy to open browsers and connect.
$> docker run -v "../02_data:/workspace" -h llm --name llm --rm --network host -it llmscratch.local bash
# run dev container plugin in vsCode and connect to the `llm` instance through remote connection
# now open a command prompt and type 
$> uv run jupyter lab --allow-root
# copy the jupyter notebook command and run it in browser with the secret key.,
```