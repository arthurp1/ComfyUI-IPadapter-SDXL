# IPAdapter-ComfyUI 
This is a custom node for [IP-Adapter](https://github.com/tencent-ailab/IP-Adapter) in [ComfyUI](https://github.com/comfyanonymous/ComfyUI).

# Install

1. Clone into custom_nodes
2. Place the IP-Adapter in `ComfyUI/custom_nodes/IPAdapter-ComfyUI/models` (e.g., [ip-adapter_sdxl.bin](https://huggingface.co/h94/IP-Adapter/blob/main/sdxl_models/ip-adapter_sdxl.bin)).
3. Place the CLIP_vision model in `ComfyUI/models/clip_vision` (e.g., [pytorch_model.bin]([https://huggingface.co/h94/IP-Adapter/blob/main/models/image_encoder/pytorch_model.bin](https://huggingface.co/h94/IP-Adapter/blob/main/sdxl_models/image_encoder/pytorch_model.bin)).

# Usage
Start ComfyUI and load the workflow `ip-adapter.json`.

## Required Inputs
+ **model**: Connect the SDXL base and refiner models.
+ **image**: Reference image.
+ **clip_vision**: Connect to the output of `Load CLIP Vision`.
+ **mask**: Optional. Connect a mask to limit the area of application. The mask should have the same resolution as the generated image.
+ **weight**: Strength of the application.
+ **model_name**: Specify the filename of the model to use.
+ **dtype**: If a black image is generated, select `fp32`. The generation time hardly changes, so it might be fine to leave it as `fp32`.

## Output
+ **MODEL**: Connect to KSampler, etc.
+ **CLIP_VISION_OUTPUT**: Normally you don't have to worry about it. Can save unnecessary calculations when using Revision, etc.

# Bug
+ For some reason, `Apply ControlNet` bugs out, so please use `Apply ControlNet(Advanced)` as an alternative.

# Models
+ Official models: https://huggingface.co/h94/IP-Adapter
