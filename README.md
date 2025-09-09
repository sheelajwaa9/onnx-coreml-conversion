# onnx-coreml-conversion

This repository demonstrates how to convert an ONNX model (`.onnx`) into a CoreML model (`.mlmodel`) using Docker and a pinned environment.

---

## Prerequisites

On macOS, make sure Docker is installed and running. The easiest way is:

```bash
brew install --cask docker
```

Then start Docker Desktop once so the Docker daemon is available.

---

## One-Liner Conversion

Run this from the directory containing your ONNX file (replace):

```bash
docker run --platform=linux/amd64 --rm -v $PWD:/work python:3.8 bash -c "\
  pip install coremltools==4.1 onnx==1.7.0 protobuf==3.20.3 && \
  python -c \"import coremltools as ct; mlmodel = ct.converters.onnx.convert(model='/work/model.onnx'); mlmodel.save('/work/model.mlmodel')\" \
"
```

---

## Output

After running, you will have:

- `model.mlmodel` in the same directory as your ONNX file
- A ready-to-use CoreML model for Xcode and Vision

---

## Why This Works

- Uses Python 3.8 with `--platform=linux/amd64` to download prebuilt wheels
- Pins CoreMLTools 4.1, ONNX 1.7.0, and Protobuf 3.20.3 (a stable, compatible combination)
- Runs fully inside Docker, keeping your local environment clean
