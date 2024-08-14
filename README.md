## Introduction

this repo modifies different gaussian splatting models for individual use, but I will be delighted if you find it useful :)

### 1, gaussian splatting to read .txt from COLMAP

**precondition:** make sure the 3dgs/2dgs environment has been setup

​		3dgs repo: https://github.com/graphdeco-inria/gaussian-splatting

​		2dgs repo: https://github.com/hbb1/2d-gaussian-splatting

**existing setup:** 3dgs and 2dgs are excellent works in the field of gaussian splatting. the original 3dgs and 2dgs read the dataset in COLMAP format, specifically from `cameras.bin` & `images.bin` & `points3D.bin` in `{datapath}/sparse/0`

**my requirement:** I need the 3dgs and 2dgs to read .txt format without error, the .txt can be generated from `params.npz`(from SplaTAM) to transform the online output data to offline input data

**my modification:** not let the colmap_loader read the `element[7]` in `point3D.txt` for it latter has no use and the `params.npz` can not generate this information

**what you need do:** just replace the raw scene/colmap_loader.py with mine

**how to use:** the commands are the same as 3dgs/2dgs

### 2，gs_viewer to render depth video

**precondition:** make sure the gaussian splatting lightning environment has been setup

​		`gaussian splatting lightning` repo: https://github.com/yzslab/gaussian-splatting-lightning

**existing setup:** `gaussian splatting lightning` is a wonderful viewer integrated with many gaussian models, and we can use the remote viewer to edit model or generate videos

**my requirement:** I need to render .mp4 depth video with the selected viewpoints, but the current render just suitable for rgb video render

**my modification:** add an extra args --render_depth to generate depth video, currently only adaptive to vanilla 3dgs and 2dgs

**what you need do:** clone my repo under gs_viewer/gs_lightning and use the env for raw `gaussian splatting lightning`

or you can also replace the modified files: `./render.py` & `./viewer.py` & `./internal/viewer/renderer.py`

**how to use:** you can get the depth video by adding --render_depth to the generated commands, other commands are the same as `gaussian splatting lightning`

for example: 

to render 3dgs rgb video

```
python render.py {output model path} --camera-path-filename {camera poses json path} --output-path {video output path}
```

to render 3dgs depth video

```
python render.py {output model path} --camera-path-filename {camera poses json path} --output-path {video output path} --render_depth
```

to render 2dgs rgb video

```
python render.py {output model path} --camera-path-filename {camera poses json path} --output-path {video output path} --vanilla_gs2d
```

to render 2dgs depth video

```
python render.py {output model path} --camera-path-filename {camera poses json path} --output-path {video output path} --vanilla_gs2d --render_depth
```