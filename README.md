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

