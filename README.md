# transcriber

Personal transcription tool built on [whisper.cpp](https://github.com/ggml-org/whisper.cpp), compiled with Vulkan GPU support for AMD GPUs.

## Setup

### Prerequisites

**Ubuntu 24.04**
```bash
sudo apt install cmake build-essential libvulkan-dev glslc libshaderc-dev spirv-headers
```

**Fedora**
```bash
sudo dnf install vulkan-loader-devel glslc libshaderc-devel spirv-headers-devel
```

### Build

```bash
cmake -B build -DGGML_VULKAN=ON
make -C build -j$(nproc)
```

### Download models

```bash
bash models/download-ggml-model.sh large-v3
bash models/download-ggml-model.sh large-v3-turbo
```

### Install the wrapper script

```bash
ln -sf "$PWD/scripts/whisper" ~/.local/bin/whisper
```

## Usage

```bash
whisper recording.mp3              # small model (default, fastest)
whisper --medium recording.mp3     # medium model
whisper --turbo recording.mp3      # large-v3-turbo (fast, near large accuracy)
whisper --large recording.mp3      # large-v3 (best accuracy)
```

Output is saved as a `.txt` file alongside the input file.

## Models

| Flag | Model | Size | Notes |
|------|-------|------|-------|
| (default) | ggml-small.en | 466 MB | Fast, English only |
| `--medium` | ggml-medium.en | 1.5 GB | Balanced, English only |
| `--turbo` | ggml-large-v3-turbo | 1.6 GB | Fast, near-large accuracy |
| `--large` | ggml-large-v3 | 3.1 GB | Best accuracy |
