# 视频信息隐藏系统
这是一款用于进行视频信息隐藏的系统，支持以下功能：
* 多媒体文件播放
* 基于文件的信息隐藏
* 基于文件的信息提取
* 通过配置文件进行算法选择
* 日志记录系统
* 视频信息隐藏/提取的进度显示
    * 进度条显示
    * 控制台进度描述
* 选择信息隐藏/提取算法
    * 三维低码率增长信息隐藏
    * 参考像素多分类的QDCT域信息隐藏
    * 基于N维立方编码的信息隐藏
    * 低码率增长信息隐藏
    * 适应拖尾系数信息隐藏
    * 三元码信息隐藏

## 一、目录结构
```
├── application/green   # 应用程序绿色版本
|       ├── workspace       # 应用程序工作空间(程序运行必需)
|       |       ├── algorithms      # 算法文件夹(程序运行必需)
|       |       |       ├── A算法           # A算法程序文件夹(程序运行必需)
|       |       |       |   ├── workspace       # A算法工作空间(程序运行必需)
|       |       |       |   ├── lencod.exe      # 嵌入应用程序(程序运行必需)
|       |       |       |   └── ldecod.exe      # 提取应用程序(程序运行必需)
|       |       |       |
|       |       |       ├── B算法           # B算法程序文件夹(程序运行必需)
|       |       |       |   ├── ...
|       |       |       |   ├── ...
|       |       |       |   └── ...
|       |       |       |
|       |       |       ├── decoder.cfg     # 解码配置文件(程序运行必需)
|       |       |       └── encoder.cfg     # 解码配置文件(程序运行必需)
|       |       |
|       |       ├── tmp             # 临时文件夹(程序运行必需)
|       |       ├── app.cfg         # 应用程序配置文件(程序运行必需)
|       |       └── test            # 用于测试多媒体文件
|       |
|       └── vih.exe         # 视频信息隐藏系统的可执行程序
|
├── ffmpeg              # FFMPEG库目录。仓库中本没有该目录，需要进行相关开发，需要添置该目录。
├── inc                 # 视频信息隐藏头文件
├── src                 # 视频信息隐藏cpp文件
├── material            # 文档材料
└── sln                 # 视频信息隐藏系统解决方案/工程文件, 开发入口.
```

## 二、依赖
### 1.*FFMPEG*
FFMPEG是一款多媒体操作框架，可以对多媒体文件(AVI/MP4/MKV/...)进行音频提取、视频提取、YUV提取以及封装多媒体文件。FFMPEG所需要的动态链接库(dll)已经放置到了*application*目录下，不用作额外的安装。

### 2.*Qt*
Qt是C++的界面设计框架，视频信息隐藏系统实现了基于Qt的MVC框架。Qt所需要的dll已经放置到了*application*目录下，不用作额外的安装。

### 3.*JM8.6*
JM是一款开源的H.264/AVC编解码器，是视频信息隐藏/提取算法的实现平台。JM通过提供可执行程序的形式，由视频信息隐藏系统调用，不用作额外的安装。JM8.6版本较低，后期可以使用更高版本的JM平台。

