# Shortcuts for StyleGAN
Here is a collection of scripts for [StyleGAN3-fun](https://github.com/PDillis/stylegan3-fun) that I wrote so that I could get rolling quickly on different projects. 

## Convert Dataset
`python dataset_tool.py --source=Lightning_512x512 --dest=datasets/Lightning-512.zip --resolution=512x512`

## Train StyleGAN2
```
python train.py --outdir=results --cfg=stylegan2 --metrics=None `
--data=datasets/Lightning-512.zip `
--resume-kimg=0 --kimg=5000 --gamma=10 --mirror=1 --mirror-y=0 --freezeD=0 `
--gpus=2 --batch=32 --batch-gpu=8 --snap-res=8k --img-snap=3 --snap=3 `
--resume=externalmodels/stylegan2-ffhq-512x512.pkl
```

## Train StyleGAN3
```
python train.py --outdir=results --cfg=stylegan3-t --metrics=None `
--data=datasets/Lips-512.zip `
--resume-kimg=0 --kimg=5000 --gamma=80 --mirror=1 --mirror-y=0 `
--gpus=2 --batch=32 --batch-gpu=8 --snap-res=8k --img-snap=1 --snap=3 `
--resume=externalmodels/stylegan3-t-afhqv2-512x512.pkl
```

## Train StyleGAN2-EXT
```
python train.py --outdir=results --cfg=stylegan2-ext --metrics=None `
--data=datasets/Escher-512.zip `
--resume-kimg=0 --kimg=5000 --gamma=80 --mirror=1 --mirror-y=1 --aug=noaug `
--gpus=2 --batch=32 --batch-gpu=8 --snap-res=8k --img-snap=1 --snap=3 `
--resume=externalmodels/StyleGAN2Extended-Aydao-AnimeDanbooru2019s-512x512-5268480kimg.pkl
```
- Due to the delicate changes introduced, StyleGAN3-Extended is very sensitive to the transfer learning process. You must start with a large gamma (80) and then later reduce to gamma (10), otherwise the model will be shocked and likely collapse.

## StyleGAN2: 256x256 Model Training
```
python train.py --outdir=results --cfg=stylegan2 --metrics=None `
--data=datasets/Chrome-256.zip --cbase=16384 `
--resume-kimg=0 --kimg=5000 --gamma=10 `
--gpus=2 --batch=32 --batch-gpu=8 --img-snap=3 --snap=6 `
--resume=externalmodels/stylegan2-ffhq-256x256.pkl
```
- When training a 256x256 model, you must include this attribute: `--cbase=16384`
- Doing test runs on a new dataset using a 256x256 model is an excellent way to run tests of what is the best value for Gamma and save valuable render time. After you've determined the best Gamma value for the 256x256 model, then just multiply the Gamma value by 4 and then use it for the 512x512 model. For instance: Gamma=0.8192 for 256x256 would become Gamma=3.2768 for 512x512.
- "As a rule of thumb, the value of `--gamma` scales quadratically with respect to the training set resolution: doubling the resolution (e.g., 256x256 → 512x512) means that `--gamma` should be multiplied by 4 (e.g., 2 → 8)."

## Generate Seed Images
```
python gen_images.py --outdir=Chrome512_truc0P7_1060kimg --trunc=0.7 `
--seeds=1-5000 `
--network=externalmodels/stylegan2-ffhq-512x512.pkl
```

## Generate Latent Seed Walk Video
```
python gen_video.py `
--output=videos/Mushroom512_SG2_truc0p7_256kimg.mp4 `
--stabilize-video --trunc=0.7 --grid=1x1 --w-frames=180 `
--seeds=100-110 `
--network=externalmodels/stylegan2-ffhq-512x512.pkl; `
```
- 60 w-frames = 1 second /// aka the time tweening between keyframes /// 120 seeds = 2 minutes
- 180 w-frames is useful for smooth motion /// 40 seeds = 2 minutes
- 360 w-frames is useful for medium motion /// 30 seeds = 3 minutes
- 720 w-frames is useful for slow motion /// 30 seeds = 6 minutes
- Need to auto randomize the order of the seeds? `--shuffle-seed=1`

## Generate and Visualize "Internal Representation" of Model (SG3 models only)
### First you must list the available internal layers that can be visualized, then plug in the results into the next step.
`python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t --available-layers --seeds=0`

### Render Test Image of "Internal Representation"
- Ignore the errors, the image will render anyways...
```
python generate.py images --network=ffhq1024 `
--seeds=0 --trunc=0.7 --anchor-latent-space --rgb=True --starting-channel=21 --layer=L10_1044_81 `
--description= --outdir=videos
```

### Render Video of "Internal Representation"
- Since the visuals move slowly, use 30fps and a long duration-sec... Then speed up in post to 60fps
- The `--duration-sec` must be >10.0 or it will result in frozen video
- Use the `--description` to add notes, such as the starting-channel and seed number. I find this is useful for production purposes.
```
python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t `
--layer=L7_276_323 --seeds=0 --starting-channel=0  --description= `
--trunc=0.7 --anchor-latent-space --rgb=True `
--slowdown=1 --duration-sec=240.0 --fps=30 `
--outdir=videos; `
```

## Generate "Flesh Digressions" Video
```
python generate.py circular-video --outdir=videos `
--flesh --seed=100 --trunc=0.7 `
--duration-sec=480 --fps=15 `
--grid-width=1 --grid-height=1 --noise-mode=none `
--description=Test1  `
--network=externalmodels/stylegan2-ffhq-512x512.pkl; `
```
- Since the visuals move slowly, use 15fps and a long duration-sec (such as 480)... Then speed up in post to 60fps to make 2 minutes of footage.
- `--anchor-latent-space` will change the look, but not really useful.

## Blend Together Two Different StyleGAN2 Models
```
python blend_models.py `
--model_res 512 `
--lower_res_pkl modelsss/graffiti.pkl `
--split_res 32 `
--higher_res_pkl modelsss/faces.pkl `
--output_path blendedmodels/Graffiti-Faces_SplitAt64_512x512.pkl
```
- https://medium.com/@adamcole.studio/network-blending-user-interface-135bad23dd9c
- Use this repo: https://github.com/Sxela/stylegan3_blending

## Train or Generate on a Specific GPU
Useful if you have a computer with multiple GPUs.

`cmd /C "set CUDA_VISIBLE_DEVICES=0 && python train.py --outdir=results --cfg=stylegan2 --metrics=None --data=datasets/Graffiti-512.zip --kimg=5000 --gamma=10 --gpus=1 --batch=32 --batch-gpu=8 --resume=externalmodels/stylegan2-ffhq-512x512.pkl"`

`cmd /C "set CUDA_VISIBLE_DEVICES=1 && python train.py --outdir=results --cfg=stylegan2 --metrics=None --data=datasets/Graffiti-512.zip --kimg=5000 --gamma=10 --gpus=1 --batch=32 --batch-gpu=8 --resume=externalmodels/stylegan2-ffhq-512x512.pkl"`

`cmd /C "set CUDA_VISIBLE_DEVICES=0,1 && python train.py --outdir=results --cfg=stylegan2 --metrics=None --data=datasets/Graffiti-512.zip --kimg=5000 --gamma=10 --gpus=2 --batch=32 --batch-gpu=8 --resume=externalmodels/stylegan2-ffhq-512x512.pkl"`
