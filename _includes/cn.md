把手识别系统
======================

[English]({{ site.baseurl }}/) \\( \\qquad \\) [**中文**]({{ site.baseurl }}/cn/)

![](http://images.freeimages.com/images/previews/7d5/under-construction-icon-1242121.jpg)

## 简介 ##

该系统主要设计目的为供重型机械操作者使用，满足连续的不间断的生物特征识别安全保证需求，提供一种满足人体工程学的不打断工作进程的生物特征识别技术。

背景
-------------

连续生物特征识别（continuous biometrics），是一种连续的，不间断的生物特征识别技术。该技术是为了保证在场景持续过程中，用户的身份可以确保没有被调换、伪造、代替、中断 [[Traore and Ahmed 2012](http://www.igi-global.com/gateway/book/52722)]。常见的连续生物特征识别，可以使用指纹识别、人脸识别、语音识别 [[Altinok and Turk 2003](http://www.cs.ucsb.edu/~mturk/pubs/AltinokTurk2003.pdf)]、按键行为识别、鼠标行为识别和触摸屏行为识别 [[Kute and Rewadkar 2014](http://www.ijsr.net/archive/v3i12/U1VCMTQzOTU%3D.pdf)]。常见问题，一：需要配备额外的生物特征识别传感器，容易打断工作进程，例如：基于心电图的持续生物特征识别技术 [ContinUse Biometrics](http://finder.startupnationcentral.org/c/continuse)。二：按键识别、鼠标识别、触屏识别等行为识别，识别性能相对较差，且受限于使用场景 [[Moskovitch etc 2009](http://www.ise.bgu.ac.il/faculty/liorr/idth.pdf)]。按键和鼠标，针对的主要是室内办公场景。触屏主要是针对智能手机。

美国国防部 2012 年开始以主动认证（[active authentication](http://www.darpa.mil/program/active-authentication)）为名针对连续生物特征识别展开相关研究 [[报道](https://gcn.com/articles/2012/03/21/darpa-dump-passwords-continuous-biometrics.aspx)，[2013 年的报告](https://www.rsaconference.com/writable/presentations/file_upload/sec-t05_final.pdf)]。

人体工学的生物特征设计模型（ergonomics biometrics design model, EBD model），是一种充分考虑人体工学因素的生物特征识别设计模型（[Qu, Xiaofeng][csxfqu]; [Zhang, David][csdzhang]; [Lu, Guangming][csgmlu]; and [Guo, Zhenhua][cszhguo], "[Door knob hand recognition system （门把手人手识别系统）][dkhrs]," *in Systems, Man, and Cybernetics: Systems, IEEE Transactions on , vol.PP, no.99, pp.1-12*.）。该模型受人-生物特征识别传感器交互模型（human - biometric sensor interaction model, HBSI model）启发，将人体工学因素与生物特征识别系统的基本设计相结合。为新生物特征识别的设计提供指导。

根据 continuous biometrics 的需求，针对重型机械操作这一场景，根据 EBD model，提出把手识别系统——人体工学的高精度人手特征的连续生物特征识别。

原理
-------------

该识别系统的主要结构是一个通过齿轮组同步的多滚轴旋转系统。该滚轴系统在外层顺时针（或逆时针）旋转的同时保持把手的其它部分稳定。这样，握着把手的手掌可以保持稳定。同时，线扫描模组在手掌内侧旋转一周采集手掌内侧图像。

![把手识别系统原理]({{ site.baseurl }}/images/fig_handle_scheme.png)

图像传感器
-------------

该系统使用订制的 CIS （contact image sensor，接触式图像传感器）模组。该 CIS 模组包括红/绿/蓝/红外四色 LED 光源、微型镜头阵列、和 CMOS 线扫描图像传感器。成像距离在 4-7 毫米。分辨率为 50/100/200 dpi 可选。三路分段并行输出。

演示系统
-------------

该演示系统仅完成了机械验证，下一步是图像采集和特征分析。

![把手识别系统演示系统]({{ site.baseurl }}/images/fig_handle_demo.png)

采集到的图像应该是持握圆柱的完整的握姿人手图像。当前分辨率最高为 200 dpi，可以采集到主线和褶皱线，还不够指纹识别所需的 500 dpi (minutiae)，更不够 1200 dpi 的汗孔(pore)。一方面可以尝试类似掌纹识别的方法；另一方面，可以通过订制更高分辨率的传感器改进图像质量。

同步运动单元
-------------

运动同步包括两部分，一部分是齿轮间的同步，精确控制滚轴与把手整体的运动。当把手外表面旋转移动距离 \\(\\pi{}D\\) 时，通过齿轮组（传动比 \\(R\\)）驱动滚轴外表面反向位移同样距离（\\(R\\pi{}d=\\pi{}D\\)），保证握住把手的手绝对位置不变。另一部分是把位移转换成 CIS 模组的图像采集控制脉冲，来调整采集到图像的长度方向的分辨率。该脉冲与移动位移固定比例，与 CIS 宽度方向分辨率要适应。既当 CIS 模组配置为 100 dpi 时，位移脉冲分辨率也要设定为 100 dpi。该设计参考线扫描掌纹识别系统 ([Qu, Xiaofeng][csxfqu]; [Zhang, David][csdzhang]; [Lu, Guangming][csgmlu], "[A Novel Line-Scan Palmprint Acquisition System (一种新型线扫描掌纹采集系统)][TSMC-LPS]," *in Systems, Man, and Cybernetics: Systems, IEEE Transactions on , vol.PP, no.99, pp.1-11*.)。

图像与特征分析
-------------

该系统采集图像为握住圆柱体的握姿状态下人手。从范围来说，采集到的图像包括整手。既手型、掌纹、内侧指节纹、指纹都在采集图像范围内。但也存在挑战，既采集到的图像不是标准状态下的人手，会有挤压和形变。但其实从生物特征识别角度来说，这种挤压和形变，也可以看做是一种基于行为习惯的特征。其实手上的纹理本身的形成，就是一种混沌的过程，就是手上皮肤的天然挤压与形变形成的，只不过是非常稳定。而行为意义上的挤压和形变的稳定性还有待考察。

在特征方面，100 dpi 能够提取主线；150 dpi 能够提取褶皱线；500 dpi 能够提取纹线；1200 dpi 能够提取汗孔。但参考低分辨率掌纹（< 150 dpi）的识别率，基本上 200 dpi 就可以提供一定的性能保证。如果处理速度够快，尝试 1200 dpi 也不是不可以。但要考虑人手图像挤压与形变的不稳定性，不要滥用高分辨率，却反而提取到一些不稳定的特征。可以确定的是，至少手型（几何特征）是能保证的。主线和褶皱线特征，既掌纹和内侧指节纹问题不大。再进一步的特征就要根据实验确定了。

其实最主要的，反而是一个稳定的 ROI（感兴趣区域）提取方法，这个更决定整体系统的稳定性。如果能够提取到稳定的区域，识别率应该至少可以达到与相近原理的系统类似（[Qu, Xiaofeng][csxfqu]; [Zhang, David][csdzhang]; [Lu, Guangming][csgmlu]; and [Guo, Zhenhua][cszhguo], "[Door knob hand recognition system （门把手人手识别系统）][dkhrs]," *in Systems, Man, and Cybernetics: Systems, IEEE Transactions on , vol.PP, no.99, pp.1-12*.）。

应用
-------------

该系统可以应用于重型工程机械，为高危险性的重型工程机械提供一种不间断的针对操作员的生物特征识别验证。采用本系统，可以保证工程机械工作时由专业人员操控，防范安全风险，提供一种不可抵赖的安全验证手段。同时本系统可以应用于安全需求较高的军事与航天设备等。

相关文献
-------------

[TSMC-LPS]: http://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=7390297
[csxfqu]: http://www.quxiaofeng.me/about
[csdzhang]: http://www4.comp.polyu.edu.hk/~csdzhang/
[csgmlu]: http://www.hitsz.edu.cn/body/shizi/detailen.php?strID=396
[cszhguo]: http://www.sz.tsinghua.edu.cn/publish/sz/139/2012/20120420104947649501973/20120420104947649501973_.html
[dkhrs]: http://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=7433472
