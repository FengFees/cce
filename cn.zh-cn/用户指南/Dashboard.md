# Dashboard<a name="cce_01_0128"></a>

## 插件简介<a name="section1418513434428"></a>

Kubernetes Dashboard是一个旨在为Kubernetes世界带来通用监控和操作Web界面的项目，集合了命令行可以操作的所有命令。

使用Kubernetes Dashboard，你可以：

-   向Kubernetes集群部署容器化应用
-   诊断容器化应用的问题
-   管理集群的资源
-   查看集群上所运行的应用程序
-   创建、修改Kubernetes上的资源（例如Deployment、Job、DaemonSet等）
-   展示集群上发生的错误

例如：您可以伸缩一个Deployment、执行滚动更新、重启一个Pod或部署一个新的应用程序。

**开源社区地址：**[https://github.com/kubernetes/dashboard](https://github.com/kubernetes/dashboard)

>![](public_sys-resources/icon-note.gif) **说明：** 
>当前华为云CCE提供的Dashboard插件已将对应镜像升级到最新版本，不受Kubernetes Dashboard漏洞CVE-2018-18264影响。
>安全漏洞CVE-2018-18264的详细信息，请参考：
>-   [https://github.com/kubernetes/dashboard/pull/3289](https://github.com/kubernetes/dashboard/pull/3289?spm=a2c4g.11186623.2.10.34d16d21dGsJMe)
>-   [https://github.com/kubernetes/dashboard/pull/3400](https://github.com/kubernetes/dashboard/pull/3400?spm=a2c4g.11186623.2.11.34d16d21dGsJMe)
>-   [https://github.com/kubernetes/dashboard/releases/tag/v1.10.1](https://github.com/kubernetes/dashboard/releases/tag/v1.10.1)

## 安装步骤<a name="section46701613154319"></a>

1.  登录CCE控制台，单击左侧导航栏的“插件管理“，在“插件市场“页签下，单击dashboard插件下的“安装插件“。
2.  在安装插件页面，选择安装的集群和插件版本，单击“下一步：规格配置”。
3.  在规格配置页面，配置以下参数。
    -   证书配置：dashboard服务端使用的证书。
        -   默认选中，可手动上传证书。
            -   证书文件：单击![](figures/zh-cn_image_0178555448.png)查看证书文件样例参考。
            -   证书私钥：单击![](figures/zh-cn_image_0178555449.png)查看证书私钥样例参考。

        -   不选择，将不需要上传证书。

            >![](public_sys-resources/icon-notice.gif) **须知：** 
            >dashboard默认生成的证书不合法，将影响浏览器正常访问，建议您选择手动上传合法证书，以便通过浏览器校验，保证连接的安全性，合法证书购买方法请参见[购买证书](https://support.huaweicloud.com/usermanual-scm/scm_01_0221.html)。


    -   访问类型：可以选择节点访问（NodePort）和负载均衡（LoadBalancer）两种类型。
        -   节点访问：
            -   绑定弹性IP：若集群没有绑定弹性IP，需单击[此处](https://console.huaweicloud.com/vpc/#/vpc/vpcmanager/eips)绑定弹性IP，绑定后单击刷新按钮。

                该插件默认以NodePort形式提供访问，需为集群任意一个节点绑定弹性IP才能使用。

        -   负载均衡：
            -   负载均衡：选择弹性负载均衡实例。若无弹性负载均衡实例，需新建共享型弹性负载均衡，完成后单击刷新按钮。

                >![](public_sys-resources/icon-note.gif) **说明：** 
                >负载均衡实例需与当前集群处于相同VPC且为公网类型。

            -   端口配置：访问类型为负载均衡时，需端口配置。
                -   协议：默认为TCP。
                -   容器端口：默认为8443。
                -   访问端口：容器端口最终映射到负载均衡服务地址的端口，用负载均衡服务地址访问工作负载时使用，端口范围为1-65535，可任意指定。



4.  单击“安装“。

    待插件安装完成后，单击“返回“，在“插件实例“页签下，选择对应的集群，可查看到运行中的实例，这表明该插件已在当前集群的各节点中安装。


## 安装后续操作<a name="section174811341488"></a>

成功安装dashboard后，需完成如下步骤才能使用：

1.  **获取认证token**

    请于“插件管理”-\>“插件实例”-\>“dashboard”完成操作。

2.  **访问dashboard**

    “插件管理”-\>“插件实例”-\>“dashboard”，单击“访问地址”中的链接并通过token登录。


## 访问dashboard<a name="section15288141117362"></a>

确认dashboard插件状态为“运行中“后，单击“访问地址“中的链接并登录，详细操作如下：

1.  登录CCE控制台，单击左侧导航栏的“插件管理“，在“插件实例”页签下，确认dashboard插件状态为“运行中“后，单击插件名称“dashboard“进入插件实例详情页。
2.  在详情页下方的“说明”页签下，单击“获取默认token”右侧的![](figures/zh-cn_image_0219106095.png)，复制“值”栏中的信息。

    **图 1**  复制token<a name="fig118242010184815"></a>  
    ![](figures/复制token.png "复制token")

3.  在插件详情页，单击“访问地址“中的链接，将会打开Kubernetes仪表盘登录页面。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >使用Chrome浏览器访问时，会出现如下“ERR\_CERT\_INVALID”的报错导致无法正常进入登录界面，解决方法请参见[附：访问报错解决方法](#section913875232612)。

    **图 2**  访问地址<a name="fig1953829125211"></a>  
    ![](figures/访问地址.png "访问地址")

4.  在登录页面中选择“令牌”的登录方式，粘贴输入复制的“值”，单击“登录“按钮。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >本插件默认不支持使用证书认证的kubeconfig进行登录，推荐使用令牌方式登录。详细信息请参考：[https://github.com/kubernetes/dashboard/issues/2474\#issuecomment-348912376](https://github.com/kubernetes/dashboard/issues/2474#issuecomment-348912376)

    **图 3**  令牌方式登录<a name="fig2040714531230"></a>  
    ![](figures/令牌方式登录.png "令牌方式登录")

5.  登录后效果，如[图4](#fig12780143011555)。

    **图 4**  Dashboard概览页<a name="fig12780143011555"></a>  
    ![](figures/Dashboard概览页.png "Dashboard概览页")


## 权限修改<a name="section10659162018415"></a>

安装Dashboard插件后初始角色仅拥有对大部分资源的只读权限，若想让Dashboard界面支持更多操作，需自行在后台对RBAC相关资源进行修改。

**具体修改方式：**

可对名为“kubernetes-dashboard-minimal”这个ClusterRole中的规则进行调整。

关于使用RBAC的具体细节可参看文档：[https://kubernetes.io/docs/reference/access-authn-authz/rbac/](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)。

## 升级插件<a name="section455343310401"></a>

1.  登录CCE控制台，单击左侧导航栏的“插件管理“，在“插件实例“页签下，选择对应的集群，单击dashboard下的“升级“。

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >-   如果升级按钮处于冻结状态，则说明当前插件版本是最新的版本，不需要进行升级操作；
    >-   若升级按钮可单击，则单击升级按钮即可升级dashboard插件。
    >-   升级dashboard插件时，会替换原先节点上的旧版本的dashboard插件，安装最新版本的dashboard插件以实现功能的快速升级。

2.  在弹出的窗口中，单击“确认“，可升级该插件。配置参数可参考[安装插件](#section46701613154319)中的参数说明。

## 卸载插件<a name="section20765191931911"></a>

1.  登录CCE控制台，单击左侧导航栏的“插件管理“，在“插件实例“页签下，选择对应的集群，单击dashboard下的“卸载“。
2.  在弹出的窗口中，单击“是“，可卸载该插件。

## 附：访问报错解决方法<a name="section913875232612"></a>

使用Chrome浏览器访问时，会出现如下“ERR\_CERT\_INVALID”的报错导致无法正常进入登录界面，原因是dashboard默认生成的证书未通过Chrome校验，当前有以下两种解决方式：

**图 5**  Chrome浏览器报错信息<a name="fig1873703218416"></a>  
![](figures/Chrome浏览器报错信息.png "Chrome浏览器报错信息")

-   方式一：使用火狐浏览器访问链接，为当前地址添加“例外”后即可进入登录页面。
-   方式二：通过启动Chrome时添加“--ignore-certificate-errors”开关忽略证书报错。

    Windows：保存链接地址，关闭所有已经打开的Chrome浏览器窗口，Windows键 +“R”弹出“运行”对话框，输入“chrome --ignore-certificate-errors”启动新的chrome窗口，输入地址进入登录界面。


