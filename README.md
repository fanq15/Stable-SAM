# Stable-SAM

Code for [Stable Segment Anything Model
](https://arxiv.org/abs/2311.15776).
Code will be released upon acceptance.


## Performance Comparison

<img src="https://github.com/fanq15/Stable-SAM/blob/main/images/miou.jpg" width="600px">

This figure shows a performance comparison among SAM, HQ-SAM and our Stable-SAM, when provided with suboptimal prompts. Our Stable-SAM consistently surpasses other methods across prompts of different quality, demonstrating better or comparable performance to the SAM prompted by ground truth box.

## Visualization Comparison

<img src="https://github.com/fanq15/Stable-SAM/blob/main/images/teaser.png" width="600px">

This figure displays the predicted masks and sampled important image features of SAM and Stable-SAM, with orange circles representing the attention weights, where a larger radius indicates a higher score. (a) SAM yields satisfactory segmentation results when provided with a high-quality box prompt. (b) Even a minor prompt modification leads to unstable segmentation output. SAM incorrectly segments the background, where the inaccurate box prompt misleads SAM to spend more attention to the background. (c) Our Stable-SAM accurately segments the target object by shifting more feature sampling attention to it.

## Stable-SAM Network

<img src="https://github.com/fanq15/Stable-SAM/blob/main/images/network.png"> 

(a) An illustration of our deformable sampling plugin (DSP) and deformable routing plugin (DRP) in SAM’s mask decoder transformer. DSP employs a small (b) offset network to predict the feature sampling offset. Subsequently, DSP resamples deformable image features at the updated sampling locations and feeds them into SAM’s token-to-image attention. DRP employs a small (c) MLP network to regulate the degree of DSP activation based on the input prompt quality. Note that our DSP adaptively adjusts solely the image feature sampling locations without altering the original SAM model.

## Reference
```
@misc{fan2023stable,
      title={Stable Segment Anything Model}, 
      author={Qi Fan and Xin Tao and Lei Ke and Mingqiao Ye and Yuan Zhang and Pengfei Wan and Zhongyuan Wang and Yu-Wing Tai and Chi-Keung Tang},
      year={2023},
      eprint={2311.15776},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```
