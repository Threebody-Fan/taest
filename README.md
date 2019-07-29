# Animate_character Detection
 **利用SSD训练一个动漫人物识别机.**

## 前言
  SSD在物体识别上很成功，很容易产生将它应用在人物识别上的想法。原本打算尝试一下去识别足球运动员，爬一些梅西C罗内马尔等球员的图片去训练，但后来觉得可能只可以识别出球队的队服，即巴萨的梅西和皇马的C罗之间很好识别，但是同样是巴萨队内的梅西，苏牙等等也许就不能很好地分辨了；同时用皇马C罗训练后，应该也无法识别出尤文的C罗。总的来说，**实际人物由于其着装，动作，表情，等等因素，做起来可能相对较难**，相比较之下**动漫人物特征鲜明，变化较少，做起来应该相对容易**，所以诞生了这样一个项目。  

## 模型
  直接用的SSD官方模型：[SSD-master官方说明文档](https://github.com/balancap/SSD-Tensorflow)。此外，对可视化做了一点修改，输出不显示类别代号，直接显示类别名称（对本项目来说，就是人物名称）。  
  
## 数据准备+训练
  一般来讲imageNet上有很多用来训练机器视觉的数据，但动漫这块可能没什么人做（没有做大范围调查，可能有现成的数据库）。所以本文用来训练的图片都是自己从视频里逐帧提取的，剔除一些没有任务的图片后，手动打标签。由于工作量不小，而且瞎眼睛，目前**只有1000张打好标签的图片，且均来自《冰菓》**。（我会把这些数据上传网盘，初步也有扩大这一数据库的想法，毕竟1000张太少了，且人物来源单一，**如果把常见的动漫人物都做一下感觉是个庞大的工程，总之看后续心情慢慢来做，也欢迎有相同兴趣（闲的蛋疼。。。）的同志一起帮忙**)     
 
 数据准备和训练的全过程不在此处详细介绍，All_process.ipynb文件记录了本文准备+训练过程的所有步骤，下载后可以用jupyter notebook打开并可以直接运行，文件内容如下：[**数据准备+训练全过程**](https://github.com/Threebody-Fan/animate-character-detection/blob/master/All_process.ipynb)。    
由于篇幅原因，数据集没有上传至github（后面有网盘链接），关于如何准备自己的数据集也可以参考此文献（本文的训练过程基本按照该文献的步骤实现的）：[如何用SSD训练自己的数据集](https://blog.csdn.net/weixin_39881922/article/details/80569803).  
训练过程相对复杂，要根据自己的数据做很多参数修改，同时为了训练又快又好，又需要调整很多参数，总之很繁琐！另外注意**所有涉及文件路径的都要改为自己的实际路径。**  
由于训练比较耗时间，建议第一次跑把步数调低一点，跑通之后，在调高训练步数。本文用的GPU是GTX1050，跑10000步花了一个晚上（约5~8小时），具体视GPU性能而定，CPU没有试过，应该会非常慢。

## 效果预览
下面是训练好的模型检测的效果。
总的来说，可能还是数据量比较小，女主的识别率较高，男主次之，男二女二最少。此外，找了一些训练集没有出现的角色，也有出现误判的情况。一些检测效果如下所示：  
先来看一些相对较好的识别效果：  
![识别效果](https://github.com/Threebody-Fan/animate-character-detection/blob/master/img1.bmp)  
没什么好说的，单人多人基本都识别出来了，框也画的比较对，就是置信率不太高（女主80左右，男主60左右）。     
  
  
  
 再来看一些识别错误的图片：  
![识别效果](https://github.com/Threebody-Fan/animate-character-detection/blob/master/img2.bmp)   
主要有两种：人物识别不了和人物识别错了。注意图3，5里的角色都没有出现在训练集里，也被当成千反田识别出来了（图3可能是由于京都脸，图5可能是由于水手服）
，且置信率还不低；此外图1错的有点不能理解。。。
## 数据集
如前文所述，将训练用的打好标签的图片上传至网盘：[网盘分享]()提取码：[     ]。  
目前只有《冰菓》的数据，且只有1000张。感觉目前二次元文化毕竟不是主流，ImageNet上并没有这种类别的图片数据，作为二次元和机器学习的两者的爱好者，有必要搞一波二次元图片数据库，希望能把这个数据库不断扩大，也欢迎有同样兴趣的小伙伴加入，当然，如果能找到现成的数据库就更好了，毕竟打标签真的费眼睛。。。
