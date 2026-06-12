## Internal Representation Renders

Rendering out videos using the "Internal Representation" mode is really interesting because you get to see the inner layers of the model, which for me partially reveals what's going on within the model, particularly if you render all videos using the same seed and them composite together tastfully in After Effects. 

But setting up the interpolation render code was a bit annoying... So I saved it for posterity. I doubt it's useful to anyone but here it is:

<hr style="border: none; border-top: 1px solid #d0d7de;">

Render Video - Internal Representation:  
ALL 1 SEED ON DIFFERANT LAYERS AND CHANNELS

```
!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=0  --description=Seed0-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=3  --description=Seed0-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=6  --description=Seed0-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=9  --description=Seed0-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=12  --description=Seed0-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=15  --description=Seed0-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=18  --description=Seed0-Channel-18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=0 --starting-channel=21  --description=Seed0-Channel20-21-22 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=0  --description=Seed0-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=3  --description=Seed0-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=6  --description=Seed0-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=9  --description=Seed0-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=12  --description=Seed0-Channel-12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=15  --description=Seed0-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=18  --description=Seed0-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=0 --starting-channel=21  --description=Seed0-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=0  --description=Seed0-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=3  --description=Seed0-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=6  --description=Seed0-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=9  --description=Seed0-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=12  --description=Seed0-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=15  --description=Seed0-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=18  --description=Seed0-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=0 --starting-channel=21  --description=Seed0-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=0  --description=Seed0-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=3  --description=Seed0-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=6  --description=Seed0-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=9  --description=Seed0-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=12  --description=Seed0-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=15  --description=Seed0-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=18  --description=Seed0-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=0 --starting-channel=21  --description=Seed0-Channel20-21-22 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=0  --description=Seed0-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=3  --description=Seed0-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=6  --description=Seed0-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=9  --description=Seed0-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=12  --description=Seed0-Channel-12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=15  --description=Seed0-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=18  --description=Seed0-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=0 --starting-channel=21  --description=Seed0-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=0  --description=Seed0-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=3  --description=Seed0-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=6  --description=Seed0-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=9  --description=Seed0-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=12  --description=Seed0-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=15  --description=Seed0-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=18  --description=Seed0-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=0 --starting-channel=21  --description=Seed0-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/SameSeed
```

<hr style="border: none; border-top: 1px solid #d0d7de;">

Render Video - Internal Representation:  
ALL DIFFERENT SEEDS, LAYERS, CHANNELS

```
!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=100 --starting-channel=0  --description=Seed100-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=101 --starting-channel=3  --description=Seed101-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=102 --starting-channel=6  --description=Seed102-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=103 --starting-channel=9  --description=Seed103-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=104 --starting-channel=12  --description=Seed104-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=105 --starting-channel=15  --description=Seed105-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=106 --starting-channel=18  --description=Seed0106-Channel-18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L6_148_512 --seeds=107 --starting-channel=21  --description=Seed107-Channel20-21-22 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=108 --starting-channel=0  --description=Seed108-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=109 --starting-channel=3  --description=Seed109-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=110 --starting-channel=6  --description=Seed110-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=111 --starting-channel=9  --description=Seed111-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=112 --starting-channel=12  --description=Seed112-Channel-12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=113 --starting-channel=15  --description=Seed113-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=114 --starting-channel=18  --description=Seed114-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L7_276_323 --seeds=115 --starting-channel=21  --description=Seed115-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=116 --starting-channel=0  --description=Seed116-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=117 --starting-channel=3  --description=Seed117-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=118 --starting-channel=6  --description=Seed118-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=119 --starting-channel=9  --description=Seed119-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=120 --starting-channel=12  --description=Seed120-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=121 --starting-channel=15  --description=Seed121-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=122 --starting-channel=18  --description=Seed122-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L8_276_203 --seeds=123 --starting-channel=21  --description=Seed123-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=124 --starting-channel=0  --description=Seed124-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=125 --starting-channel=3  --description=Seed125-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=126 --starting-channel=6  --description=Seed126-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=127 --starting-channel=9  --description=Seed127-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=128 --starting-channel=12  --description=Seed128-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=129 --starting-channel=15  --description=Seed129-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=130 --starting-channel=18  --description=Seed130-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L9_532_128 --seeds=131 --starting-channel=21  --description=Seed131-Channel20-21-22 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=132 --starting-channel=0  --description=Seed132-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=133 --starting-channel=3  --description=Seed133-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=134 --starting-channel=6  --description=Seed134-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=135 --starting-channel=9  --description=Seed135-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=136 --starting-channel=12  --description=Seed136-Channel-12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=137 --starting-channel=15  --description=Seed137-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=138 --starting-channel=18  --description=Seed138-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L10_1044_81 --seeds=139 --starting-channel=21  --description=Seed139-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=140 --starting-channel=0  --description=Seed140-Channel0-1-2 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=141 --starting-channel=3  --description=Seed141-Channel3-4-5 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=142 --starting-channel=6  --description=Seed142-Channel6-7-8 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=143 --starting-channel=9  --description=Seed143-Channel9-10-11 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=144 --starting-channel=12  --description=Seed144-Channel12-13-14 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=145 --starting-channel=15  --description=Seed145-Channel15-16-17 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=146 --starting-channel=18  --description=Seed146-Channel18-19-20 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed

!python generate.py random-video --network=ffhq1024 --cfg=stylegan3-t \
--layer=L11_1044_51 --seeds=147 --starting-channel=21  --description=Seed147-Channel21-22-23 \
--trunc=1.0 --anchor-latent-space --rgb=True \
 --slowdown=1 --duration-sec=240.0 --fps=30 \
--outdir=/content/drive/MyDrive/AI/colab-sg3-videogenA/stylegan3-fun/videos/DiffSeed
```
