# Big Picture of Working with StyleGAN2+3

I've found the Youtube workshops and Google Colab Notebooks from [Derrick Schultz](https://www.patreon.com/cw/bustbright) to be very helpful in laying the foundational knowledge of working with StyleGAN2 in the Google Colab cloud. These workshops are seriously a goldmine for this kind of experimenting with StyleGAN2, I can't emphasize that enough. This one particular workshop helped me out immensely: https://www.youtube.com/watch?v=LArTgflsL98

### Here's the big picture of the workflow for StyleGAN2/3:
1. Create a 512x512 image dataset. 1,000 images is the absolute minimum. 10,000 to 50,000 images is preferable and will create a more flexible model. I use Stable Diffusion to generate these image datasets.
2. Use the FFHQ-512x512 pre-trained model supplied by Nvidia and then transfer learn it to your dataset for between 8 to 48 hours, or longer if you're able!
4. Render out between 1,000 to 10,000 seed images using your newly trained model. Curate the best images and assemble them into the desired order. Use that to make a sequential list of the seed numbers in text form.
5. Plug in the seed numbers and render out a latent walk video using the same newly trained model.
6. Take the videos into the 'Topaz Video AI' app and uprez from 512x512 to 2048x2048.

### Tips
- I use the FFHQ-512x512 pre-trained model from Nvidia and fine-tune it on my datasets. Then pick out the best PKL models and render out the latent walk videos.
- After much experimenting, I'd found that the StyleGAN3 codebase is more mature, even better is the [StyleGAN3-fun](https://github.com/PDillis/stylegan3-fun) codebase, and luckily it still supports the StyleGAN2 approach. Personally I prefer the StyleGAN2 approach to how it morphs visually, it trains about x2 faster, and the generated video seems to be smoother.
- One thing that kept tripping me up is that the image dataset resolution (512x512 is ideal currently) must match the PKL pre-trained model (FFHQ-512x512.pkl) from Nvidia. Otherwise it will throw a cryptic error when trying to train.
- Another thing is that the image dataset requirements are kinda strict. They must all be exactly cropped or resized to 512x512 pixels. They must all be RGB 8-bit images without an alpha channel. If the image is CMYK or index color then it'll throw a cryptic error. So if you're gathering a bunch of images from Google or Flickr, then Photoshop Actions are very helpful to streamline this process. Or ImageMagick via command line.
- You can of course run all of this locally on your computer if you have a good GPU. It's a pain in the ass to get StyleGAN3-fun repo working smoothly.
- I haven't seen much shared about training with really tiny datasets. I've found that the 1000 to 2000 image datasets end up with a decent amount of interpolative potential. Yet for the 200 to 500 range of image datasets I had to ride the line of avoiding mode collapse by hand selecting the seeds prior to rendering out the latent walk video. In other words, the generated visuals would start to repeat itself and so I'd overcome that by hand selecting and arranging the gems. I've been outputting between 10,000 and 50,000 images from Stable Diffusion and getting very good results, but the text prompt must be very concise so that the visuals are strictly visualizing a certain thing. If you're curious about using SD with SG2, check out my tech notes for the [Graffiti Reset](https://www.jasonfletcher.info/vjloops/graffiti-reset.html) VJ pack.
