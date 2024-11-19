# 概述
<font style="color:#000000;">Memory Machine Cloud(MMC)为公有云用户提供更加简单、高效、省钱的云平台解决方案，基于WaveRider智能选配云主机和SpotSurfer断点续算两大核心能力实现云成本降低70%，性能提升50%。</font>

<font style="color:#000000;"></font>

<font style="color:#000000;">本文档介绍基于计算巢如何快速部署并使用MMC。</font>

<font style="color:#000000;"></font>

# 前提条件


<font style="color:rgb(51, 51, 51);">部署MMC实例服务实例，需要对部分阿里云资源进行访问和创建操作。因此您的账号需要包含如下资源的权限。 </font>**<font style="color:rgb(51, 51, 51);">说明</font>**<font style="color:rgb(51, 51, 51);">：当您的账号是RAM账号时，才需要添加此权限。</font>

| <font style="color:rgb(51, 51, 51);">权限策略名称</font> | <font style="color:rgb(51, 51, 51);">备注</font> |
| --- | --- |
| <font style="color:rgb(51, 51, 51);">AliyunECSFullAccess</font> | <font style="color:rgb(51, 51, 51);">管理云服务器服务（ECS）的权限</font> |
| <font style="color:rgb(51, 51, 51);">AliyunROSFullAccess</font> | <font style="color:rgb(51, 51, 51);">管理资源编排服务（ROS）的权限</font> |
| <font style="color:rgb(51, 51, 51);">AliyunComputeNestUserFullAccess</font> | <font style="color:rgb(51, 51, 51);">管理计算巢服务（ComputeNest）的用户侧权限</font> |




# 计费说明


<font style="color:rgb(51, 51, 51);">MMC在计算巢部署的费用主要涉及：</font>

+ <font style="color:rgb(51, 51, 51);">弹性云主机（ECS）费用</font>
+ <font style="color:rgb(51, 51, 51);">对象存储（OOS）费用</font>
+ <font style="color:rgb(51, 51, 51);">通过MMC控制节点，动态弹性创建的ECS的费用，这部分费用在MMC控制台页面可以清晰看到</font>

<font style="color:rgb(51, 51, 51);"></font>

# <font style="color:rgb(51, 51, 51);">服务架构</font>
![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731984964730-f561d0f8-787d-48ec-b9de-6ff2163778d2.png)

# 参数说明

| <font style="color:rgb(51, 51, 51);">参数组</font> | <font style="color:rgb(51, 51, 51);">参数项</font> | <font style="color:rgb(51, 51, 51);">说明</font> |
| --- | --- | --- |
| <font style="color:rgb(51, 51, 51);">服务实例</font> | <font style="color:rgb(51, 51, 51);">服务实例名称</font> | <font style="color:rgb(51, 51, 51);">长度不超过64个字符，必须以英文字母开头，可包含数字、英文字母、短划线（-）和下划线（_）</font> |
| | <font style="color:rgb(51, 51, 51);">地域</font> | <font style="color:rgb(51, 51, 51);">服务实例部署的地域</font> |
| <font style="color:rgb(51, 51, 51);">OpCenter配置</font> | <font style="color:rgb(51, 51, 51);">OpCenter机型</font> | <font style="color:rgb(51, 51, 51);">MMC控制节点的机器型号</font> |
| | <font style="color:rgb(51, 51, 51);">主机登录秘钥对</font> | 秘钥对用于弹性扩缩启动ECS |
| | 数据盘大小 | opCenter数据盘大小 |
| | DB盘大小 | opCenterDB盘大小 |
| | 磁盘类型 | opCenter磁盘类型 |
| <font style="color:rgb(51, 51, 51);">网络配置</font> | <font style="color:rgb(51, 51, 51);">可用区</font> | <font style="color:rgb(51, 51, 51);">ECS实例所在可用区</font> |
| | <font style="color:rgb(51, 51, 51);">VPC ID</font> | <font style="color:rgb(51, 51, 51);">资源所在VPC</font> |
| | <font style="color:rgb(51, 51, 51);">交换机ID</font> | <font style="color:rgb(51, 51, 51);">资源所在交换机</font> |
| | <font style="color:rgb(51, 51, 51);">mvPublicService</font> | 是否提供公网 |






# 部署流程


