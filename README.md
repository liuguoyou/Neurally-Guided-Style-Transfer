# Neurally-Guided-Style-Transfer

The official implementation of algorithms described in papers:

**(1) Arbitrary Style Transfer Using Neurally-Guided Patch-Based Synthesis** </br>
_[O. Texler](https://ondrejtexler.github.io/), [D. Futschik](https://dcgi.fel.cvut.cz/people/futscdav),
[J. Fišer](https://research.adobe.com/person/jakub-fiser/), [M. Lukáč](https://research.adobe.com/person/michal-lukac/), 
[J. Lu](https://research.adobe.com/person/jingwan-lu/), [E. Shechtman](https://research.adobe.com/person/eli-shechtman/), 
and [D. Sýkora](https://dcgi.fel.cvut.cz/home/sykorad/)_ </br>
[[`WebPage`](https://ondrejtexler.github.io/neurally_guided/index.html)],
[[`Paper`](https://ondrejtexler.github.io/res/CAG_main.pdf)],
[[`BiBTeX`](#CitingNeurallyGuided)]
<!-- In Computers & Graphics (Elsevier, January 2020) -->

**(2) Enhancing Neural Style Transfer using Patch-Based Synthesis** </br>
_[O. Texler](https://ondrejtexler.github.io/),
[J. Fišer](https://research.adobe.com/person/jakub-fiser/), [M. Lukáč](https://research.adobe.com/person/michal-lukac/), 
[J. Lu](https://research.adobe.com/person/jingwan-lu/), [E. Shechtman](https://research.adobe.com/person/eli-shechtman/), 
and [D. Sýkora](https://dcgi.fel.cvut.cz/home/sykorad/)_ </br>
[[`WebPage`](https://dcgi.fel.cvut.cz/home/sykorad/stylitneural.html)],
[[`Paper`](https://dcgi.fel.cvut.cz/home/sykorad/Texler19-NPAR.pdf)],
[[`Slides`](https://dcgi.fel.cvut.cz/home/sykorad/Texler19-NPAR.pptx)]
<!-- In Proceedings of the 8th ACM/EG Expressive Symposium, pp. 43-50 (Expressive 2019, Genoa, Italy, May 2019) -->

Neural based style transfer methods are capable of delivering amazing stylized imagery; however, the results are usually low-resolution,
blurred, contrast does not match the original style, and the image lacks many artistically essential details, e.g., brush-strokes, 
properties of the used artistic medium, or canvas structure.

This tool is designed to overcome the aforementioned drawbacks of neural based style transfer and allow for creating 
high-quality and extremely high-resolution images. The use-case is the following. 
* Let's assume we have a style exemplar and target photograph in high-resolution.
* First, we run these two images through our favorite neural-based style transfer method. The result we get is 
of a low resolution and does not represent the used style exemplar well.
* Second, we use this tool to restore the quality of the neural result and upscale it to the resolution of the style exemplar.

<p align='center'>
  <img src='doc/res_blonde.jpg'/>
  <b>Portrait on a wall.</b> Target and Style are of 4000x3000 px. Neural results (Gatys et al. and DeepDream, top left triangles) were 
  generated in approximately 580x435 px. Neural results were then reconstructed and upscaled by this tool (Gatys et al.+ours and 
  DeepDream+ours, bottom right triangles) to the original resolution of 4000x3000.
</p>

<p align='center'>
  <img src='doc/res_346M.jpg'/>
  <b>Extremely large 346Mpix image.</b> Target and Style are of 26412x13127 px. The neural result (not shown here) was approximately 700x348 px. This result
  was then reconstructed and nearly 40 times upscaled by this tool to the original resolution. The right part of the figure shows 
  zoom-in patches. See all the individual brush strokes and its sharp boundaries. Also, notice how well the structure of the original canvas and
  little cracks of the painting are preserved.
</p>


## Build
### On Windows 
* Run `build-win.bat`, it should output `styletransfer.exe`
* It depends on OpenCV and it expects `opencv_world420.dll` in your PATH. Pre-build DLL can be downloaded at https://opencv.org/opencv-4-2-0/, (or directly https://sourceforge.net/projects/opencvlibrary/files/4.2.0/opencv-4.2.0-vc14_vc15.exe/download)

### On Linux 
* Download and build OpenCV 4.2.0 (https://opencv.org/opencv-4-2-0/)
* Copy `libopencv_world.so`, `libopencv_world.so.4.2`, and `libopencv_world.so.4.2.0` to the `opencv-4.2.0/lib`
* Do not forget to update your `LD_LIBRARY_PATH` to point to the `opencv-4.2.0/lib`
* Run `build-linux.sh`, it should output `styletransfer`

## Parameters
* `--style <string>`, mandatory, path to the style image
* `--neural_result <string>`, mandatory, path to the neural result
* `--out_path <string>`, optional, output path, if not specified `--neural_result`+"_enhanced.jpg" is used instead 
* `--target <string>`, optional, has to be specified if you want to use `--guide_by_target` or `--recolor_by_target`
* `--guide_by_target <bool>`, optional, might help to restore some content of the target image, but also might make the result worse stylization-wise (target has to be perfectly aligned with neural_result)
* `--recolor_by_target <bool>`, optional, recolor the final result to have similar colors as the target image
* `--patch_based_source_blur <int>`, optional, specify how much the result is abstract
* `--patch_based_style_weight <float>`, optional, specify whether to follow style or content during the patch based synthesis
* `--patch_based_max_mp <float>`, optional, defines the maximal resolution (in megapixels) on which the patch based synthesis runs 
* `--patch_based_backend <string>`, optional, values are "CPU", "CUDA" or "AUTO"

## Examples
* Once compiled successfully, check and run `examples/wolf/run.bat` or `examples/wolf/run.sh`
* The result image should appear next to the scripts

## <a name="CitingNeurallyGuided"></a>Citing Neurally-Guided-Style-Transfer
If you find Neurally-Guided-Style-Transfer usefull for your research or work, please use the following BibTeX entry.

```
@ARTICLE{Texler20-CAG,
  author  = {Ond\v{r}ej Texler and David Futschik and Jakub Fi\v{s}er and Michal Luk\'{a}\v{c} 
               and Jingwan Lu and Eli Shechtman and Daniel S\'{y}kora},
  journal = "Computers \& Graphics",
  title   = {Arbitrary Style Transfer Using Neurally-Guided Patch-Based Synthesis},
  year    = {2020},
}
```
