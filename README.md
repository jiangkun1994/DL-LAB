# Google Cloud Platform  
因为小组都是中国人，就不用英文写了，我总是觉得用英语看这些复杂的东西有时候很费解。而且我也是第一次用这玩意儿，好多地方也是不太清楚，具体会在后面说明。  
## 配置说明  
此次GCP配置是配置了提供给GitHub项目[faster_rcnn](https://github.com/Kelicious/faster_rcnn)的环境。  
## 配置步骤  
1. 因为我已经帮大家创立好了在GCP上面的VM，所以大家不需要再创建了，否则之前那个会自动删掉（昨天我没删除TA帮创建的，后面一刷新，莫名奇妙的不见了），包括已配置的环境也会删掉，**所以谨慎重新创建**。  
2. 大家先用自己的gmail在[Google Cloud](https://cloud.google.com/)上注册云帐号，然后点击左上角的“三条杠”可以看到有个`Compute Engine`，然后点进去就可以看到我们自己的虚拟机了。详细操作可以参考[Google Cloud Tutorial](http://cs231n.github.io/gce-tutorial/)。  
3. 下面是如何使用这个虚拟机，如同孙玮说的，这个虚拟机没有具体的人机交互界面，也就是类似桌面这些东西，所以下载东西有时候有点奇怪，比如我就不知道如何从google drive上面下大于100M的东西，所以昨天我是从本机上传来的，还好不大，不然会费很多时间。下载其余的压缩包啊，GitHub上面的项目啊，都和linux一样，比如`wget`和`git clone`这些都可以用。所以如何打开这个虚拟机的命令行呢，有两种方法：  
- 点击第二步界面里`连接`下面的`SSH`，单击或双击都行，因为有时候会卡，弹出来就行。然后此时就是这个虚拟机的终端了，里面存的东西大家应该都是一样的，像GitHub一样。*（推荐此方法）*  
- 第二种方法是用自己的电脑端链接GCP的虚拟机，这个方法可以参考[Google Cloud Tutorial](http://cs231n.github.io/gce-tutorial/)，但是我不推荐，不知道是不是我操作的原因，我本地电脑端链接后，里面的东西并不和GCP上的虚拟机里的东西一样，所以这个也是我遇到的问题。  
4. 关于操作界面，如果我们在这上面进行深度学习的话，很多东西应该是可以用`Anaconda`来显示的，比如用`jupyter notebook`。但是我不确定，我跑的这个项目最后结果是什么样子的。  
## 已配置环境  
- Anaconda3  
- 利用[faster_rcnn](https://github.com/Kelicious/faster_rcnn)创立了`faster_rcnn`的虚拟环境，并按照项目的要求配置了所需要的依赖库，包含了很多了东西，具体见项目里的`environment.ec2.yml`文件。  
- NVIDIA DRIVER 390版本  
## 如何跑？  
1. 点击`SSH`，弹出窗口后，运行指令`source activate faster_rcnn`。
2. 进入项目里，`cd faster_rcnn`。  
3. 按照项目里的训练过程进行跑（需要下的东西我都下好了，weights以及图片我都下好并且放置在要求的地方了）。  
4. 比如跑第一个指令`python faster_rcnn/train_rpn_step1.py --voc_paths $VOC_ROOT/VOC2007/,$VOC_ROOT/VOC2012/ --phases 60000:1e-3,20000:1e-4 --optimizer sgd --img_set trainval --network resnet50 --anchor_scales 128,256,512 --resize_dims 600,1000 --save_weights_dest models/rpn_weights_r50_fullreg_step1_voc20072012_trainval.h5 --save_model_dest models/rpn_model_r50_fullreg_step1_voc20072012_trainval.h5 2>&1 | tee train_r50_rpn_step1_tmp` 注意，我只下了VOC2007的数据，等以后我们需要再下其他的，所以这个指令你得删掉`,$VOC_ROOT/VOC2012/`，嘻嘻。  
5. 不想跑了的话，运行`source deactivate`退出虚拟环境，然后输入`exit`退出界面。  
6. **ATTENTION!不使用的话请记住把我们的虚拟机这个instance点击停止！**，具体操作为点击`SSH`旁白的三个点，里面有`stop`。然后请静待一会儿，直到看到停止为止，不然会没钱了，哭唧唧。
