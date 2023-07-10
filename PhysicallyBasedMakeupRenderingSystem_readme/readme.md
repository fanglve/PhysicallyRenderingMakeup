# 标题

基于物理的数字人美妆仿真系统

## 功能介绍
系统基于unreal engine，使用metahuman Irene模型叠加由km模型、多层模型表达的化妆层，提出了一个实时数字人多层化妆品渲染系统。模型首先分层实现眼影、口红、粉底、腮红四类化妆品。系统内部设计厚度、化妆贴图、吸收系数和散射系数分别控制不同种类化妆品的厚度、风格、颜色。然后，系统基于反射率、透射率定义使用多层模型，计算各层化妆品的叠加反射率、透射率。最后使用次表面轮廓渲染方法渲染皮肤，并将化妆品效果与皮肤渲染效果叠加。系统的主要局限在于不能渲染珠光、亮片、水乳材质的化妆品。

## 效果展示
### 腮红、眼影实验结果
![image](/pics/color_blush eyeshadow.png)

### 粉底、口红实验结果
![image](/pics/color_foundation lipstick.png)

### 参数厚度X对腮红、口红、眼影的影响
![image](/pics/thickness_foundation lipstick.png)

### 眼影口红化妆贴图对化妆品渲染位置的控制
![image](/pics/makeup mask_eye shadow lipstick.png)

### 粉底腮红化妆贴图对化妆品渲染位置的控制
![image](/pics/makeup mask_foundation blush.png)

## 安装
0. 文件的安装环境为unreal engine 5.1.1
1. 首先在https://www.unrealengine.com/zh-CN/metahuman 制作自己的metahuman。利用unreal engine中的quickxel bridge插件下载自己的metahuman。
2. 将metahuman导入后，在与Metahumans/Common/Face/Materials/Baked文件夹平行的位置，解压文件夹。
3.由于您的metahuman的皮肤和Irene可能有所不同，而压缩包中的皮肤材质是基于metahuman Irene构建的。所以需要将解压后的文件夹中的skin文件替换为您的metahuman的材质图层，并右键这个材质图层创建对应的材质图层实例。再将材质图层实例skin_Inst拖入化妆品材质文件NewMaterial_2，将结点skin_Inst分别连接到BreakMaterialAttributes的属性结构和SetMaterialAttributes的材质属性接口。
![image](/pics/skin_inst.png)
4. 点击屏幕中的metahuman，点击网格体栏中的骨骼网格体资产。打开网格体，将网格体中的head_LODx_shader_shader插槽文件全部替换为NewMaterial_2_Inst文件。
5. 将KY_EyeLipstickMask和KY_FoundationBlusherMask的文件替换为EyeLipstickMask和FoundationBlusherMask的文件内容



## 使用
1. 文件夹中的文件主要包含两个材质函数，三个材质实例，一个材质，一个材质图层和一个材质图层实例。
2. 两个材质函数分别为km模型、多层模型的材质表达，被应用在化妆品材质NewMaterial_2文件中。材质函数的参数也作为模型的主要参数，由实例文件NewMaterial_2_Inst调节。
3. 主要通过NewMaterial_2材质图层的MakeMaterialAttributes的shading Model结点控制化妆品和皮肤的着色模型。
2. 在化妆品材质的实例文件NewMaterial_2_Inst中，以字母KY_开头的文件为模型可控的参数。
(1) KY_xxxMask控制两种化妆品的化妆贴图
(2) KY_xxxThickness控制化妆品厚度
(3) KY_xxAbsorptionCoefficient控制化妆品吸收系数，KY_xxScatteringCoefficient控制化妆品散射系数。


## 主要局限
由于系统中化妆品BRDF的构造方式，目前系统只能处理膏状化妆品，如口红、液体眼影、粉底等，不能处理粉末状、珠光、亮片等材质。因此不能模拟散粉、高光、眼影等常用化妆品的效果。







