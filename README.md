# git_branch
# git版本管理及常用指令 :see_no_evil:

目录

[1.1 分支规范	1](#_toc19203)

[方案一：Git Flow 模式	1](#_toc17056)

[常用分支规则	3](#_toc2366)

[Master分支	3](#_toc25334)

[Develop分支	3](#_toc27463)

[Feature分支	3](#_toc30548)

[Release分支	3](#_toc29661)

[Hotfix分支	4](#_toc11557)

[日常工作模式	4](#_toc471)

[紧急需求和Hotfix	4](#_toc6800)

[方案二：AoneFlow模式	5](#_toc683)

[基本使用规则	5](#_toc3959)

[规则一，开始工作前，从主干创建特性分支。	5](#_toc17900)

[规则二，通过合并特性分支，形成发布分支。	5](#_toc18293)

[日常工作模式	6](#_toc25042)

[紧急需求和Hotfix	7](#_toc19646)

[部分功能取消上线	7](#_toc22812)

[多环境支持	7](#_toc6928)

[分支使用规则	7](#_toc29883)

[主干分支规则	7](#_toc19220)

[功能分支规则	7](#_toc6190)

[发布分支规则	8](#_toc4575)

[标签规范	8](#_toc19838)


#
1. # <a name="_toc7323"></a><a name="_toc19203"></a>**分支规范**
## <a name="方案一：git flow 模式"></a><a name="_toc11580"></a><a name="_toc17056"></a>**方案一：Git Flow 模式**
经典的Git工作模式，源于Vincent Driessen提出了 [A Successful Git Branching Model](http://nvie.com/posts/a-successful-git-branching-model/)论文。下面是Git Flow官方的流程图

![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.001.jpeg)

### <a name="常用分支规则"></a><a name="_toc16522"></a><a name="_toc2366"></a>**常用分支规则**
#### <a name="_toc25334"></a>**Master分支**




![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.002.png)

注：其中[]中为可选项，视项目情况而定，下同。
#### <a name="_toc27463"></a>**Develop分支**







![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.003.png)
#### <a name="_toc30548"></a>**Feature分支**








![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.004.png)
#### <a name="_toc29661"></a>**Release分支**




![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.005.png)


#### <a name="_toc11557"></a>**Hotfix分支**




![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.006.png)



### <a name="日常工作模式"></a><a name="_toc471"></a>**日常工作模式**

1. 项目开始情况下代码管理员会初始化远程仓库，并基于master的初始版本创建三条分支，他们是**origin/master(对应生产)，origin/release(对应测试环境)，origin/develop(对应开发环境) 并为这三条分支设置保护策略，三条分支均不允许直接的commit与push修改。**
1. 项目规划本次上线的需求和版本。
1. 开发接到需求后基于develop分支切功能分支进行开发。
1. 功能开发完成后依次合并代码到develop分支进行联调，并提交PR进行code     review。
1. 联调完成后准备测试时由develop分支合并到release分支，并发布到测试环境进行测试。
1. 测试完成后基于release分支进行发布，发布成功后将release分支合并到master分支和develop分 支，并在master分支上打tag标记。

### <a name="紧急需求和hotfix"></a><a name="_toc6800"></a>**紧急需求和Hotfix**
1\. 在上述过程中，需要hotfix或者有紧急需求时，则需要从master切hotfix分支进行修复，修复后直接拿hotfix分支上线，上线完成后合回master、develop、release分支。

## <a name="_toc22463"></a><a name="_toc683"></a>**方案二：AoneFlow模式**
其他主流发布模式和分支使用方式。AoneFlow 只使用三种分支类型：主干分支、特性分支、发布分支，以及三条基本规则。
### <a name="基本使用规则"></a><a name="_toc31924"></a><a name="_toc3959"></a>**基本使用规则**
#### <a name="_toc17900"></a>**规则一，开始工作前，从主干创建特性分支。**
AoneFlow 的特性分支基本借鉴 GitFlow，没有什么特别之处。每当开始一件新的工作项（比如新的功能或是待解决的问题）的时候，从代表最新已发布版本的主干上创建一个通常以

![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.007.png)<span>feature/</span> 前缀命名的特性分支，然后在这个分支上提交代码修改。也就是说，每个工

作项（可以是一个人完成，或是多个人协作完成）对应一个特性分支，所有的修改都不允许直接提交到 主干。

![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.008.jpeg)

#### <a name="_toc18293"></a>**规则二，通过合并特性分支，形成发布分支。**
![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.009.png)AoneFlow 的发布分支设计十分巧妙，可谓整个体系的精髓。GitFlow 先将已经完成的特性分支合并回公共主线（即开发分支），然后从公共主线拉出发布分支。TrunkBased   同样是等所有需要的特性都在主干分支上开发完成，然后从主干分支的特定位置拉出发布分支。而 AoneFlow 的思路是，从主干上拉出一条新分支，将所有本次要集成或发布的特性分支依次合并过去，从而得到发布分支。发布分支通常 以<span>release/</span> 前缀命名。

![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.010.jpeg)
###
#### **规则三，发布到线上正式环境后，合并相应的发布分支到主干，在主干添加标签，同时删除该发布分支 关联的特性分支。**
当一条发布分支上的流水线完成了一次线上正式环境的部署，就意味着相应的功能真正的发布了，此时 应该将这条发布分支合并到主干。为了避免在代码仓库里堆积大量历史上的特性分支，还应该清理掉已 经上线部分特性分支。与 GitFlow 相似，主干分支上的最新版本始终与线上版本一致，如果要回溯历史版本，只需在主干分支上找到相应的版本标签即可。

![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.011.jpeg)


### <a name="_toc29771"></a><a name="_toc25042"></a>**日常工作模式**
1. 项目选择一条分支作为主干分支（长期存在），例如master，主分支只保存和线上一致的代码， 不允许直接在上面提交代码。
1. 当有开发任务或者问题修复时由开发人员基于主分支切功能分支进行开发。
1. 需求开发完成后基于master切测试环境的发布分支release\_test，并将本次要测试的功能分支代码 依次合并过去。合并前最好同步master代码到本地防止冲突。合并时要进行Code Review。
1. 修改bug时基于功能分支进行修改，修改完成后提交到release\_test中。
1. 测试完成后，基于master切UAT环境的发布分支release\_uat，如果功能没有变动则直接将

   release\_test合并到release\_uat中。

1. 生产发布时基于master切生产环境的发布分支release\_prod，如果功能没有变动则直接将

   release\_uat合并到release\_prod中进行发布，发布完成后将release\_prod的代码合回master分支，并打上版本标签。

1. 发布成功后删除功能分支和release-test、release-uat和release-prod分支。

### <a name="_toc10135"></a><a name="_toc19646"></a>**紧急需求和Hotfix**
1. 生产环境出现bug或者有紧急需求时需要从主分支切一个功能分支进行开发。
1. 修复完成后基于master切测试环境的发布分支release\_test，将修复的分支合并过去进行测试。如 果此时有其他需求在测试时需要搁置并让路。
1. 待生产Bug修复完成后按照正常标准进行发布。

### <a name="部分功能取消上线"></a><a name="_toc5931"></a><a name="_toc22812"></a>**部分功能取消上线**
1. 测试阶段或者UAT阶段，如果有一些功能的Bug较多无法满足上线要求或因为客户要求取消某些需 求时，则需要把这部分功能剔除出去。
1. 可以基于主分支重新切一条发布分支，并将要保留的代码合并到这个分支中，再进行一轮测试。测 试完成后再进行发布。
1. 是否需要再进行测试由需求影响范围决定。

### <a name="多环境支持"></a><a name="_toc25844"></a><a name="_toc6928"></a>**多环境支持**
1. 假设有一些特殊的场景验证时可单独快速地组合一个发布分支，从而不影响其他环境的测试发布等。

### <a name="分支使用规则"></a><a name="_toc15165"></a><a name="_toc29883"></a>**分支使用规则**

#### <a name="_toc19220"></a>**主干分支规则**



![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.012.png)


#### <a name="_toc6190"></a>**功能分支规则**







![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.013.png)


#### <a name="_toc4575"></a>**发布分支规则**







![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.014.png)

### <a name="_toc19838"></a>**标签规范**



![](assets/Aspose.Words.e7131a3b-c15e-4afa-b093-59a05cf67bea.015.png)