### 4.*K-Lite Codec Pack*
Qt界面在进行视频播放的时候，需要选择视频解码器，当前产品采用`K-Lite`作为视频播放的解码器。点击[这里](http://www.codecguide.com/download_k-lite_codec_pack_standard.htm)，进入K-Lite的下载页面，请下载并安装。

## 三、使用
视频信息隐藏系统是绿色软件，已经将所需要的所有文件放置到了*application*文件夹下，不需要进行其他任何的额外的安装和配置。
### 1.*打开视频*
在vih系统中，打开一个视频后，可以对该视频进行播放、嵌入信息以及提取信息。通过主界面中的`打开`按钮可以打开视频：

![](/material/open.png)

打开的多媒体格式包括但不局限于MP4、MKV、RMVB、WMV等。在打开视频后，可以通过主界面的`播放`按钮进行视频播放：

![](/material/play.png)

### 2.*信息隐藏*
信息隐藏操作是针对当前被打开的多媒体文件进行的，在vih刚刚启动时，没有多媒体文件被打开，因此这是不能进行信息嵌入，相关的按钮也也不会有响应。在打开视频后，通过主界面的`信息嵌入`按钮可以打开关于信息嵌入的面板:

![](/material/embpanel.png)

随后填写上关于待嵌入的数据文件的路径，以及输出的多媒体文件的路径，就可以点击嵌入按钮进行嵌入了：

![](/material/embfill.png)

在信息隐藏的过程中，vih会显示信息隐藏的进度。除了停止信息隐藏外和多媒体播放外，vih系统不允许在信息隐藏过程中进行其他任何操作的。

![](/material/embing.png)

当信息隐藏结束，vih系统会弹出提示。若是正常结束，则在对应路径处，已经生成了相应的载密视频文件。若是出现异常，则会弹框提示错误原因。
### 3.*信息提取*
信息提取是真对当前被打开的多媒体文件进行的，同样，vih刚刚启动时是不能进行信息提取的。在打开视频后，通过主界面的`信息提取`按钮可以打开信息提取相关面板：

![](/material/extpanel.png)

在该面板中填写上数据提取后的存放路径即可开始提取:

![](/material/extfill.png)

提取成功后，会弹框提示。若是正常结束，在对应的路径处可以看到提取的数据文件。若是出现异常，则会弹框提示错误原因。
### 4.*算法选择*
在主界面的`工具箱`中，有`算法选择`工具，可以选取进行信息隐藏和信息提取所采用的算法。

![](/material/chose.png)
### 5.*调试控制台*
在主界面的`工具箱`中，有`调试控制台`工具，可以打开控制台，用于在信息隐藏和信息提取过程中，清晰的看到程序的运行过程与中间输出。

![](/material/console.png)

## 四、添加算法
### 1.*Algorithm接口*
在源码中，每一个视频信息隐藏/提取算法都由一个Algorithm对象进行表示，该Algorithm中包含了该算法的很多信息，包括:
* 算法名称
* 算法工作空间路径
* 嵌入算法可执行程序路径
* 提取算法可执行程序路径
* 算法环境变量

由于不同的成员实现的算法不同，传参的方式也不同，Algorithm对象并不知道如何去传递参数。类Algorithm提供了`load_env_args()`方法，用来返回调用算法可执行程序前的环境变量以及参数列表。每当有一种新的传参方式的算法引入时，需要对Algorithm进行继承，并覆盖`load_env_args()`方法，用于决定Algorithm如何传参：
```cpp
class NewAlgorithm : public Algorithm{
public:
    NewAlgorithm(const QString& dir, const QString &name) : Algorithm(dir, name){}
public:
    void load_env_args(OperaType type, QStringList &env, QStringList &args) override {
        // 1).父类的参数加载方式, 用来获得最基本的env和args
        // 对于编码, args=['-d', '../../encoder.cfg'], env加载为算法缓存的param
        // 对于解码, args=['../../decoder.cfg'], env加载为算法缓存的param
        Algorithm::load_env_args(type, env, args);

        // 2).设置自己的参数加载方式, 对于自己定义的一些参数，建议通过环境变量传参，并在算法应用程序中进行检查。
        // 不含参数时，算法程序应该通过标准错误流来输出错误信息。
        AlgoConf::emb_secret_path();    // 嵌入所需要的秘密文件路径
        AlgoConf::ext_secret_path();    // 提取时秘密文件的输出路径
    }
};
```
需要注意的是，只有在需要新的参数传递方式时才需要实现新的Algorithm子类，否则都可以复用现成的Algorithm子类。
### 2.*AlgorithmBuilder*
为了方便选择性的加载不同算法，因此引入了Builder模式，并构建了AlgorithmBuilder类。Builder将会通过`build()`函数，构建一个Algorithm子类，该子类中已经实现了如何传参。因此类AlgorithmBuilder和类Algorithm是配套的，每当实现了一个Algorithm后，就需要实现一个对应的AlgorithmBuilder。一个AlgorithmBuilder的引入需要三个步骤:
* a) 实现AlgorithmBuilder<br>
主要是实现AlgorithmBuilder的ctor方法，这个方法用来告诉Builder如何实例化一个Algorithm。
```cpp
class NewBuilder : public AlgorithmBuilder{
    IAlgorithm *ctor(const QString& dir, const QString &name) override{
        return new NewAlgorithm(dir, name);
    }
};
```
* b) 添加至builderMapper<br>
为了根据app.cfg的配置加载算法，需要给Builder取名字，并将新算法Builder加入builderMapper。
```cpp
// 本代码位于main.cpp中
#include "NewBuilder.h"
bool check_load_model(shared_ptr<PanelStatusModel> m){
    ...
    QHash<QString, AlgorithmBuilder*> builderMap;
    builderMap.insert("LHH", new LHHBuilder());
    builderMap.insert("WTQ", new WTQBuilder());
    builderMap.insert("NEW", new NewBuilder());
    ...
}
```
* c) 重新编译

注意，由于AlgorithmBuilder和Algorithm配套，因此也就是需要在新的传参方式的时候，才需要引入新的AlgorithmBuilder。
### 3.*算法文件夹*
通过JM编译好隐藏/提取算法的可执行程序(lencod.exe/ldecod.exe)，可以构建算法文件夹。需要确保算法文件夹的命名、路径和此说明中的统一，否则无法加载算法。
```
└── 算法名(文件夹)
    ├── workspace       # 算法工作空间
    ├── lencod.exe      # 信息隐藏算法可执行程序
    └── ledecod.exe     # 信息提取算法可执行程序
```
### 4.*app.cfg*
在app.cfg的`algorithms`的最后指定新增算法的Builder类，以及算法名。视频信息隐藏系统将会获取该算法名，在`algorithms/`文件夹下寻找同名文件夹，然后判断文件夹下面所需要的文件是否存在，若不存在则会禁止程序加载。
```
algorithms = [A算法, LHH]; [B算法, WTQ]; [新算法，新算法Builder];
```
对于传参模式已经存在的算法程序而言，可以直接构建算法文件夹，然后再app.cfg中指定新算法名，以及对应的Builder即可。Builder其实就是用来指定算法采用何种传参方式的，Builder将会进一步build该传参方式的Algorithm类。

### 5.*算法注意事项*
* 正常结束的程序返回值应该为0
* 异常结束程序返回值为非零，并将错误原因填写到标准错误输出中
* 处理常见的异常情况
    * 需要的文件不存在
    * 需要的参数不存在
    * 需要的参数格式有误，无法使用
    * 选择的秘密文件过大，无法被全部嵌入