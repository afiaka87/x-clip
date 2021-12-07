<img src="./clip.png" width="600px"></img>

## x-clip (wip)

A concise but complete implementation of <a href="https://openai.com/blog/clip/">CLIP</a> with various experimental improvements from recent papers

## Install

```bash
$ pip install x-clip
```

## Usage

```python
import torch
from x_clip import CLIP

clip = CLIP(
    dim_text = 512,
    dim_image = 512,
    dim_latent = 512,
    num_text_tokens = 10000,
    text_enc_depth = 6,
    text_seq_len = 256,
    text_heads = 8,
    num_visual_tokens = 512,
    visual_enc_depth = 6,
    visual_image_size = 256,
    visual_patch_size = 32,
    visual_heads = 8,
    use_all_token_embeds = True   # whether to use fine-grained contrastive learning (FILIP)
)

text = torch.randint(0, 10000, (4, 256))
images = torch.randn(4, 3, 256, 256)
mask = torch.ones_like(text).bool()

loss = clip(text, images, text_mask = mask, return_loss = True)
loss.backward()
```

## Usage - CLI
```sh
train.py [-h] [--datadir DATADIR] [--bpe_path BPE_PATH]
            [--batch-size BATCH_SIZE] [--num-epochs NUM_EPOCHS]
            [--learning-rate LEARNING_RATE]
            [--clip_grad_norm_factor CLIP_GRAD_NORM_FACTOR]
            [--log_frequency LOG_FREQUENCY]
            [--ckpt_save_path CKPT_SAVE_PATH] [--overwrite] [--amp]
            [--dim_text DIM_TEXT] [--dim_image DIM_IMAGE]
            [--dim_latent DIM_LATENT] [--text_enc_depth TEXT_ENC_DEPTH]
            [--text_seq_len TEXT_SEQ_LEN] [--text_heads TEXT_HEADS]
            [--num_visual_tokens NUM_VISUAL_TOKENS]
            [--visual_enc_depth VISUAL_ENC_DEPTH]
            [--visual_heads VISUAL_HEADS]
            [--visual_image_size VISUAL_IMAGE_SIZE]
            [--visual_patch_size VISUAL_PATCH_SIZE] [--channels CHANNELS]
            [--use_all_token_embeds]
```

## Citations

```bibtex
@misc{radford2021learning,
    title   = {Learning Transferable Visual Models From Natural Language Supervision}, 
    author  = {Alec Radford and Jong Wook Kim and Chris Hallacy and Aditya Ramesh and Gabriel Goh and Sandhini Agarwal and Girish Sastry and Amanda Askell and Pamela Mishkin and Jack Clark and Gretchen Krueger and Ilya Sutskever},
    year    = {2021},
    eprint  = {2103.00020},
    archivePrefix = {arXiv},
    primaryClass = {cs.CV}
}
```

```bibtex
@misc{yao2021filip,
    title   = {FILIP: Fine-grained Interactive Language-Image Pre-Training}, 
    author  = {Lewei Yao and Runhui Huang and Lu Hou and Guansong Lu and Minzhe Niu and Hang Xu and Xiaodan Liang and Zhenguo Li and Xin Jiang and Chunjing Xu},
    year    = {2021},
    eprint  = {2111.07783},
    archivePrefix = {arXiv},
    primaryClass = {cs.CV}
}
```
