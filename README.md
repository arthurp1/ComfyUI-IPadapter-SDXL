# IPAdapter-ComfyUI 
This is a custom node for [IP-Adapter](https://github.com/tencent-ailab/IP-Adapter) in [ComfyUI](https://github.com/comfyanonymous/ComfyUI).

2023/08/27:
Specifications for the plus model have been updated, and the node now supports multiple images and area selection via masks.

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

## Multiple conditions.
By naturally connecting the nodes, multiple images can be input. By combining with Mask, you can also conditionally divide the left and right.
![image](https://github.com/laksjdjf/IPAdapter-ComfyUI/assets/22386664/c2282aee-ab98-488d-936e-1787994e957f)
The background also gets split, which could be an issue.

# Hint
+ The input image is automatically cropped to a square in the center, so if you want to avoid this, you can either manually crop it beforehand or use `preprocess/furusu Image crop`. For `preprocess/furusu Image crop`, there are options to pad the image (`padding`) or to crop based on the character's face (`face_crop`). The required [lbpcascade_animeface.xml](https://github.com/nagadomi/lbpcascade_animeface) might not be automatically downloaded, so in that case, please manually place it in the root directory of the repository.

# Bug
+ For some reason, `Apply ControlNet` bugs out, so please use `Apply ControlNet(Advanced)` as an alternative.

# Models
+ Official models: https://huggingface.co/h94/IP-Adapter
