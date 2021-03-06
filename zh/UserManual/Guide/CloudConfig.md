# 云配置
## 简介
###什么是Cloud Config
每个应用在云端都有一个对应的`MLCloudConfig`对象，用以存储该应用的参数。Cloud Config服务帮助您访问和操作云端参数。您可以通过Console在MaxLeap中配置应用参数，并且使用iOS/Android SDK读取云端的参数。
###为何需要Cloud Config
将应用的部分配置放置在云端的优势在于：

* **动态配置：**
* **个性化用户体验：**在云端，您可以根据Segment配置参数，使不同用户群有不同的用户体验

## 下一步
**如果您希望进一步了解MaxLeap Cloud Config服务SDK，请参考[iOS开发指南 － Cloud Config](ML_DOCS_GUIDE_LINK_PLACEHOLDER_IOS#CLOUD_CONFIG_ZH)或[Android开发指南 － Cloud Config](ML_DOCS_GUIDE_LINK_PLACEHOLDER_ANDROID#CLOUD_CONFIG_ZH)。**

##云参数列表
在开发者中心"云配置"中，我们可以查看该应用下所有的云参数的列表。该列表包含以下列：

列名|描述
-------|-------
Parameter|参数名
Type|参数类型
Value|参数的值
Detail|(修改/删除按钮)

###新建云参数
点击左上角"＋新建参数"按钮，提供参数名，参数类型及参数的值，便可以完成云参数的新建：

![imgCFAddConfig.png](../../../images/imgCFAddConfig.png)

云参数新建完毕后，系统将提示您，是否向不同的Segment赋不同的值：

![imgCFAddConfigPopup.png](../../../images/imgCFAddConfigPopup.png)

点击确定后，您将进入云参数的修改界面：

点击“添加云参数”，您便可以不同的Segment设定不同的参数值：

![imgCFAddSegment.png](../../../images/imgCFAddSegment.png)

最后，您的云参数的值将随着不同的Segment而具有不同的值：

![imgCFSegmentDone.png](../../../images/imgCFSegmentDone.png)

###修改/删除云参数
在Detail列中选择修改按钮，即可进入修改页面。

在Detail列中选择删除按钮，点击确认，即可删除该云参数。

## 下一步

**如果您希望进一步了解MaxLeap Cloud Config服务SDK，请参考[iOS开发指南 － Cloud Config](ML_DOCS_GUIDE_LINK_PLACEHOLDER_IOS#CLOUD_CONFIG_ZH)或[Android开发指南 － Cloud Config](ML_DOCS_GUIDE_LINK_PLACEHOLDER_ANDROID#CLOUD_CONFIG_ZH)。**
