# Setup Machine Learning on Apple Silicon M1

Hi folks 👋

This is simply a setup instruction for machine learning required packages, Python and TensorFlow on Apple Metal M1.

The latest Mac ARM M1-based machines have considerably better machine learning support than their previous Intel-based counterparts and yet it is exciting to try some casual ML models using the neural engine in this chip. While most of the CUDA packages architecture is different than the M1, installing ML packages could be a pain at the bottom!

This instruction aims to simply and craft a step-by-step guide to setup using MiniForge.

Note: PyTorch is currently struggling to catch up with M1 and there is no straight solution to using accelerated GPU with Python, feel free to pull this repo and add any other update/solution you might have.

## Install Homebrew

Homebrew is a package manager for the Mac, kind of similar to `yum` or `apt-get` for Linux. Copy and paste below line in a macOS Terminal to get things rolling.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

🚨 follow the steps when it finished, requires to echo command.

Now, you need to install the xcode-select command-line utilities. Use the following command to install:

```
xcode-select --install
```

🚨 If this command didn't work, you should install XCode from the App Store.

## Install MiniForge

It's time to put Homebrew to work, let's install MiniForge using Homebrew with this line:

```markdown
brew install miniforge
```

MiniForge is based on Anaconda but it emphasize on different CPU architectures such as M1 which is our current concern.

## Install Jupyter

Jupyter notebooks are always handy and good to have, so along with your IDE of your choice, install using the below command:

```
conda install -y jupyter
```

## Some extra libraries

I found at [this file](/tensorflow-apple-metal.yml) authored by [Jeff Heaton](https://github.com/jeffheaton) very useful. It installs some of very handy libraries at once, such as Pandas, SciPy, Matplotlib, etc.

I highly recommend installing them using the .yml file in this repo and run the command below which creates an environment called `tensorflow` and install all the dependencies in the file:

👉 I do highly recommend installing MiniConda along with MiniForge before proceeding as it helps keeping your PATHs organized.

```
conda env create -f tensorflow-apple-metal.yml -n tensorflow
```

Once the setup is done, access to this environment using the following command:

```
conda activate tensorflow
```

🚨 If the above command shows error, try `conda init {SHELL}` such as zsh or bash and run the activate again. If that didn't work too, then try `conda info --envs`, copy the path of tensorflow env and use `conda activate /PATH`.

Let's also add Jupyter to this environment:

```
conda install nb_conda
```

## Register environment

Alright it's time to register our newly created environement to the kernel using this command:

```
python -m ipykernel install --user --name tensorflow --display-name "Python 3.9 (tensorflow)"
```

🚨 Make sure your environment is activated and you are in (tensorflow).

## Testing the environment¶

Almost there! Let's just make sure everything is setup and works fine! Jump in to a new Jupyter notebook using this command:

```
jupyter notebook
```

And now paste and run this code to validate your setup:

```python
import sys

import tensorflow.keras
import pandas as pd
import sklearn as sk
import tensorflow as tf

print(f"TensorFlow Version: {tf.__version__}")
print(f"Keras Version: {tensorflow.keras.__version__}")
print()
print(f"Python {sys.version}")
print(f"Pandas {pd.__version__}")
print(f"Scikit-Learn {sk.__version__}")
gpu = len(tf.config.list_physical_devices('GPU'))>0
print("GPU is", "available" if gpu else "NOT AVAILABLE")
```

Wa-la! Here is your new glory M1 running latest versions of Machine Learning packages and waiting for you to create awesome stuff.
