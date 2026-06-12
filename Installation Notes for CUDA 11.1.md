## STYLEGAN3-FUN INSTALLATION INSTRUCTIONS (CUDA 11.1)

1. Install VisualStudioSetup2019.exe  
--- Install package: Desktop Development with C++  
--- Install package: Python Development  

2. Execute BAT script:
C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat

3. REBOOT

4. Install cuda_11.1.0_456.43_win10.exe  
--- This will replace the currently installed GPU driver, which seemingly is the latest version plus the CUDA toolkit  
--- Need to uninstall any other CUDA Toolkit versions first

5. REBOOT

6. Install Miniconda3-py39_22.11.1-1-Windows-x86_64.exe

7. REBOOT

8. Open "Anaconda Powershell Prompt"

9. Extract ZIP to desktop:  
stylegan3-fun.zip

10. Navigate to folder within the Powershell prompt:  
<cd C:\Users\Zenith\Desktop\stylegan3-fun>

11. Run command:  
<conda env create -f environment.yml>

12. When done, run command:  
<conda activate stylegan3>

13. When done, run:  
<pip install torch===1.9.1+cu111 torchvision===0.10.1+cu111 torchaudio===0.9.1 -f https://download.pytorch.org/whl/torch_stable.html>

14. If this folder exists, then delete it:  
C:\Users\Zenith\AppData\Local\torch_extensions

15. All done! Ready to play with StyleGAN2 or 3

<hr style="border: none; border-top: 1px solid #d0d7de;">

When trying to render out video using the <gen_video.py> script, I saw this error:
"OMP: Error #15: Initializing libiomp5md.dll, but found libiomp5md.dll already initialized."

To solve this and allow the code to continue running, add the following to the Windows environment variables:
Variable Name: KMP_DUPLICATE_LIB_OK
Variable Value: TRUE

<hr style="border: none; border-top: 1px solid #d0d7de;">

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
