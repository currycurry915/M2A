<div align="center">

<h1>AttentionFlow: Text-to-Video Editing Using Motion Map Injection Module</h1>

<h3><!--<a href="https://arxiv.org/abs/2303.17599"> Accept되면 링크 넣기-->AttentionFlow: Text-to-Video Editing Using Motion Map Injection Module</a></h3>

<!-- [Wen Wang](https://scholar.google.com/citations?user=1ks0R04AAAAJ&hl=zh-CN)<sup>1*</sup>, &nbsp; [Kangyang Xie](https://github.com/felix-ky)<sup>1*</sup>, &nbsp; [Zide Liu](https://github.com/zideliu)<sup>1*</sup>, &nbsp; [Hao Chen](https://scholar.google.com.au/citations?user=FaOqRpcAAAAJ&hl=en)<sup>1</sup>, &nbsp; [Yue Cao](http://yue-cao.me/)<sup>2</sup>, &nbsp; [Xinlong Wang](https://www.xloong.wang/)<sup>2</sup>, &nbsp; [Chunhua Shen](https://cshen.github.io/)<sup>1</sup> 나중에 우리 이름 넣고 고치기
 --> 
<!-- <sup>1</sup>[ZJU](https://www.zju.edu.cn/english/), &nbsp; <sup>2</sup>[BAAI](https://www.baai.ac.cn/english.html) -->

<br>

<image src="results/figure1.jpg" />
<br>

</div>

<h2>Abstract</h2>
Text-to-image diffusion, which has been trained with a large amount of text-image pair dataset, shows remarkable performance in generating high-quality images. Recent research using diffusion model has been expanded for text-guided video editing tasks by using text-guided image diffusion models as baseline. Existing video editing studies have devised an implicit method of adding cross-frame attention to estimate frame-frame attention to attention maps, resulting in temporal consistent editing. However, because these methods use generative models trained on text-image pair data, they do not take into account one of the most important characteristics of video: motion. When editing a video with prompts, the attention map of the prompt implying the motion of the video, such as `running' or `moving', is not clearly estimated and accurate editing cannot be performed. In this paper, we propose the `Motion Map Injection' (MMI) module to perform accurate video editing by considering movement information explicitly. The MMI module provides a simple but effective way to convey video motion information to T2V models by performing three steps: 1) extracting motion map, 2) calculating the similarity between the motion map and the attention map of each prompt, and 3) injecting motion map into the attention maps.  Considering experimental results, input video can be edited accurately and effectively with MMI module. To the best of our knowledge, our study is the first method that utilizes the motion in video for text-to-video editing.


## Installation

### Requirements

```shell
pip install -r requirements.txt
```
Installing [xformers](https://github.com/facebookresearch/xformers) is highly recommended for improved efficiency and speed on GPUs. 

### Weights

**[Stable Diffusion]** [Stable Diffusion](https://arxiv.org/abs/2112.10752) is a latent text-to-image diffusion model capable of generating photo-realistic images given any text input. The pre-trained Stable Diffusion models can be downloaded from Hugging Face (e.g., [Stable Diffusion v1-4](https://huggingface.co/CompVis/stable-diffusion-v1-4), [v2-1](https://huggingface.co/stabilityai/stable-diffusion-2-1)). We use Stable Diffusion v1-4 by default.

## Zero-shot testing

Simply run:

```bash
accelerate launch test_vid2vid_zero.py --config path/to/config
```

For example:
```bash
accelerate launch test_vid2vid_zero.py --config configs/car-moving.yaml
```

Note that we disable Null-text Inversion and enable fp16 for faster demo response.

## Examples
<table class="center">
<tr>
  <td style="text-align:center;"><b>Input Video</b></td>
  <td style="text-align:center;"><b>Video-P2P</b></td>
  <td style="text-align:center;"><b>Ours</b></td>
</tr>

 <tr>
  <td width=25% style="text-align:center;color:gray;">"clouds flowing under a skyscraper"</td>
  <td width=25% style="text-align:center;">"waves flowing under a skyscraper"</td>
  <td width=25% style="text-align:center;color:gray;">"waves flowing under a skyscraper"</td>
</tr>

<!-- <tr>
 오리지널 코드
  <td style colspan="2"><img src="results/clouds-waves-input.gif"></td>
  <td style colspan="2"><img src="results/clouds-waves-existing.gif"></td>
  <td style colspan="2"><img src="results/clouds-waves-MMI.gif"></td>
</tr> -->
<td height = "0">
  <div style = "height:100%"><img src = "results/clouds-waves-input.gif" height = "100%"></div>
  <div style = "height:100%"><img src = "results/clouds-waves-existing.gif" height = "100%"></div>
  <div style = "height:100%"><img src = "results/clouds-waves-MMI.gif" height = "100%"></div>
</td>

<tr>
  <td width=25% style="text-align:center;color:gray;">"clouds flowing on the mountain"</td>
  <td width=25% style="text-align:center;">"lava flowing on the mountain"</td>
  <td width=25% style="text-align:center;color:gray;">"lava flowing on the mountain"</td>
</tr>

<tr>
  <td style colspan="2"><img src="results/clouds-lava-input.gif"></td>
  <td style colspan="2"><img src="results/clouds-lava-existing.gif"></td>
  <td style colspan="2"><img src="results/clouds-lava-MMI.gif"></td>       
</tr>

<tr>
  <td width=25% style="text-align:center;color:gray;">"spinning wings of windmill are beside the river"</td>
  <td width=25% style="text-align:center;">"yellow spinning wings of windmill are beside the river"</td>
  <td width=25% style="text-align:center;color:gray;">"yellow spinning wings of windmill are beside the river"</td>
</tr>

<tr>
  <td style colspan="2"><img src="results/yellow-wings-input.gif"></td>
  <td style colspan="2"><img src="results/yellow-wings-existing.gif"></td>
  <td style colspan="2"><img src="results/yellow-wings-MMI.gif"></td>       
</tr>
</table>

