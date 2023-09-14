# Revit2GLTF

#### 关于glTF

关于glTF这里就不多做什什么介绍了，可以去看官网的介绍，glTF是一种规范格式，和obj之类的3D格式本质是一样的，他的文件包括了.gltf（描述模型的整体信息），.bin用二进制保存几何信息。还有材质文件。
通过读取gltf文件中的scenes、nodes、meshes、accessors、bufferViews、buffers、materials、textures、images。每一层的递进都有数组下标来确定。其中中最重要的是mesh，它通过primitives字段指定， prmitives中的attributes 指定了顶点、顶点法线、uv坐标在accessors数组的对应数据的下标。用过底层openGl和webgl的同学们就会发现这个gltf中mesh的描述和openGl中大同小异。整个gltf结格的设计和就是为了和webgl以及webgl更好的契合，他们之类的GL都是同样的意思
————————————————
版权声明：本文为CSDN博主「Cowboy小张同学」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_35187495/article/details/118278840

#### 介绍

这是一个基于MIT开源协议的revit导出gltf的开源库，支持revit2020~revit2023，项目依赖于revit，通用构件的合并以及C#对draco算法库的封装，拥有极快的导出速度和极高的压缩率。

在线查看案例：https://cowboy1997.github.io/Revit2GLTF/threejs/main

![image](https://github.com/cowboy1997/Revit2GLTF/blob/main/test.png)

 Revit导出glTF
      revit导出glTF中现在已经有比较多开源的插件了，质量比较高的是
      https://github.com/McCulloughRT/Revit2glTF，不过这个插件还只是半成品，而且以及不更新了，可能作者已经转行了开发了，
      因此我在前人的基础上完善重构了个导出glTF。整个导出很简单，就是调用继承了revitapi的IExportContext接口，然后把构件信息填进去了glTF里面，整体包括了以下内容：
填加y轴向上的矩阵变化
填加导出法向量、UV和材质贴图
增加判断顶点索引数据类型，减少导出文件体体积
对draco算法的C＃封装，直接在C#中多线程使用draco算法，极大提高导出draco版本的gltf的时间
修改相似构件判断方法。同一类型几何信息只导出一次，大大提高导出速度和减少文件大小。
这里我做了一个测试导出revit的案例文件，开启draco和不开启draco都是在几秒内就完成了。nice！！自我感觉良好！！

#### 支持

1、支持revit带材质导出GLTF

2、支持导出revit法向量、UV

3、支持draco多线程压缩

4、支持相同构件合并

5、支持导出gltf/glb

6、支持导出revit属性

#### 安装教程
3、资源下载
编译好的安装包下载路径https://github.com/cowboy1997/Revit2GLTF/releases/download/Revit2GLTF/Setup.msi
源代码路径
https://github.com/cowboy1997/Revit2GLTF

1、直接下载编译好的安装包https://github.com/cowboy1997/Revit2GLTF/releases/download/Revit2GLTF/Setup.msi

2、或者打开sln编译Revit2GLTF模块（依赖RevitAPI、RevitAPIUI、Newtonsoft）。如果你想重新编译修改DracoNet需要重新引入draco的文件头和静态库

#### 关于

如有不懂，欢迎加入QQ群：835368069
包括BIM开发，Cad开发，threejs开发，python，webAssembly等等的。
大家喜欢可以加群一起卷起来！！卷卷卷卷！！！
