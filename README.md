# ControlVideo: Adding Conditional Control for One Shot Text-to-Video Editing 
This is the official implementation for "[ControlVideo: Adding Conditional Control for One Shot Text-to-Video Editing](http://arxiv.org/abs/2305.17098)". The project page is available [here](https://ml.cs.tsinghua.edu.cn/controlvideo/). Code will be released soon.
## Overview
ControlVideo incorporates visual conditions for all frames to amplify the source video's guidance, key-frame attention that aligns all frames with a selected one and temporal attention modules succeeded by a zero convolutional layer for temporal consistency and faithfulness. The three key components and corresponding fine-tuned parameters are designed by a systematic empirical study. Built upon the trained ControlVideo, during inference, we employ DDIM inversion and then generate the edited video using the target prompt via DDIM sampling.
![image](assets/method.png)
## Main Results
![image](assets/demo.png)
## To Do List
- [ ] Multi Controls Code Organization
- [x] Support ControlNet 1.1 
- [ ] Support Attention Control
- [ ] More Applications such as Image-Guided Video Generation
- [ ] Hugging Face
- [ ] More Sampler
## Environment
```
Ubuntu 20.04 on WSL2
CUDA 11.6
Python 3.9
```

```
git clone https://github.com/dai-ichiro/controlvideo
cd controlvideo
pip install -r requirements_cu116.txt
```
## Prepare Pretrained Text-to-Image Diffusion Model
Download the [Stable Diffusion 1.5](https://huggingface.co/runwayml/stable-diffusion-v1-5/tree/main). Put it in ```./sd```.

Download ControlNet for [canny](https://huggingface.co/lllyasviel/control_v11p_sd15_canny), [HED](https://huggingface.co/lllyasviel/sd-controlnet-hed), [depth](https://huggingface.co/lllyasviel/control_v11f1p_sd15_depth) and [pose](https://huggingface.co/lllyasviel/control_v11p_sd15_openpose). Put them in ```./controlnet``` .
## Quick Start
```
python main.py \
  --control_type hed \
  --video_path videos/car10.mp4 \
  --source "a car" \
  --target "a red car" \
  --out_root outputs/ \
  --max_step 300
```
The ```control_type``` is the type of controls, which is chosen from ```canny/hed/depth/pose```. The ```video_path``` is the path to the input video. The ```source``` is the source prompt for the source video. The ```target``` is the target prompt. The ```max_step``` is the step for training. The ```out_root``` is the path for saving results. 
## Run More Demos 
Download the [data](https://drive.google.com/drive/folders/1RrYCaq6QxSVD2K4wJFrTyDnISli8f625?usp=sharing) and put them in ```videos/```.
```
python run_demos.py
```
## References
If you find this repository helpful, please cite as:
```
@article{zhao2023controlvideo,
  title={ControlVideo: Adding Conditional Control for One Shot Text-to-Video Editing},
  author={Zhao, Min and Wang, Rongzhen and Bao, Fan and Li, Chongxuan and Zhu, Jun},
  journal={arXiv preprint arXiv:2305.17098},
  year={2023}
}
```
This implementation is based on [Tune-A-Video](https://github.com/showlab/Tune-A-Video) and [Video-p2p](https://github.com/ShaoTengLiu/Video-P2P).

