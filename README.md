# Stable-SAM

Code for [Stable Segment Anything Model
](https://arxiv.org/abs/2311.15776).
Code will be released upon acceptance.

## Abstract
The Segment Anything Model (SAM) achieves remarkable promptable segmentation given high-quality prompts which, however, often require good skills to specify. To make SAM robust to casual prompts, this paper presents the first comprehensive analysis on SAM's segmentation stability across a diverse spectrum of prompt qualities, notably imprecise bounding boxes and insufficient points. Our key finding reveals that given such low-quality prompts, SAM's mask decoder tends to activate image features that are biased towards the background or confined to specific object parts. To mitigate this issue, our key idea consists of adjusting the sampling locations of image feature using learnable deformable offsets, while the original SAM model architecture and weights remain unchanged. Consequently, our deformable sampling plugin (DSP) enables SAM to adaptively shift attention to the prompted target regions in a data-driven manner, facilitated by our effective robust training strategy (RTS). During inference, dynamic routing plugin (DRP) is proposed that toggles SAM between the deformable and regular grid sampling modes, conditioned on the input prompt quality. Thus, our solution, termed Stable-SAM, is one of its kind focusing on solely adjusting feature sampling locations, which offers several advantages: 1) improved SAM's segmentation stability across a wide range of prompt qualities, while 2) retaining SAM's powerful promptable segmentation efficiency and generality, with 3) minimal learnable parameters (0.08 M) and fast adaptation (by 1 training epoch). Extensive experiments across multiple datasets validate the effectiveness and advantages of our approach, underscoring Stable-SAM as a more robust solution for segmenting anything.

## Performance Comparison

<p>
      <img src="https://github.com/fanq15/Stable-SAM/blob/main/images/miou.jpg" width="600px"> <br>
      <em>This figure shows a performance comparison among SAM, HQ-SAM and our Stable-SAM, when provided with suboptimal prompts. Our Stable-SAM consistently surpasses other methods across prompts of different quality, demonstrating better or comparable performance to the SAM prompted by ground truth box.
      </em>
</p>


## Visualization Comparison


<p>
      <img src="https://github.com/fanq15/Stable-SAM/blob/main/images/teaser.png" width="600px"> <br>
      <em>This figure displays the predicted masks and sampled important image features of SAM and Stable-SAM, with orange circles representing the attention weights, where a larger radius indicates a higher score. (a) SAM yields satisfactory segmentation results when provided with a high-quality box prompt. (b) Even a minor prompt modification leads to unstable segmentation output. SAM incorrectly segments the background, where the inaccurate box prompt misleads SAM to spend more attention to the background. (c) Our Stable-SAM accurately segments the target object by shifting more feature sampling attention to it.
      </em>
</p>



## Stable-SAM Network


<p>
      <img src="https://github.com/fanq15/Stable-SAM/blob/main/images/network.png"> <br>
      <em>(a) An illustration of our deformable sampling plugin (DSP) and deformable routing plugin (DRP) in SAM’s mask decoder transformer. DSP employs a small (b) offset network to predict the feature sampling offset. Subsequently, DSP resamples deformable image features at the updated sampling locations and feeds them into SAM’s token-to-image attention. DRP employs a small (c) MLP network to regulate the degree of DSP activation based on the input prompt quality. Note that our DSP adaptively adjusts solely the image feature sampling locations without altering the original SAM model.
      </em>
</p>


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
