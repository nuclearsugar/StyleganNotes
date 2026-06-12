## StyleGAN3-Fun Installation Instructions (CUDA 11.3)
_BEWARE: These notes are from 2022 and I'm not sure how useful or applicable they are anymore_

1. Install VisualStudioSetup2019.exe  
--- Install package: Desktop Development with C++  
--- Install package: Python Development

2. Execute BAT script:  
C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat

3. REBOOT

4. Install cuda_11.3.0_465.89_win10.exe  
--- This will replace the currently installed GPU driver, which seemingly is the latest version plus the CUDA toolkit  
--- Need to uninstall any other CUDA Toolkit versions first

5. REBOOT

6. Install Miniconda3-py39_22.11.1-1-Windows-x86_64.exe

7. REBOOT

8. Open "Anaconda Powershell Prompt"

9. Extract ZIP to desktop:  
stylegan3-fun.zip

10. Navigate to folder within the Powershell prompt:  
`cd C:\Users\Zenith\Desktop\stylegan3-fun`

11. WITHIN <environment.yml> NEED TO CHANGE THE FOLLOWING CODE:  
`nvidia::cudatoolkit=11.3`  
TO:  
`cudatoolkit=11.3`

12. Run command:  
`conda env create -f environment.yml`

13. When done, run command:  
`conda activate stylegan3`

14. If this folder exists, then delete it:  
C:\Users\Zenith\AppData\Local\torch_extensions

15. Try doing a training session. If you see the error below, then manually create folders for this full path: `<C:\Users\Zenith\AppData\Local\Temp\torch\kernels>`

C:\Users\Zenith\Desktop\stylegan3-fun-main\training\augment.py:231: UserWarning: Specified kernel cache directory could not be created! This disables kernel caching. Specified directory is  C:\Users\Zenith\AppData\Local\Temp/torch/kernels. This warning will appear only once per process. (Triggered internally at  C:\cb\pytorch_1000000000000\work\aten\src\ATen\native\cuda\jit_utils.cpp:860.)  
  s = torch.exp2(torch.randn([batch_size], device=device) * self.scale_std)

17. All done! Ready to play with StyleGAN2 or 3

==========================================

When trying to render out video using the <gen_video.py> script, I saw this error:  
`"OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized."`

To solve this and allow the code to continue running, add the following to the Windows environment variables:  
```
Variable Name: KMP_DUPLICATE_LIB_OK  
Variable Value: TRUE
```

==========================================

DOCUMENTATION OF THINGS LEARNED... MANY HOURS SPENT GETTING THIS TO FUNCTION  
--- Must use Visual Studio 2019, since Visual Studio 2022 does not link correctly to the CUDA Toolkit 11.1  
--- Must use Python 3.9  
--- Must use CUDA Toolkit 11.1  
--- VERY HELPFUL = https://github.com/NVlabs/stylegan3/issues/103  
--- VERY HELPFUL = https://github.com/PDillis/stylegan3-fun/blob/main/docs/troubleshooting.md#why-is-cuda-toolkit-installation-necessary  
--- VERY HELPFUL = https://github.com/PDillis/stylegan3-fun/issues/7  
--- https://github.com/NVlabs/stylegan2-ada-pytorch/issues/155  
--- https://github.com/NVlabs/stylegan3/issues/88  
--- https://www.youtube.com/watch?v=BCde68k6KXg  
--- https://towardsdatascience.com/generating-your-own-images-with-nvidia-stylegan2-ada-for-pytorch-on-ampere-a80fab52d6b5
