
# 1. 本项目建立的依赖包的安装指导：

一、安装 vclH60控件包，这个要首先安装，
　　然后安装　“个人资金”
二、再按任意次序安装其它包
三、建立了 环境变量 YDHSRC='D:\work\ydh_crm\src'
    库路径、搜索路径可以使用该环境变量，参考delphi环境变量的使用
    $(YDHSRC)\...
四、如果遇到版本异常,删除“C:\Program Files\Borland\Delphi7\Projects\Bpl”这个目录下的我们自己编译的所有文件，
    注意不要删除 第三方报表控件 文件名形式为：“QR4*”，时间是 2004，2006年。
    然后重新编译安装包！
    
    
 # 2. 安装包名称和路径：
 ```
0.    YDHSRC='D:\work\ydh_crm\src'      
1.    hwtvcl60.dpk          　　　　　　　$(YDHSRC)\control\vclH60               
2.    Pdygx.dpk(单据关系查询)             $(YDHSRC)\control\dygx                
3.    PkgFPGL.dpk(发票管理)　　           $(YDHSRC)\control\exe_fpgl             
4.    Package_grzjbl.dpk(个人资金)    　　$(YDHSRC)\control\个人资金              
　　　　　　　　　　　　　　　　　　　　　     $(YDHSRC)\control\个人资金\资金管理
5.    ydh_yggl.dpk          　　　　　　　$(YDHSRC)\control\员工管理              
6.    ydh_add.dpk           　　　　　　　$(YDHSRC)\control                       
　　　　　　　　　　　　　　　　　　　　　     $(YDHSRC)\control\订单与发票
　　　　　　　　　　　　　　　　　　　　　     $(YDHSRC)\control\企业收付款
7.    Pkjkm.dpk(会计帐本)　　             $(YDHSRC)\exe_kuijikemu   //这个别忘记啦！在另外一个目录里面
8.    y_qygl_crm.dpr        　　　　　　　$(YDHSRC)\                //这个是主项目
```

注意：上述源代码路径要　加入　Library path,  菜单：Tool\Enviroment option\library\Library path

每个包的项目前缀 ”H_“  ， 版本号码100

# 3. 总结：
- package 源代码路径要　加入　Library path,  菜单：Tool\Enviroment option\library\Library path,否则应用项目的编译无法通过
- 注意，package 的源码路径可能有多个子目录，都要加进去！
- 每个unit单元文件只能处于一个 package中，不要千万不要重复包含！
- 遇到package 安装异常，删除“C:\Program Files\Borland\Delphi7\Projects\Bpl”下我们的输出文件，重新编译安装，一般都可以解决。
- package 源码路径 加入应用项目的 Library path，不是 package search 路径，试过了，不行！  
