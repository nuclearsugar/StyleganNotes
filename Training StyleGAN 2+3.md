# My Experience with Training StyleGAN2+3
Training and fine-tuning StyleGAN models is nearly undocumented. It is very slow and delicate to get working. But when it does, it makes quite unique visuals.

## My Notes On Training
- Here is a summary of my findings regarding each useful attribute when training with the [StyleGAN3-fun](https://github.com/PDillis/stylegan3-fun) repo.
- Batch-GPU: Increase the `Batch-GPU` to whatever the GPU VRAM will allow for. This will decrease the training time. For example 16GB: `batch-gpu=8` and 40GB: `batch-gpu=32`
- Batch: I always set `batch=32` due to VRAM limitations. Changing the Batch will also affect the Gamma.
- InitStrength: If you're resuming a transfer learning session and you still have the logs from the prior training run, then you can input the last known augmentation value. This will speed up the initial training since it doesn't need to find the augmentation equilibrium over 7 to 10 ticks from starting at zero and instead just starts off right from what value is manually input. Although this seems to introduce some artifacts sometimes and so I've avoided using it.
- Resume-kimg: Use `Resume-kimg` to pick up from a prior training session or begin transfer learning from any model.
- Mirror X: horizontal flip.
- Mirror Y: vertical flip. Not advised if there is a right-side up within the images of your dataset.
- Learning Rate: The learning rate for the discriminator is set by default to `--dlr=0.002`. But if you have a dataset with tons of variation, try lowering the learning rate to `--dlr=0.001` and see what happens. This will slow down the training process yet allow the model to stablize. I have not tested this yet.
- BlurPercent: I have not yet experimented with this attribute yet, but seems like it would solve the bubble problem that I experienced while training the Chimpanzee512 model since it contained lots of detail. `--blur-percent` Blur both real and generated images before passing them to the Discriminator. The blur `blur_init_sigma=10.0` will completely fade after the selected percentage of the training is completed (using a linear ramp). Another experimental feature, should help with datasets that have a lot of variation, and you wish the model to slowly learn to generate the objects and then its details.
- Augmentations: use with the default value unless you have at least 40,000 images in your dataset and then you can disable augmentations `aug=noaug` for improved convergence.
- Augmentations: "Specifying `--aug=noaug` disables adaptive discriminator augmentation (ADA), which may improve the results slightly if the training set is large enough (at least 100k images when accounting for x-flips). With small datasets (less than 30k images), it is generally a good idea to leave the augmentations enabled." - https://github.com/NVlabs/stylegan3/blob/main/docs/configs.md
- 512x512 datasets produce the best results. 1024x1024 datasets doubles training time and is therefore more difficult to nail down the gamma settings needed.
- StyleGAN3 isn't very forgiving with small datasets and produces less desirable interpolation compared to StyleGAN2. It also takes double the time to train compared to StyleGAN2. Unless you have a dataset that is highly self similar, stick with StyleGAN2.
-  The organization of the image dataset will seemingly affect the training of the GAN. Or at least for my small fine-tuning training runs. I prepared a dataset containing ~73,000 images of graffiti and the images are currently organized by certain themes. For example there are 562 in a red spiky theme, 894 in a blue flowy theme, 345 in a green blocky theme, and remain in this grouped fashion when alphanumerically ordered. So I performed 2 training tests: 1 organized dataset and 1 randomized dataset. They each ended up with very different results after training. The organized dataset converged within 100kimg, while the randomized dataset was a mess.
- If it's getting stuck at the step: `Setting up PyTorch plugin "bias_act_plugin"...` then delete: <C:\Users\<username>\AppData\Local\torch_extensions\torch_extensions\Cache> and then re-run StyleGAN3 python code.
- Useful training notes here - https://github.com/l4rz/practical-aspects-of-stylegan2-training - and - https://gwern.net/face - and - https://towardsdatascience.com/stylegan-v2-notes-on-training-and-latent-space-exploration-e51cf96584b3 - and - https://rpubs.com/JonasKnecht/665744
- I always start with the FFHQ model for transfer learning. After watching a workshop from Derrick Schultz, he emphasized that since Nvidia heavily trained these models to act as their "tour de force" and so these models received about 70 days of training time equivalent to x1 GPU. And so the neural network is highly developed, much more so than basically any other model available. Also the amount of backgrounds within the Flicker Faces HQ dataset is extreme and so the transfer learning process is therefore forgiving. - https://github.com/NVlabs/stylegan2?tab=readme-ov-file#training-networks
- If retraining a SG2 512x512 dataset then use - https://api.ngc.nvidia.com/v2/models/nvidia/research/stylegan2/versions/1/files/stylegan2-ffhq-512x512.pkl
- If retraining a SG2 1024x1024 dataset then use - https://api.ngc.nvidia.com/v2/models/nvidia/research/stylegan2/versions/1/files/stylegan2-ffhq-1024x1024.pkl
- If retraining a SG3 512x512 dataset then use - https://api.ngc.nvidia.com/v2/models/nvidia/research/stylegan3/versions/1/files/stylegan3-t-afhqv2-512x512.pkl

## Notes On Training In Regards To Gamma
- It is important to note that SG2 and SG3 have very different needs when it comes to the Gamma value. "The optimal value is usually the same for `--cfg=stylegan3-t` and `--cfg=stylegan3-r`, but considerably lower for `--cfg=stylegan2`" - https://github.com/NVlabs/stylegan3/blob/main/docs/configs.md
- For SG2, `gamma=10` is a good starting point for 512x512 datasets. But if the dataset is too diverse then the model will have trouble converging. If the dataset has lots of variation then first fine-tune the Generator so that it will create fake but accurate images to feed into the Discriminator, otherwise the model can collapse or never converge. So use `gamma=80` to smooth out too much variety in the dataset. Second, after that the model has been transfer learned to the dataset, it’s time to further fine-tune train it. So set `gamma=10` now the Generator can now accept the variety in the dataset and will be able to converge better. Futher on, you can perhaps set `gamma=5` or `gamma=1` to get even better variation in the output seeds of the model.
- Useful Gamma examples from Nvidia can found here - https://github.com/NVlabs/stylegan3/blob/main/docs/configs.md - and here - https://github.com/NVlabs/stylegan2-ada-pytorch/blob/main/train.py#L154
- When trying to find the ideal Gamma value, "Try increasing the value by 2x and 4x, and also decreasing it by 2x and 4x."
https://github.com/NVlabs/stylegan3/blob/main/docs/configs.md#old-stylegan2-ada-configurations
- For unknown reasons Nvidia suggests using multiples of 8 for the Gamma value, hence the strange values: 13.1072, 6.5536, 3.2768, 1.6384, 0.8192 - I am not sure if it really matters to use these precise values or whole numbers.
- If no value is manually input for Gamma, then it will be automatically determined by the following formula: 
`Gamma = 0.0002 * (Resolution^2) / Batch`. For the 512x512 model resolution that I typically work at, this translates to Gamma=1.6384, which is interesting since it's much lower than I've ever found remotely useful.

## NVIDIA Notes On Training In Regards To Gamma
The most important hyperparameter that needs to be tuned on a per-dataset basis is the R1 regularization weight, `--gamma`, that must be specified explicitly for train.py. As a rule of thumb, the value of `--gamma` scales quadratically with respect to the training set resolution: doubling the resolution (e.g., 256x256 → 512x512) means that `--gamma` should be multiplied by 4 (e.g., 2 → 8). The optimal value is usually the same for `--cfg=stylegan3-t` and `--cfg=stylegan3-r`, but considerably lower for `--cfg=stylegan2`.

In practice, we recommend selecting the value of `--gamma` as follows:
- Find the closest match for your specific case in this document (config, resolution, and GPU count).
- Try training with the same `--gamma` first.
- Then, try increasing the value by 2x and 4x, and also decreasing it by 2x and 4x.
- Pick the value that yields the lowest FID.

https://github.com/NVlabs/stylegan3/blob/main/docs/configs.md

Suggested values for training a 512x512 dataset: (looks familiar? it's a multiple of 16)  
`--gpus=1 --batch=8`  
1.6384 =  /4  
3.2768 = /2  
6.5536 = suggested default  
13.1072 = x2  
26.2144 = x4

Suggested values for training a 1024x1024 dataset: (looks familiar? it's a multiple of 16)  
`--gpus=1 --batch=4`  
13.1072 =  /4  
26.2144 = /2  
52.4288 = suggested default  
104.8576 = x2  
209.7152 = x4

The results may also be improved by adjusting `--mirror` and `--aug`, depending on the training data. Specifying `--mirror=1` augments the dataset with random x-flips, which effectively doubles the number of images. This is generally beneficial with datasets that are horizontally symmetric (e.g., FFHQ), but it can be harmful if the images contain noticeable asymmetric features (e.g., text or letters). Specifying `--aug=noaug` disables adaptive discriminator augmentation (ADA), which may improve the results slightly if the training set is large enough (at least 100k images when accounting for x-flips). With small datasets (less than 30k images), it is generally a good idea to leave the augmentations enabled.

You can select the number of GPUs by changing the value of `--gpu`; this does not affect the convergence curves or training dynamics in any way. By default, the total batch size `--batch` is divided evenly among the GPUs, which means that decreasing the number of GPUs yields higher per-GPU memory usage. To avoid running out of memory, you can decrease the per-GPU batch size by specifying `--batch-gpu`, which performs the same computation in multiple passes using gradient accumulation.

By default, train.py exports network snapshots once every 200 kimg, i.e., the product of `--snap=50` and `--tick=4`. When using few GPUs (e.g., 1–2), this means that it may take a very long time for the first snapshot to appear. We recommend increasing the snapshot frequency in such cases by specifying `--snap=20`, `--snap=10`, or `--snap=5`.

Note that the configurations listed in this document have been specifically tuned for 8 GPUs. The safest way to scale them to different GPU counts is to adjust `--gpu`, `--batch-gpu`, and `--snap` as described above, but it may be possible to reach faster convergence by adjusting some of the other hyperparameters as well. Note, however, that adjusting the total batch size `--batch` requires some experimentation; decreasing `--batch` usually necessitates increasing regularization `--gamma` and/or decreasing the learning rates (most importantly `--dlr`).

## Training In Regards to FreezeD for SG2
- Now that I'm training using much larger dataset (>30,000 images) I think that FreezeD is no longer helpful and is hindering training performance. I believe that when training tiny datasets (<500 images) then it was beenficial to help avoid overfitting at the lowest levels of the model.
- Use `freezed=4` for transfer learning. This freezes the lower levels of the discriminator to improve the fine-tune training process and helps to avoid mode collapse and overfitting in small datasets (aka 5,000 or less images). Overall it improves results, less self repetition, and slightly lowers the training time per tick. The first four layers of the model are very low resolution (4x4, 8x8, 16x16) and do not carry much detail and so it doesn’t need retraining. Plus using `freezed=4` helps the visuals to feel more fluid, possibily because of the extensive training to the FFHQ model and it's therefore maturity. - https://arxiv.org/abs/2002.10964 - https://gwern.net/face#extended-stylegan2-danbooru2019-aydao
- After training has stabilized using `freezed=4` after about 2000 to 3000 kimg, now you can switch over to `freezed=13`. But if you switch to `freezed=13` too early then it will introduce visual artifacts into the model. This will allow the training to render a little bit faster, about 30 seconds per tick. Using `freezed=13` means that only the very last layer of a 512x512 model will recieve training and all of the smaller resolution layers will be frozen during training. I have found this useful for when it seems that I have hit a threshold of the model learning any more details, so instead I just focus on the very last layer and then more detail can be absorded. I believe this is because the layers are connected in a way that smaller resolution layers affect larger resolution layers, and so freezing the smaller layers allows it to train differently. 
- The highest value is `freezed=13`. Any higher values will result in the value being treated as if it were 13. I believe this is because there are only 14 layers within a StyleGAN2 network model.
- Need to test this: "In our experience, `--freezed=10` and `--freezed=13` tend to work reasonably well." - https://github.com/NVlabs/stylegan3/blob/main/docs/configs.md
- Cannot use FreezeD on SG3 when starting up a transfer learning, due to the redesigned internal network compared to SG2. But I think FreezeD can enabled on SG3 when it's stablized and you want to just train on the higher rez layers of the model.

## Train on a Specific GPU
`cmd /C "set CUDA_VISIBLE_DEVICES=0 && python train.py --outdir=results --cfg=stylegan2 --metrics=None --data=datasets/Graffiti-512.zip --kimg=5000 --gamma=10 --gpus=1 --batch=32 --batch-gpu=8 --resume=externalmodels/stylegan2-ffhq-512x512.pkl"`

`cmd /C "set CUDA_VISIBLE_DEVICES=1 && python train.py --outdir=results --cfg=stylegan2 --metrics=None --data=datasets/Graffiti-512.zip --kimg=5000 --gamma=10 --gpus=1 --batch=32 --batch-gpu=8 --resume=externalmodels/stylegan2-ffhq-512x512.pkl"`

`cmd /C "set CUDA_VISIBLE_DEVICES=0,1 && python train.py --outdir=results --cfg=stylegan2 --metrics=None --data=datasets/Graffiti-512.zip --kimg=5000 --gamma=10 --gpus=2 --batch=32 --batch-gpu=8 --resume=externalmodels/stylegan2-ffhq-512x512.pkl"`

## Details From Diego
I asked Diego Porres Bustamante  (maintainer of StyleGAN3-fun) the following:  
The gamma attribute has been giving me trouble during training. It seems to be highly dependent on the dataset being input. Nvidia suggests: "try increasing the value by 2x and 4x, and also decreasing it by 2x and 4x". So far in multiple tests running at 1, 2.5, 100, even still 10 is the best value to use across multiple datasets. Yet I can find little documentation or discussion about the gamma attribute, so I don't understand what it's actually doing. Do you have any tips or thoughts to help me better approach it?

And heard back this:
- Regarding the gamma value, how I approach/view it is as a data distribution manipulator of sorts. That is, imagine your data landscape as having lots and lots of peaks representing the modes, and gamma will make these easier to distinguish or join them all into one. For example, if we take a face dataset, then there will be lots of groups: faces with moustache, red hair, eyeglasses, smiles, etc. If we set a high value of gamma, then all these details disappear and the only distribution that "matters" is that of a face (2 eyes, nose, mouth, hair), so the Generator will effectively lose expressiveness. Setting a low value of gamma does the opposite, and the Generator will be highly expressive.
 The bad thing about setting a low gamma is that the model might not converge or collapse, as is usually the case. For this reason, what I do is I set a really high gamma first (80 or so), as I want the training to first be successful, but also for the Generator to create images in the vicinity of what I want. Then, I resume training from the last checkpoint where I used a large gamma, but now I lower gamma, then do the same iteratively until I get something I like.
- Regarding when to lower the gamma​, it's really an art form. I simply have set a sort of rule to not train for too long, i.e., finetune/train a model with a high gamma for 5000kimg​, and then lower it a lot (go from 80 to 10 for example), and then train for 2000kimg​, then see if things need to be repeated (lowering and longer training).
- If you wanna read more about gamma, here's a quick summary, but this is more math-heavy than perhaps needed: https://paperswithcode.com/method/r1-regularization

About FreezeD
- From what I remember, you should set a higher value for freezeD at the end of Transfer Learning​, and this is what they suggest in the docs: "In our experience, `--freezed=10` and `--freezed=13` tend to work reasonably well." - https://github.com/PDillis/stylegan3-fun/blob/main/docs/configs.md#transfer-learning
- Sorry, was rereading what I said and I meant that, at the end of the "Transfer Learning" section in the configs.md​ file, they say that using `--freeze-d=10`​ or `--freeze-d=13`​ worked best for them from the beginning of training, not at the end of transfer learning itself!

StyleGAN2-Extended
- I'm also adding an extended version of StyleGAN2 (`--cfg=stylegan2-ext`​ when running train.py​), and I'm getting nice results, at the cost of each model being ~1 Gb instead of ~320 Mb. This is a work in progress, so test it if you want, but I haven't really converged to a final version of this. - https://gwern.net/face#extended-stylegan2-danbooru2019-aydao

## Interesting Reading
- Documenting the process of coding StyleGAN2 from scratch. Has some interesting insights.
- The Path to StyleGan2: Implementing the StyleGAN - https://ym2132.github.io/StyleGAN
