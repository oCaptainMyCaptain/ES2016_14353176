# DOL开发环境配置及安装笔记

标签（空格分隔）： 未分类

---

## DOL开发环境配置

### DOL框架描述：



### DOL安装过程




1. ##### 安装**必要的环境**

   `sudo apt-get update`

   ![](http://i1.piimg.com/567571/ba69fbfb64c9a4d5.png)

   `sudo apt-get install ant`

   ![](http://i1.piimg.com/567571/ab4ad1c4a1098cf2.png)

   `sudo apt-get install openjdk-7-jdk`

   ![](http://i1.piimg.com/567571/a468ba49c9271d64.png)

   `sudo apt-get install unzip`

   ![](http://i1.piimg.com/567571/01cc1f979f505cd8.png)

   ​

2. ##### **下载文件**

   需要两个压缩包分别为[systemc-2.3.1.tgz](http://www.accellera.org/images/downloads/standards/systemc/systemc-2.3.1.tgz)和[dol_ethz.zip](http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip),可以直接在网上下载，最好是在所用的系统里下载，免得发生丢失的情况。

   ```perl
   sudo wget http://www.accellera.org/images/downloads/standards
   /systemc/systemc-2.3.1.tgz
   sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip
   ```

   ​

3. ##### **解压文件**

   * 自行建立dol文件夹

     `mkdir dol`

     ![](http://i1.piimg.com/567571/b775e87658c23233.png)

     ​可以看到我们的目录里面出现了这个**dol**目录，我这里在根目录建立

   * 将**dol_ethz**解压到**dol**这个文件夹中

     ```unzip dol_ethz.zip -d dol```

   * 解压下载的**systemc-2.3.1.tgz**，同样解压到根目录下

     ```tar -zxvf systemc-2.3.1.tgz```

     ![](http://p1.bqimg.com/567571/f1821fec851c174f.png)

   ​

4. ##### **编译systemc**

   * 进入到刚才解压的**systemc-2.3.1**中

     `cd systemc-2.3.1`

   * 新建文件夹**objdir**

     `mkdir objdir`

   * 进入文件夹**objdir**

     `cd objdir`

   * 在命令行里面运行**configure**，这个是根据系统的环境设置一下参数

     `../configure CXX=g++ --disable-async-updates`

     可以得到下面的结果：

     ![](http://p1.bqimg.com/567571/31c75a9b4a4a5148.png)

   * 开始**编译**

     `sudo make install`

     编译之后，可以得到下图所示结果：

     ![](http://p1.bqimg.com/567571/accca4c2b268c24c.png)

     `cd ..`

     `ls`

     ![](http://p1.bqimg.com/567571/9e1bd9c17f884630.png)

     打开编译完的目录如上面所示，记下**工作路径**

     `pwd`

     ![](http://p1.bqimg.com/567571/46e083f7ff40df68.png)

     这个路径在之后的配置中会起到作用

   ​

5. ##### **编译DOL**

   * ##### 进入刚刚新建的**dol**文件夹中

     `cd ../dol`

   * 修改dol里面的**build_zip.xml**文件


     用**gedit**打开这个文件

     ```
     <property name="systemc.inc" value="YYY/include"/>
     <property name="systemc.lib" value="YYY/lib-linux
     /libsystemc.a"/>
     ```

     将上面两句代码里面的**YYY**改成之前**pwd**的结果，也就是上面得到的

     `/home/linhongwei14353176/systemc-2.3.1`

   * 进行**编译**

     `ant -f build_zip.xml all`

     ![](http://i1.piimg.com/567571/aff9fab40f4896be.png)

     如果这个步骤成功，显示上图结果，即**BUILD SUCCESSFUL**

   * 运行**例子**进行验证

     `cd build/bin/main`

     `ant -f runexample.xml -Dnumber=1`

     运行上面两行命令，得到以下结果：

     ![](http://i1.piimg.com/567571/482b672b8f17b305.png)

     最后结果为**BUILD SUCCESSFUL**。至此，DOL开发环境**配置完成**

### 实验感想

​	**本次实验内容是DOL开发环境配置，中间经历了很多莫名其妙的错误，一直不知道是怎么错的。重装了三遍才完成，估计是开始从windows把文件拉到虚拟机有掉了某些东西吧，到最后就只能重来，以后还是老老实实，能在虚拟机里下载就在里面下载吧，希望之后的实验都能顺利完成！**