访问计算巢MMC[部署链接](https://computenest.console.aliyun.com/service/instance/create/cn-hangzhou?type=user&ServiceId=service-e570217a60a6477790a2)，选择套餐、配置参数后，确认订单：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985177195-648f382d-b8a4-4e1c-8e23-25f8728fcb1b.png)

2 确认订单后可以看到云资源价格预览，以及依赖的权限检查结果：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985276607-fcb8f7e5-33aa-45d2-8752-1c71bfa87010.png)

点击立即创建：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985343646-cd6ca803-6f74-4436-b5cd-8943ad4a8872.png)



点击「去列表查看」可以看到服务实例部署的详细进度如下：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985374317-6218ee75-77d1-47d0-a107-f9bb71346b6e.png)



完成部署后点击服务连接进入详情页面：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985569910-62dbcb1a-979a-49fc-bd1c-e5e505a55e5e.png)

点击详情页面的OpCenter登录地址，即可登录：



![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985625531-bb929312-d426-4951-9c98-0fd440482875.png)



# 服务激活
打开试用地址：[https://cn.mmcloud.io/customer/register](https://cn.mmcloud.io/customer/register) ，申请试用License：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985742234-ae93be29-c12d-4c16-950a-2065459addec.png)



填写试用信息之后点击注册，注册完成后到邮箱完成激活。



完成激活之后再MMC控制台页面输入用户名和密码完成激活，激活后试用周期为一个月。



![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731985927224-48bf9719-2c70-4090-8d56-30db1d96c42f.png)



激活之后页面显式状态为:



![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731986093609-c0b5faa9-e213-4d27-b3ad-fc3b16a7ca85.png)



# 服务使用
本示例通过使用blast:latest镜像，执行一个数据处理的任务为例，演示MMC的任务调度、成本分析等核心功能。



点击页面「创建任务」按钮：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731986276839-9da321c9-00bd-4589-8909-8028f00c6de1.png)



![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731986379219-56ca082c-4580-4d0a-a9df-372875268ffe.png)



上述自定义脚本具体内容为：

```yaml
#!/bin/bash

# This is a demo script for using bwa application
# To run this job
#   float submit -i bwa -j <this_script> --cpu 4 --mem 16 --dataVolume [size=64]:/data

export PATH=/opt/aliyun:$PATH

LOG_FILE=${FLOAT_LOG_PATH}/output
touch ${LOG_FILE}
exec >$LOG_FILE 2>&1

cd /BWA_BASE

# download and unzip dataset
echo "Downloading dataset ..."
wget https://public-ehpc-package.oss-cn-hangzhou.aliyuncs.com/lifescience/b37_human_g1k_v37.fasta
wget https://public-ehpc-package.oss-cn-hangzhou.aliyuncs.com/lifescience/gatk-examples_example1_NA20318_ERR250971_1.filt.fastq.gz
gunzip gatk-examples_example1_NA20318_ERR250971_1.filt.fastq.gz
wget https://public-ehpc-package.oss-cn-hangzhou.aliyuncs.com/lifescience/gatk-examples_example1_NA20318_ERR250971_2.filt.fastq.gz
gunzip gatk-examples_example1_NA20318_ERR250971_2.filt.fastq.gz

# workload start
echo "bwa index start ..."
bwa index b37_human_g1k_v37.fasta

echo "samtools start ..."
samtools faidx b37_human_g1k_v37.fasta

echo "bwa mem start ..."
bwa mem -t 16 -R '@RG\tID:ehpc\tPL:illumina\tLB:library\tSM:b37' b37_human_g1k_v37.fasta \
    gatk-examples_example1_NA20318_ERR250971_1.filt.fastq gatk-examples_example1_NA20318_ERR250971_2.filt.fastq \
    | samtools view -S -b - > ERR250971.bam

# workload end

NOW=$(date +"%Y-%m-%d_%H:%M:%S")
echo "Upload result ..."
#ossutil64 cp ${LOG_FILE} $OSS_BUCKET/bwa-output/${NOW}_LOG
#ossutil64 cp ERR250971.bam $OSS_BUCKET/bwa-output/${NOW}_ERR250971.bam
```

完成配置后点击「提交」按钮，完成任务提交。



![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731986450006-52e9172a-3ee8-49e9-a163-e070fb3e54a0.png)



「费用总结」部分可以看到花费的费用：

![](https://intranetproxy.alipay.com/skylark/lark/0/2024/png/47856458/1731986536362-28dc3f56-2928-4603-8efe-9309d012309a.png)


# 联系我们
