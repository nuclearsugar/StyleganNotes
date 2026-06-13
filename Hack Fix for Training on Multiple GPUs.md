# Hack Fix for Training on Multiple GPUs

More info regarding this bug: https://github.com/PDillis/stylegan3-fun/issues/33

> When attempting to run the [StyleGAN3-fun](https://github.com/PDillis/stylegan3-fun) repo, you may run into the training stalling when attempting to train. It will just look like it's loading indefinitely. I believe this is due to the initial GPU:0 locking out access to bias_act.pyd and similiar StyleGAN3 custom cuda kernels plugins.
> 
> To fix this and enable training, you must create duplicate some of the standalone files of these plugins. I did this in the following way for (x2) GPUs:
> 
> in the custom_ops.py file starting after line 138:
> ```
> try:
>     torch.utils.cpp_extension.load(name=module_name, build_directory=cached_build_dir,
>         verbose=verbose_build, sources=cached_sources, **build_kwargs)
>     module = importlib.import_module(module_name)
> except:
>     print('forcing secondary ' + module_name)
> 
>     torch.utils.cpp_extension.load(name=module_name+'_2', build_directory=cached_build_dir,
>                                    verbose=verbose_build, sources=cached_sources, **build_kwargs)
>     module = importlib.import_module(module_name+'_2')
> ```
> 
> Now navigate to the following directory:  
> C:\Users\"YourUserName"\AppData\Local\torch_extensions\torch_extensions\Cache\py38_cu116\
> 
> Here, you will find 3 plugin folders that were created during your initial attempt. Create copies of these folders in the same directory but add "_2" to the end of each folder name.
> 
> Now when you run the model with multiple GPUs, once the model encounters the situation where a plugin load has failed, it will try the secondary plugin that you have just created and will succeed.
> 
> Feel free to automate this process if you are running with GPUs >2 but this workaround should work. Note that the initial setup may take about 1-5min longer than before.

Source - https://github.com/NVlabs/stylegan3/issues/218
