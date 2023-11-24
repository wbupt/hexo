title: RCWA 相关1
tags: [RCWA]
published: true
hideInList: false
isTop: false
date: 
feature:
sticky: 101
top: 101
category: 学习 # 分类 RCWA

---
# RCWA1

## 介绍

$\boldsymbol{E}*{top}^{inc}exp\left(i\big(k_x^{inc}x+k*{z~top}^{inc}(z-h)\big)\right)$

$a=a+b$

RCWA（Rigorous Coupled Wave Analysis）全名是`严格耦合波分析`，是一种用于设计、分析及优化周期性结构的数值计算方法。它可以用来模拟各种周期性结构，比如光学元器件中的光栅、光纤光栅、光子晶体等，也可以用于模拟电磁结构中的电磁波导、电磁障碍物、互联线等。

RCWA方法利用`傅里叶变换`将**周期相干场**分解为**傅里叶变换**的模式，然后利用模式的耦合关系求解出这些模式的反射、透射、散射等物理量。由于RCWA是一种严格的全波方法，因此它可以考虑各种效应，比如多次反射、全息效应等，对于对场分布有精细要求的问题有很好的解决方案。

RCWA具有高精度、高效能、灵活性等特点，因此它已经成为现代光学和电磁学中一种常用的设计和分析周期性结构的工具。

---

# RETICOLO 网状的



Authors: J.P. Hugonin and P. Lalanne



• Reticolo 1D代码用于分析传统安装中的1D光栅。

arXiv: 2101:00901



• Reticolo 1D-conical代码用于分析传统和锥形安装中的1D光栅。

• Reticolo 2D代码用于分析2D交叉光栅。

分析二维交叉光栅。

它们是在Matlab下运行的免费软件。要安装它们，请复制附带的文件夹“reticolo_allege”，并将文件夹添加到Matlab路径中。软件可以在此处下载。



### This technical note is composed of three parts:

本技术说明由三部分组成:

1. Reticolo code 1D for analyzing 1D gratings in classical mountings Reticolo 代码1D用于分析经典安装中的一维光栅
2. Reticolo code 1D-conical for analyzing 1D gratings in classical and conical mountings 用于分析经典和锥形装置中的一维光栅的 Reticolo 程序1D锥形
3. Reticolo code 2D for analyzing 2D crossed grating Reticolo 代码2D用于分析二维交叉光栅





They are free software that operate under Matlab. To install them, copy the companion folder “reticolo_allege” and add the folder in the Matlab path. The software can be downloaded here.

它们是在 Matlab 下运行的自由软件。要安装它们，复制相关文件夹“ reticolo _ allege”，并将该文件夹添加到 Matlab 路径中。软件可以在这里下载

 

The version V9 launched in 01/2021 features a few novelties:

2021年1月发布的 v9版本有一些新特性:

ü it includes a treatment of stacks of arbitrarily anisotropic multilayered thin-films.1 Be aware that the substrate and superstrate cannot be anisotropic. This part is documented in Reticolo codes 1D-conical (or identically 2D).

它包括对任意各向异性的多层薄膜堆叠的处理，1 Be 意识到衬底和上层不能是各向异性的。这部分记录在 Reticolo 代码1d-锥形(或同样的2d)中。

ü It features an option to visualize the Bloch modes.

它提供了一个可视化 Bloch 模式的选项。

ü Diagonal anisotropy (𝜺𝒙𝒙 ≠ 𝜺𝒚𝒚 ≠ 𝜺𝒛𝒛) can be incorporated in structured grating layers and gratings with uniform layers having arbitrary anisotropy (𝜺𝒙𝒚 ≠ 𝟎 …) can also be handled)

对角各向异性(εxx ≠ εy≠ εzz)可以被引入到结构光栅层中，具有任意各向异性的均匀层光栅(εxy ≠0...)也可以被处理

ü It is fully compatible with earlier versions.

它与早期版本完全兼容。

 

2021年1月发布的V9版本具有一些新功能： 它包括对任意各向异性多层薄膜堆的处理。请注意，基板和上置基底不能是各向异性的。本部分在Reticolo代码1D-conical（或2D相同）中有文档记录。 它具有可视化布洛赫模的选项。 对于具有对角各向异性（≠≠）的结构性光栅层以及具有任意各向异性（≠ ...）的均匀光栅层的光栅也可以处理。 它与早期版本完全兼容。

2021年1月发展的 v9版本有一些新功能: 它包括它包括它对任意角层的光栅的意义，基础板和上基底性不能够是各向性的分部分别在 reticolo 码1d-锥形(或2d 相对)中有文档记录。它以及具有可视化布洛赫的选项对于有具体项目具有可视化布洛赫的选项。

  

This is simply achieved by retaining a single Fourier harmonics coefficient in the expansion (nn=0). The extension is not optimal from numerical-efficiency perspectives, but has been provided on demand of several users who additionally complained of mistakes in available freeware packages on thin films.

这只是通过在展开式中保留一个单一的傅里叶谐波系数(nn = 0)来实现。从数值效率的角度来看，这种扩展并不是最佳的，但它是根据一些用户的要求提供的，这些用户还抱怨可用的薄膜免费软件包中存在错误。

Note also that we have launched in 2013 the RETICOLOfilm-stack program, a freeware that computes the reflection and transmission of arbitrary stacks of anisotropic thin films. RETICOLOfilm-stack is vectorialized and thus treats several wavelengths and incidences in a single instruction (see https://zenodo.org/record/7512710).

请注意，我们在2013年发布了 RETICOLOfilm-stack 程序，这是一个计算任意堆叠各向异性薄膜的反射和透射的免费软件。RETICOLOfilm-stack 是矢量化的，因此在一条指令中处理多个波长和入射(见 https://zenodo.org/record/7512710)。

通过在展开式中保留单个傅里叶谐波系数（nn=0）即可轻松实现该目标。从计算效率的角度来看，扩展不是最优的，但是由于多个用户要求并提到了现有免费软件程序中的错误，因此我们提供了这个扩展。 此外，请注意，2013年我们推出了RETICOLOfilm-stack程序，它是一个免费软件，用于计算各向异性薄膜的任意堆栈的反射和透射。RETICOLOfilm-stack是矢量化的，因此可以在单个指令中处理多个波长和入射角度（请参见https://zenodo.org/record/7512710）。

通过在此我们提出了 reticolofilm-stack，它是一个免费软件即可计算堆长和在各种轻向异射膜系统中的反射透射度角的设计

# RETICOLO CODE 1D



for the diffraction by stacks of lamellar 1D gratings (classical diffraction) 用于分析分层1D光栅的衍射 （经典衍射）

对于层状一维光栅的衍射(经典衍射) ，用于分析层状一维光栅的衍射(经典衍射)

Reticolo code 1D is a free software for analyzing 1D gratings in classical mountings. It operates under Matlab. To install it, copy the companion folder “reticolo_allege” and add the folder in the Matlab path. Reticolo code 1D  是一款免费软件，用于分析经典安装的一维光栅。它在 Matlab 下运行。要安装它，复制伴随文件夹“ reticolo _ allege”，并将该文件夹添加到 Matlab 路径中。



## 1. Generality 概述

它可以计算由层状结构组成的光栅的衍射效率和衍射幅度。它包含用于计算和可视化光栅内部和外部的电磁场的例程。在此版本中，无法分析二维周期性的（交叉的）光栅。

RETICOLO is a code written in the language MATLAB 9.0. It computes the diffraction efficiencies and the diffracted amplitudes of gratings composed of stacks of lamellar structures. It incorporates routines for the calculation and visualisation of the electromagnetic fields inside and outside the grating. With this version, 2D periodic (crossed) gratings cannot be analysed.

RETICOLO是用MATLAB 9.0编写的代码。它计算由层状结构组成的光栅的衍射效率和衍射振幅。它包括计算和可视化光栅内外电磁场的例程。这个版本中，无法分析二维周期性（交叉）光栅。

As free alternative to MATLAB, RETICOLO can also be run in GNU Octave with minimal code changes. For further information, please contact tina.mitteramskogler@profactor.at.

作为MATLAB的免费替代品，RETICOLO也可以在GNU Octave中运行，只需进行最小程度的代码更改。欲了解更多信息，请联系tina.mitteramskogler@profactor.at。

 

In brief, RETICOLO implements a frequency-domain modal method (known as the Rigorous Coupled wave Analysis/RCWA). To get an overview of the RCWA, the interested readers may refer to the following articles:

简而言之，RETICOLO 实现了一种频域模态方法(称为严格耦合波分析/RCWA)。为了得到 RCWA 的概述，感兴趣的读者可以参考以下文章:

`1D-classical and conical diffraction` 1d-经典和圆锥衍射

1. M.G. Moharam et al., JOSAA **12**, 1068 (1995),

2. M.G. Moharam et al, JOSAA **12**, 1077 (1995),

3. P. Lalanne and G.M. Morris, JOSAA **13**, 779 (1996),
4. G. Granet and B. Guizal, JOSAA **13**, 1019 (1996),
5. L. Li, JOSAA **13**, 1870 (1996), see also C. Sauvan et al., Opt. Quantum Electronics **36**, 271-284 (2004) which simply explains the raison of the convergence-rate improvement of the Fourier-Factorization rules without requiring advanced mathematics on Fourier series and generalizes to other kinds of expansions. 具体而言，关于傅里叶分解规则的收敛速率优化原因，可以参考李灵宏在1996年发表在JOSAA期刊上的文章“Efficient computation of diffraction in the Rayleigh-Sommerfeld region by exact use of the scalar wave equation”以及C. Sauvan等人在2004年出版的文章“Theory of the Fabry-Pérot resonator: A review”（Opt. Quantum Electronics 36, 271-284），两篇文章均不需要关于傅里叶级数和其他扩展方法的高级数学知识，可以简单地解释傅里叶分解规则的收敛速率优化原因，并推广至其他类型的展开方法。



`2D-crossed gratings` 2d 交叉光栅

1. L. Li, JOSAA **14**, 2758-2767 (1997),
2. E. Popov and M. Nevière, JOSAA **17**, 1773 (2000)

which describe the up-to-date formulation of the approach used in RETICOLO. Note that the formulation used in the last article (which proposes an improvement for analysing metallic gratings with continuous profiles like sinusoidal gratings) is not available in the RETICOLO version of the web. The RCWA relies on the computation of the eigenmodes in all the layers of the grating structure in a Fourier basis (plane-wave basis) and on a scattering matrix approach to recursively relate the mode amplitudes in the different layers.

描述了 RETICOLO 中使用的方法的最新公式。请注意，上一篇文章中使用的公式(其中提出了一种改进方案，用于分析具有连续剖面的金属光栅，如正弦光栅)在 RETICOLO 版本的 web 中是不可用的。RCWA 依赖于在傅里叶基(平面波基)上计算光栅结构各层的本征模，并利用散射矩阵方法将不同层的模振幅递推关联起来。

 

`Eigenmode solver` For conical diffraction analysis of 1D gratings, the Bloch eigenmode solver used in Reticolo is based on the article "P. Lalanne and G.M. Morris, JOSAA **13**, 779 (1996)".

本征模式求解器: 对于一维光栅的圆锥衍射分析，Reticolo 中使用的 Bloch 本征模式求解器是基于“ p. Lalanne 和 g.m. Morris，JOSAA 13,779(1996)”一文

 

`Scattering matrix approach` The code incorporates many refinements that we have not published and that we do not plan to publish. For instance, although it is generally admitted that the S-matrix is inconditionnally stable, it is not always the case. We have developed an in-house transfer matrix method which is more stable and accurate. The new transfer matrix approach is also more general and can handle perfect metals. The essence of the method has been rapidly published in "J.-P. Hugonin, M. Besbes and P. Lalanne, Op. Lett. **33**, 1590 (2008)".

散射矩阵方法: 该代码包含了许多我们没有发表过也不打算发表的改进。例如，尽管人们普遍承认 s 矩阵是无条件稳定的，但事实并非总是如此。我们开发了一种更稳定和准确的内部转移矩阵方法。新的转移矩阵方法也更加通用，可以处理完美的金属。这种方法的精髓已经在《日报》上迅速发表。作者: Hugonin，m. Besbes and p。莱特。33,1590(2008)”。

 

`Field calculation` The calculation of the near-field electromagnetic fields everywhere in the grating is performed according to the method described in "P. Lalanne, M.P. Jurek, JMO **45**, 1357 (1998)" and to its generalization to crossed gratings (unpublished). Basically, no Gibbs phenomenon will be visible in the plots of the discontinuous electromagnetic quantities, but field singularities at corners will be correctly handled.

**场计算: 根据“ P.Lalanne，m.p. Jurek，JMO 45,1357(1998)”中描述的方法及其对交叉光栅的推广(未发表) ，计算了光栅内各处的近场电磁场。基本上，在不连续电磁量的图中不会看到吉布斯现象，但是在角落处的场奇异性将被正确处理。**

 

`Acknowledging the use of RETICOLO` In publications and reports, acknowledgments have to be provided by referencing to J.P. Hugonin and P. Lalanne, RETICOLO software for grating analysis, Institut d'Optique, Orsay, France (2005), arXiv:2101:00901.

使用RETICOLO声明: 在出版物和报告中，承认必须参考 j.p. Hugonin 和 p. Lalanne，RETICOLO 光栅分析软件，法国 Orsay 光学研究所，arXiv: 2101:00901

 

**In addition, one may fairly quote the following references in journal publications**:

此外，人们可以在期刊出版物中公正地引用以下参考文献:

-M.G. Moharam, E.B. Grann, D.A. Pommet and T.K. Gaylord, "Formulation for stable and efficient implementation of the rigorous coupled-wave analysis of binary gratings", J. Opt. Soc. Am. A **12**, 1068-1076 (1995), if TE-polarization efficiency calculations are provided -P. Lalanne and G.M. Morris, "Highly improved convergence of the coupled-wave method for TM polarization",

\- m.g. Moharam，e.b. Grann，d.a. Pommet 和 t.k. Gaylord，“稳定和有效地实施严格的二元光栅耦合波分析的公式”，J.Opt。译注:。译注:。A 12,1068-1076(1995) ，如果提供 te 偏振效率的计算-p. Lalanne 和 gm. Morris，“极大地改进了 TM 偏振耦合波方法的收敛性”,

J. Opt. Soc. Am. A **13**, 779-789 (1996) and G. Granet and B. Guizal, "Efficient implementation of the coupled- wave method for metallic lamellar gratings in TM polarization", J. Opt. Soc. Am. A **13**, 1019-1023 (1996), if TM- polarization efficiency calculations are provided, -P. Lalanne and M.P. Jurek, "Computation of the near-field pattern with the coupled-wave method for TM polarization", J. Mod. Opt.45, 1357-1374 (1998), if near-field electromagnetic-field distributions are shown.

## 2 The diffraction problem considered 

颜色问题的考虑

In general terms, the code solves the diffraction problem by a grating defined by a stack of layers (in the z- direction) which have all identical periods in the x-direction and are invariant in the y direction, see Fig. 1. In the following, the (x,y) plane and the z-direction will be referred to as the transverse plane and the longitudinal direction, respectively. To define the grating structure, first we have to define a top and a bottom. This is rather arbitrary since the top or the bottom can be the substrate or the cover of a real structure. It is up to the user. Once the top and the bottom of the grating have been defined, the user can choose to illuminate the structure from the top or from the bottom. The z-axis is oriented from bottom to top.

通常情况下，该代码通过在z方向上具有相同周期的层数组成的光栅来求解衍射问题，该光栅在x方向上具有相同的周期并在y方向上不变，见图1。接下来，（x，y）平面和z方向将分别称为横向平面和纵向方向。为了定义光栅结构，首先我们需要定义其顶部和底部。这相当任意，因为顶部或底部可以是真实结构的衬底或覆盖层，根据用户的设定来选择。在定义了光栅的顶部和底部后，用户可以从顶部或底部照射光结构。z轴从下向上定向。

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403113229636.png" alt="image-20230403113229636" style="zoom: 67%;" />



 图1. 衍射场的瑞利展开。 第m阶具有平行动量等于𝑘𝑥𝑖𝑛𝑐+ 𝑚𝐾𝑥。我们定义两个点Otop = (0,0, h)在光栅顶部以及Obottom = (0,0,0)在光栅底部。

RETICOLO is written with the convention for the complex notation of the fields. So, if the materials are absorbant, one expects that all indices have a positive imaginary part. The Maxwell's equations are of the form
RETICOLO 是用约定书写的，用于字段的复杂符号。因此，如果材料是吸收性的，人们期望所有的指数都有一个正虚部分。麦克斯韦方程组是这种形式




其中，𝜀= 𝑛2 是相对介电常数，为一个复数，𝜆是真空中的波长。

接下来，考虑了两种情况： 

1. TE极化：电场E与Oy平行； 
2. TM极化：磁场H与Oy平行。



RETICOLO returns the diffraction efficiencies of the transmitted and reflected orders for a plane wave incident from the top and from the bottom with the same calculation. Of course, these two incident plane waves must have identical x-component of the parallel wave vector: $k_{x}^{inc}$. This possibility which is not mentioned in the literature to our knowledge is important in practice since the user may get, with the same computational loads, the diffraction efficiencies of the grating component illuminated from the substrate or from the cover.

RETICOLO可以返回从顶部和底部入射的平面波的衍射效率的透射和反射阶数，并采用相同的计算。当然，这两个入射平面波的平行波矢量的x分量必须相同：$k_{x}^{inc}$。在我们所知的文献中未提到这一可能性，但在实践中非常重要，因为用户可以在同样的计算负载下获取从衬底或覆盖层照明的光栅组件的衍射效率。

 RETICOLO-1D calculates the electric and magnetic fields diffracted by the grating for the following incident plane wave:

RETICOLO-1D 计算了以下入射平面波的光栅衍射的电场和磁场:

$\boldsymbol{E}_{top}^{inc}exp\left(i\big(k_x^{inc}x+k_{z~top}^{inc}(z-h)\big)\right)$

$\textbf{H}^{inc}_{top}\textit{exp}\left(i\left(k^{inc}_{x}x+k^{inc}_{ztop}(z-h)\right)\right)$ 如果从顶部层入射，

where $~k^{inc}_{z~top}=-\sqrt{\left(2\pi n_{top}/\lambda\right)^2-(k^{inc}_x)^2}$

$\boldsymbol{E}_{bottom}^{inc}exp\left(i\big(k_x^{inc}x+k_{z\text{bottom}}^{inc}(z-h)\big)\right)$

$\textbf{H}_{bottom}^{inc}exp\left(i\big(k_x^{inc}x+k_{z\textit{bottom}}^{inc}(z-h)\big)\right)$, 如果从底部层入射，

where $k_{Z\textit{bottom}}^{inc}=\sqrt{(2\pi n_{bottom}/\lambda)^2-(k_x^{inc})^2}$.

The z-component of the Poynting vector of the incident plane wave is ±0.5.

入射平面波的波矢量的z分量为±0.5。



The Rayleigh-expansion of the diffracted electric fields are shown in the following figure. 

下图显示了衍射电场的瑞利展开结果：

 $\boldsymbol{E}^{diff}_{top}=\sum_m\boldsymbol{E}^{m}_{top}\exp\left[i((k^{inc}_x+mK_x)x+k^{m}_{z\text{top}}(z-h)\right]$

$\boldsymbol{H}_{top}^{d i f}=\sum_m\boldsymbol{H}^{m}_{top}\exp\left[i((k^{inc}_x+mK_x)x+k^{m}_{ztop}(z-h)\right]$

where $k^m_{z~top}=\sqrt{\left(2\pi n_{top}/\lambda\right)^2-(k^inc_x+m K_x)^2}$

$\begin{array}{rcl}\boldsymbol{E}^{diff}_{bottom}&=\sum_m\boldsymbol{E}^{m}_{bottom}exp\left[i((k_x^{inc}+mK_x)x+k^{m}_{\text{z bottom}}z\right]\end{array}$

$\begin{array}{r l}\boldsymbol H_{bottom}^{diff}&=\sum_m\boldsymbol H_{bottom}^m exp[i((k_x^{inc}+mK_x)x+k_{z\text{bottom}}^m z]\end{array}$

where $k^m_z\text{bottom}=\sqrt{(2\pi n_{bottom}/\lambda)^2-(k^inc_x+mK_x)^2}$



They are shown in the following figure. 它们如图1所示。

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403113229636.png" alt="image-20230403113229636" style="zoom: 67%;" />



Fig. 1. Rayleigh expansion for the diffracted fields. $K_x=(2\pi)/period$. The $m^{\text{th}}$ order has a parallel momentum equal to $\quad k_{x}^{inc}+m K_{x}$. We define two points $\text{O}_{\text{top}}=(0,0,\text{h})$ at the top of the grating, and $\text{O}_{\text{bottom}}=(0,0,0)$ at the bottom of the grating .

 图1. 衍射场的瑞利展开。 𝐾𝑥=(2𝜋)/𝑝𝑒𝑟𝑖𝑜𝑑。第m阶具有平行动量等于𝑘𝑥𝑖𝑛𝑐+ 𝑚𝐾𝑥。我们定义两个点Otop = (0,0, h)在光栅顶部以及Obottom = (0,0,0)在光栅底部。

The following is organized so that one can straightforwardly write a code using the software 以下内容旨在帮助用户直接使用该软件编写代码.



## Preliminary input parameters 初步输入参数

The name of the following parameters are given as examples. The user may define his own parameter vocabulary. 下列参数的名称作为示例给出。用户可以定义自己的参数词汇表。

 

**wavelength = 3**; % wavelength (l) in a vacuum. It might be 3 nm or 3 µm. You do not need to specify the unit but all other dimensions are of course in the same unit as the wavelength.

在真空中，wavelength = 3;% wavelength ()。它可能是3 nm 或3 μm。你不需要指定单位，但所有其他维度当然是在同一个单位作为波长。

 

period = in the x-direction.  周期 = 在 x 方向

 

`nn = 20`; % this define the set of Fourier harmonics retained for the computation. More specifically, 2´nn+1 represent the number of Fourier harmonics retained from –nn to nn. This is a very important parameter ; for large n values, a high accuracy for the calculated data is achieved, but the computational time and memory is also large. If all the textures are homogeneous (case of a thin-film stack), we may set nn=1 and the period may be arbitrarily set to any value, 1 for example. NB: Because of our normalization (Poynting vector equal to 1), the computed reflected and transmitted amplitude coefficients are not identical to those provided by the classical Fresnel formulas found in textbooks.

`nn = 20`  ％这定义了计算中保留的傅里叶谐波集合。更具体地说，2×nn+1代表从-nn到nn保留的傅里叶谐波数量。这是一个非常重要的参数；对于大的n值，可以实现计算数据的高精度，但计算时间和内存也很大。如果所有的纹理都是均匀的（如薄膜堆），我们可以将nn设置为1，周期可以任意设置为任何值，例如1。注意：由于我们的归一化（泊松矢量等于1），计算得到的反射和透射幅度系数与教科书中的经典Fresnel公式提供的系数不同。

 

`parm = res0(1)` for TE polarization;  对于 TE 极化，parm = res0(1) ;

`parm = res0(-1)` for TM polarization; 对于 TM 极化，parm = res0(- 1) ;

% res0.m is a function that set default values to all parameters used by the code and determine the polarisation. res0.m是一个函数，它为代码使用的所有参数设置默认值，并确定极化。

`k_parallel` =$\boldsymbol{k_x^{inc}}$(𝟐𝝅/𝝀) is the normalised parallel momentum of the incident plane wave. 入射平面波的归一化平行动量. 

If the grating is illuminated from the top region (or from the bottom region) under an incident angle θ, one has: 如果光栅在入射角为θ的情况下从顶部区域（或底部区域）照射，则有：

`k_parallel=n_inc\*sin(θ)`

`K _ parallel = n _ inc \* sin (θ) `

where n_inc is the refractive index of the top (or bottom) layer. One expects that it is a positive real number and that the texture (see Section 4.1) associated to the top (or the bottom) layer has a background with a uniform refractive index “n_inc”.

其中，n_inc是顶部（或底部）层的折射率。人们期望它是一个正实数，并且与顶部（或底部）层相关联的纹理（见第4.1节）具有具有均匀折射率“n_inc”的背景。 

(Note that the “k_parallel” variable is defined **without** the factor 𝟐𝝅/𝝀.)  

（请注意，“k_parallel”变量的定义没有因子2π/λ。）

 It is very important to keep in mind that wether one defines the incident plane wave in the top layer or in the bottom layer, the calculation will be done for both an incident wave from the top and an incident wave from the bottom, with an identical parallel momentum k_parallel. 

需要牢记的是，不管是在顶部层还是底部层中定义入射平面波，计算都将针对从顶部入射的波和从底部入射的波进行，并具有相同的平行动量k_parallel。

These 5 parameters (“wavelength, nn, parm and k_parallel) are required by the code. Some other parameters can additionally be defined. For example, the default parameters do not take the symmetry of the problem into account. So if one wants to use symmetries, a new parameter has to be defined: “parm.sym.x”, (see section 7). If one wants to calculate accurately the electromagnetics fields, one has to define: ” parm.res1.champ=1”, but this increases the calculation time and memory loads (see section 8)

这5个参数（“波长、nn、parm和k_parallel)”是代码所需的。还可以定义其他一些参数。例如，缺省参数没有考虑问题的对称性。因此，如果想要使用对称性，需要定义一个新的参数：“parm.sym.x”（参见第7节）。如果想要精确计算电磁场，则必须定义：“parm.res1.champ=1”，但这将增加计算时间和内存负载（请参见第8节）。



 

## Structure definition (grating parameters) 

结构定义（光栅参数）

The grating encompasses a uniform upperstrate, called the top in the following, a uniform substrate, called the bottom in the following, and many layers which define the grating, which is defined by a stack of layers. Every layer is defined by a “texture” and by its thickness. Two different layers may be identical (identical texture and thickness), may have different thicknesses with identical texture, may have different thicknesses and textures. To define the diffraction geometry, we need to define the different textures and then the different layers.

光栅包括一个统一的上层基板，以下称为顶部，在以下称为底部的统一基板上，以及定义光栅的许多层，它由一组层定义。每层由一个“纹理”和它的厚度来定义。两个不同的层可以相同（相同的纹理和厚度），可以具有不同厚度相同的纹理，也可以具有不同厚度和纹理。为了定义衍射几何，我们需要定义不同的纹理，然后是不同的层。

 

### How to define a texture?

如何定义纹理？

 Every texture is defined by a cell-array composed of two line-vectors of identical length. The first vector, let us say [x1 x2 ... xp ...xN], contains all the x-values of the discontinuities. One *must* have :

每个纹理都由一个包含两个相同长度的行向量的单元数组定义。第一个向量，我们称之为 [x1 x2 ... xp ...xN]，包含所有不连续点的x值。必须满足以下条件：

1. N>1
2. $x_p<x_{p+1}$ for any p
3. $x_N-x_1\leq\text{period}$.

The second line-vector [n1 n2 ... np ... nN] contains the refractive indices of the material between the discontinuities. More explicitly, we have a refractive index np for xp-1<x<xp. Because of periodicity, note that the refractive index for xN<x<x1+period is equal to n1.

第二条线向量[ n1 n2... np... nN ]包含介于不连续面之间的材料的折射率。更明确地说，我们对 xp-1 < x < xp 有折射率 np。由于周期性，请注意 xN < x < x1 + 周期的折射率等于 n1。

The specific case of a uniform texture with a refractive index n is easily defined by texture{1}={n}. In that specific case, no need of a second vector since there is no discontinuity.

具有折射率 n 的均匀织构的特殊情况很容易由织构{1} = { n }来定义。在这种情况下，不需要第二个矢量，因为没有不连续性。

 The textures have all to be to be packed together in a cell array textures={textures{1}, textures{2}, textures{3}} prior calling subroutine **res1.m.**

这些纹理必须在调用子例程 res1.m 之前被打包在一个单元格阵列纹理 = {纹理{1} ，纹理{2} ，纹理{3}中。

 Example : 例子:

```matlab
period=17; # 周期 = 17; 
textures =cell(1,2); # 纹理 = 单元格(1,2) ;
textures{1}={1.5}; %uniform texture # 纹理{1} = {1.5} ;% 均匀纹理
textures{2}={[-5,-3,1,6],[2,1.3,1.5,3]}; %texture composed of 4 different refractive indices ％由四个不同折射率组成的纹理

```



The following figure shows the refractive indices of the two textures.以下图显示了这两个纹理的折射率。

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403163538201.png" alt="image-20230403163538201" style="zoom: 50%;" />

Fig. 2. Textures{1} and {2}.  图2. 纹理{1}和{2}。

 

`Slits in perfectly-conducting metallic textures`: 完美导体金属纹理中的缝隙: 

Mixing perfectly-conducting metallic textures and dielectric textures in the same grating structure is possible. We have first to define a background by its refractive index “inf” (for infinity). In this uniform background, we can incorporate strip inclusions with a complex or real refractive index “ninclusion” defined by the position c of its center and its x-width L. The inclusions cannot overlap.

在同一光栅结构中混合完美导体金属纹理和介质纹理是可能的。首先，我们需要通过其折射率“inf”（表示无穷大）来定义一个背景。在这个统一的背景中，我们可以插入带有复杂或实折射率“ninclusion”的条形包含物，该包含物由其中心位置c和x宽度L来定义。这些包含物不能重叠。



For example: 例如:

```HTML
textures {3}= {inf, [c1,L1,ninclusion1],[c2,L2, ninclusion2]}
# 纹理{3} = { inf，[ c1，L1，ninclusion 1] ，[ c2，L2，ninclusion 2]
```



`Anisotropic layers:` 各向异性层:

Grating layers (not the substrate nor the superstrate) can be anisotropic with diagonal tensors (𝜀𝑥𝑦 = 𝜀𝑥𝑧 … = 0). 光栅层(不是衬底也不是上层)可以是各向异性的对角张量(εxy = εxz... = 0)。

To implement diagonal anisotropy 实现对角各向异性

parm.res1.change_index=$\{\left[n_{\text{prov}}^1,n_{x}^1,n_{y}^1,n_{z}^1\right],\left[n_{\text{prov}}^2,n_{x}^2,n_{y}^2,n_{z}^2\right]\}$; % $\mathbf{n}_{\text{prov}}^1\neq\mathbf{n}_{\text{prov}}^2$

The refractive index nprov1 is then replaced **in all textures** by epsilon=diag([(n 1)2, (n 1 )2, (nz1 )2]). Beware if the superstate (or substrate) has a refractive index nprov1, it will also be replaced and this is not allowed. Thus we recommend using an unusual value for nprov1 (e.g. 89.99999 or rand(1)).

然后，折射率 nprov1在所有纹理中被 epsilon = diag ([(n1)2，(n1)2，(nz1)2])取代。当心，如果超态(或衬底)具有折射率 nprov1，它也将被替换，这是不允许的。因此，我们建议使用 nprov1的不寻常值(例如89.99999或兰特(1))。

The user may also diagonal permeability tensors 用户也可以使用对角渗透张量

parm.res1.change_index=

 $\{~\left\{\left[n_{\text{prov}}^1,~n_x^1,n_y^1,n_z^1,m_x^1,m_y^1,m_z^1\right],\left[n_{\text{prov}}^2,~n_x^2,n_y^2,n_z^2\right]\right\}$;

​    

Parm.res1.change _ index = {[ nprov1，n1，n1，nz1，m1，m1] ，[ nprov2，n2，n2，nz2] ;

The     refractive     index     nprov1  is   then   replaced   **in   all   textures**   by $\text{epsilon=diag}([(n_x^1)^2,(n_y^1)^2,(n_z^1)^2]),\text{mu=diag}([(m_x^1)^2,(m_y^1)^2,(m_z^1)^2]).$

在所有结构中，折射率 nprov1由 ε = diag ([(n1)2，(n1)2，(n1)2]) ，mu = diag ([(m1)2，(m1)2，(m1)2])取代。

For slits in perfectly-conducting metallic textures, anisotropy cannot be implemented. 对于完全导电金属织构中的缝隙，各向异性是不能实现的。

 In order to check if the set of textures is correctly set up, the user can set the variable parm.res1.trace equal to 1: “parm.res1.trace = 1;”. 

Then a Matlab figure will show up the refractive-index distribution of all textures. Each

texture is represented with the coordinate x varying from –period/2 to period/2

 为了检查纹理集是否正确设置，用户可以将变量parm.res1.trace设置为1：“parm.res1.trace = 1;”。然后，一个Matlab图将显示出所有纹理的折射率分布。每个纹理都用坐标x表示，其变化范围为-period/2到period/2。



### How to define the layers? 如何定义图层？

This is performed by defining the “Profile” variable which contains, starting from the top layer and finishing by the bottom layer, the successive information (thickness and texture-label) relative to every layer. Here is an example that illustrates how to set up the “Profile” variable:

这是通过定义“Profile”变量来实习的，该变量从顶部层开始，以底部层结束，相对于每个层，顺序包含连续的信息（厚度和纹理标签）。以下是一个示例，演示如何设置“Profile”变量：

```matlab
Profile = {[0,1,0.5,0.5,1,0.5,0.5,2,0],[1,3,2,4,3,2,4,6,2]}; 
```

It means that from the top to the bottom we have: the top layer is formed by a thickness 0 of texture 1, then we have twice textures 3, 2 and 4 with depth 1, 0.5 and 0.5 respectively, texture 6 with depth 2, and finally the bottom layer (formed by texture 2) with null thickness. Since textures 1 and 2 correspond to the top and bottom layers, they must be uniform. In this example, the top and bottom layers have a null thickness. However, one may set an arbitrary thickness. Especially, if one needs to plot the electromagnetic fields in the bottom and top layers, the thicknesses hb and hh (see Fig. 4) over which the fields have to be visualized has to be specified. For hb=hh=0, the Rayleigh expansions of the fields in the top and bottom layers are not plotted.  

这意味着从顶部到底部，我们有：顶部层由纹理1的厚度为0组成，然后我们有两次深度分别为1、0.5和0.5的纹理3、2和4，深度为2的纹理6，最后是由纹理2形成的底部层，厚度为零。由于纹理1和2对应于顶部和底部层，它们必须是均匀的。在这个例子中，顶部和底部层的厚度都为零。然而，可以设置任意厚度。特别地，如果需要绘制底部和顶部层中的电磁场，则必须指定要可视化场的厚度hb和hh（见图4）。对于hb=hh=0，不绘制顶部和底部层中场的Rayleigh展开。

In this particular Profile, the structure formed by texture 3 with thickness 1, texture 2 with thickness 0.5 and texture 4 with thickness 0.5 is repeated twice. It is possible to simplify the instruction defining the “Profile” variable in order to take into account the repetitions:  

在这个特定的“Profile”中，由纹理3（厚度为1）、纹理2（厚度为0.5）和纹理4（厚度为0.5）形成的结构重复了两次。可以简化定义“Profile”变量的指令，因为计算会考虑到重复性：

```matlab
Profile = {{0,1},{[1,0.5,0.5], [3,2,4], 2},{[2,0],[6,2]}};  
```

 If a structure is repeated many times, the above “factorized” instruction of Eq. 2 is better than the “expanded” one of Eq. 1, in terms off computational speed, because the calculation will take into account the repetitions.

The profile is shown below.  如果一个结构需要多次重复，那么上述式子2的“因式分解”指令比式子1的“展开”指令在计算速度上更好，因为计算将考虑到这些重复。

 The profile is shown below. 以下是一个示例变量“Profile”的具体情况。

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403164752176.png" alt="image-20230403164752176" style="zoom:50%;" />

 Fig. 3. Texture stacks. The example corresponds to a profile defined by Profile =  {[hh,1,0.5,0.5,1,0.5,0.5,2, hb],[1,3,2,4,3,2,4,6,2]}; . The top and bottom layers have uniform textures.  

图3. 纹理堆栈。该示例对应于一个由Profile = {[hh,1,0.5,0.5,1,0.5,0.5,2, hb],[1,3,2,4,3,2,4,6,2]}定义的配置文件。顶部和底部层具有均匀的纹理。



 

 

### Solving the eigenmode problem for every texture

求解每个纹理的特征模态问题

The first computation with the RCWA consists in calculating the eigenmodes associated to all textures. This is done by the subroutine “res1.m”, following the instruction:

RCWA 的第一个计算包括计算与所有纹理相关的特征模式。这是由子程序“ res1.m”按照指令完成的:

### res1程序

`计算纹理`

 aa = res1(wavelength,period,textures,nn,k_parallel,parm);  



 

This subroutine has 6 input arguments: the wavelength “**wavelength**”, the period of the grating “**period**”, the “**textures**” variable, the number of Fourier harmonics “**nn**”, the normalized parallel incident wave vector “**k_parallel**, and the “**parm**” variable containing the values of all parameters used by the code and the selected the polarisation. If one has to study the diffraction by different gratings composed of the same textures, one needs to compute only once the eigenmodes. It is possible to save the “aa” variable in a “.mat” file and to reload it for the computation of the diffracted waves, see an example in Annex 10.3.

这个子程序有6个输入参数：

1. 波长“wavelength”，
2. 光栅周期“period”，
3. “textures”变量，
4. 傅里叶谐波的数量“nn”，
5. 归一化的平行入射波矢“k_parallel”，
6. 以及包含代码使用的所有参数值和所选偏振的“parm”变量。

如果需要研究由同一纹理组成的不同光栅的衍射，则只需计算一次特征模式。可以将“aa”变量保存在一个“.mat”文件中，并重新加载以计算衍射波，见附录10.3中的示例。

 

## Computing the diffracted waves

### res2程序

`计算衍射波` 

This is the second step of the computation. This is done by the subroutine “res2.m”, following the instruction:

这是计算的第二步。这是通过子程序“res2.m”完成的，按照以下指示进行：

```matlab
result = res2(aa, Profile);
```

This subroutine has 2 input arguments: the output “**aa**” of the subroutine “res1.m” and the “**Profile**” variable. The output argument “**result**” contains all the information on the diffracted fields. “**result**” is an object of class ‘reticolo’ that can be indexed as an usual structure with parentheses, or with the labels of the considered orders between curly braces. Examples will be given in the following.

这个子程序有两个`输入`参数：

1. 子程序“res1.m”的输出“aa”
2. “Profile”变量。

输出参数“result”包含所有关于衍射场的信息。“result”是一个‘reticolo’类的对象，可以像普通结构体一样用括号进行索引，或使用大括号中的考虑阶级别的标签进行索引。示例将在接下来给出。

This information is divided into the following sub-structures fields :

这些信息分为以下子程序结构`输出`6个字段:

从`上方`入射

```matlab
- “result. inc_top”
- “result. inc_top_reflected”
- “result. inc_top_transmitted”
```

从`下方`入射

```matlab
- “result. inc_bottom”
- “result.inc_bottom_reflected”
- “result. inc_bottom_transmitted”
```



The sub-structure “**result.inc_top_reflected**” contains all the information concerning the propagative *reflected* waves *for an incident wave from the top layer* of the grating. The incident wave is described in the sub-structure “**result.inc_top”**.

子结构“result.inc_top_reflected”包含有关来自光栅顶层的入射波的传播反射波的所有信息。 入射波在子结构“result.inc_top”中描述。

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403165245428.png" alt="image-20230403165245428" style="zoom:50%;" />

Fig. 4. The two obtained solutions.   图4. 获得的两个解决方案。

Each sub-structure of result is composed of the several fields. Each field is a Matlab column vector or matrix having the same number N of lines. N is the number of propagative orders considered and can be 0.  

result的每个子结构由多个字段组成。每个字段都是一个Matlab列向量或矩阵，具有相同的行数N。 N是考虑的传播阶数，可以为0。

 

| Field name   字段名 | Signification   意义                                         | size |
| ------------------- | ------------------------------------------------------------ | ---- |
| order  阶数         | orders of the diffracted  propagative plane waves   衍射传播平面波的阶 | N, 1 |
| theta   Θ           | angle $\theta$m of each diffracted order   每个衍射阶数的角 m | N, 1 |
| **K**               | normalised wave vector   归一化波矢                          | N, 3 |
| efficiency效率      | efficiency of each diffracted  order   每个衍射级数的效率    | N, 1 |
| amplitude   振幅    | complexe amplitude in TE  polarization of every order   各阶 TE 极化中的复振幅 | N, 1 |
| **E**               | electric field (Ex, Ey, Ez) of the diffracted orders  at O_top or O_bottom when the amplitude of the incident plane wave is one.   当入射平面波的振幅为1时，在 O _ 顶或 O _ 底的衍射级数的电场(Ex，Ey，Ez) | N, 3 |
| **H**               | magnetic field (Hx, Hy, Hz) of the diffracted orders  at O_top or O_bottom when the amplitude of the incident plane wave is one.   当入射平面波振幅为1时，在 o _ 顶或 o _ 底的衍射级磁场(Hx，Hy，Hz)。 | N, 3 |
| PlaneWave_E         | E-vector  components of the $\overrightarrow{\text{PW}}$ ’s (in the Oxyz basis) <br /> PW 的 e 向量分量(在 Oxyz 基础上) | N, 3 |
| PlaneWave_H         | H-vector  components of the $\overrightarrow{\text{PW}}$ ’s (in the Oxyz basis)  <br />PW 的 h 向量分量(在 Oxyz 基础上) | N, 3 |

 (To use the same notations as in the conical code or in the crossed-grating code, set parm.res1.result=-1 before calling res1.m).

(要使用与锥形代码或交叉光栅代码相同的符号，在调用 res1.m 之前设置 parm.res1.result =-1)。

 

### Efficiencies 效率

For a given diffraction order n, the diffraction efficiency is defined as the ratio between the flux of the diffracted Poynting vector and the flux of the incident Poynting vector (flux through a period of the grating).

对于给定的衍射阶数n，衍射效率定义为衍射Poynting矢量通量和入射Poynting矢量通量（通过光栅一个周期的通量）之比。



 The efficiencies of all propagative reflected and transmitted waves for an incident wave from the top of the grating are given by the two vectors “**result.inc_top_reflected.efficiency**” and “**result.inc_top_transmitted.efficiency**”. If all refractive indices are real, the sum of all elements of these two vectors is equal to one because of the energy conservation. The labels n of the corresponding orders are in “**result.inc_top_reflected.order**” (see below for a description of the other fields of this sub_structure).

对于来自光栅顶部的入射波的所有传播反射和透射波的效率分别由两个向量“result.inc_top_reflected.efficiency”和“result.inc_top_transmitted.efficiency”给出。 如果所有折射率都是实数，则这两个向量的所有元素之和等于1，因为能量守恒。 相应阶级别的标签n在“result.inc_top_reflected.order”中（有关此子结构的其他字段的描述，请参见下文）

 `Some examples` 一些例子

1. The efficiency of the reflected order -2 ($\quad\text{k}_{//}\text{=}\frac{\text{inc}}{\text{x}}-2\text{K}_X\quad$) when the grating is illuminated from the top is equal to result. inc_top_reflected.efficency{-2}. If this order is evanescent, the efficiency is 0.当光栅从顶部照射时，反射级$\quad\text{k}_{//}\text{=}\frac{\text{inc}}{\text{x}}-2\text{K}_X\quad$的效率等于结果。表面反射。效率{-2}。如果这个顺序是消失的，那么效率是0。

It is important to have in mind the difference between : 

```matlab
result.inc_top_reflected.efficiency{-2} : efficiency of order 2
result.inc_top_reflected.efficiency(-2) : gives an error !
result.inc_top_reflected.efficiency{2} : efficiency of order 2
result.inc_top_reflected.efficiency(2) : efficiency in order result. inc_top_reflected.order(2);
```



1. The orders of all the transmitted-propagative plane waves for an incident wave from the top of the grating are given by the vector “**result.inc_top_transmitted.order**”.

来自光栅顶部的入射波的所有传播透射平面波的级别可以在向量“result.inc_top_transmitted.order”中找到。



1.  The efficiencies of all propagative reflected waves for an incident wave from the bottom in TM polarization are given by the vector “**result.inc_bottom_reflected.efficiency**”.

对于在TM偏振下从底部入射的入射波，所有传播反射波的效率由向量“result.inc_bottom_ reflected.efficiency”给出。



### Rayleigh expansion for propagatives modes

传播模式的瑞利展开

The coefficients of the Rayleigh expansion of Fig. 1 can be obtained from the structure **result**. For instance, when the grating is illuminated from the bottom with a TE polarised mode, we have :

图1的瑞利展开系数可由结构计算结果得到。例如，当光栅从底部用 TE 偏振模式照明时，我们有:

```matlab
Ebottom =result.inc_bottom_reflected.E{m} (3 components in Oxyz)
m
Hbottom =result inc_bottom_reflected.H{m} (3 components in Oxyz)
m
Etop =result.inc_bottom_transmitted.E{m} (3 components in Oxyz)
m
Htop =result.inc_bottom_ transmitted.H{m} (3 components in Oxyz)
```

and the incident plane wave defined in page 4 is given by :

第4页中定义的入射平面波由以下人员给出:

```matlab
Ebottom =result inc_bottom.E (3 components in Oxyz)
inc
Hbottom =result.inc_bottom.H (3 components in Oxyz).
```

### Amplitude of diffracted propagative waves

衍射传播波的振幅

####  入射角度 Angle $\theta_m$


<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403170721968.png" alt="image-20230403170721968" style="zoom:50%;" />



Fig. 5 qm angles. 图5m 角。

 

The angle qm related to order m is varying between –90 and 90. It is oriented in such a way that the k-parallel momentum of the corresponding wave vector (incident or diffracted) is

与阶数m相关的角度θm在-90度至90度之间变化。它的方向安排是这样的，使得相应波矢（入射或衍射）的k-parallel动量为：

$\text{k_x}^{\text{inc}}+\text{mk_x}=(2\pi/\lambda)\text{n_top}\sin(\Theta_\text{m})\text or (2\pi/\lambda)\text{n_bottom_}\sin(\Theta_\text{m})$ 有点错误

$$

= (2π/λ) n_top sin(qm) or (2π/λ) n_bottom_sin(qm).








###  $O_{top}$ and $O_{bottom}$ points 最高点和最低点

Otop and Obottom are 2 important points (see Fig. 1). In the Cartesian coordinates system Oxyz , they are defined by: Otop=(0,0,h) at the top of the grating, and Obottom=(0,0,0) at the bottom of the grating.

Otop和Obottom是两个重要点（见图1）。 在笛卡尔坐标系Oxyz中，它们分别定义为：

Otop =（0,0，h）在光栅顶部， Obottom =（0,0,0）在光栅底部。

  


In addition, let us consider an arbitrary point M=(x,y,z) in the 3D space in Oxyz. Associated to this point, we define the two vectors :

另外，让我们考虑Oxyz中三维空间中的任意点M =（x，y，z）。 与此点相关联，我们定义两个向量：

$\quad\mathbf{r}_{\text{top}=}\overline{\mathrm{O}_{\text{top}}{\text{M}}}$, and

$\quad\mathbf{r}_{\text{bottom}=}\overline{\mathrm{O}_{\text{bottom}}{\text{M}}}$.



 

### Jones’ coefficient 琼斯系数

Let us assume that the grating is illuminated from the top layer and let us consider a diffracted order m in the bottom layer. Any other diffraction situation is straighforwardly deduced.

让我们假设光栅是从顶层照明，让我们考虑一个衍射阶数 m 在底层。任何其他衍射情况都是直接推导出来的。

Let α be a given complex number. The incident electromagnetic field (6 components of **E** and **H** in every points of the 3D space) can be written :

设 α 是给定的复数。入射电磁场(三维空间中每个点上的 e 和 h 的6个分量)可以写成:

$\mathbf{W}^{\text{inc}}=\alpha\overrightarrow{\mathbf{PW}}$

where PW is a plane wave defined in every point by PW=A exp(ikinc top rtop), A being the electromagnetic fields (6 components) of the plane wave at M=Otop, and kinc top is the incident wave vector. A and K=kinc top / kinc top are given by the structure “result“ as will be defined later.

Similarly, the diffracted electromagnetic field in the m bottom order can be written :

其中，PW是由PW = A exp（ikinc top rtop）在每个点定义的平面波，其中A是平面波在M = Otop处的电磁场（6个分量），而kinc top是入射波矢量。向量A和K = kinc top / kinc top由结构“result”给出，稍后将进行定义。

同样地，m级别的衍射电磁场可以写成：

$\mathbf{W}_\mathrm{m}^{\mathrm{dif}}=\gamma\overline{\mathbf{PW^m}}$

where $\gamma$ is a complex number, PWm is a plane wave defined in every point by PWm=Am exp (ikm bottom rbottom ), Am is the electromagnetic fields (6 components) of the plane wave at M=Obottom, and km bottom is the wave vector of the mth transmitted order. Am and, Km=kmbottom / kmbottom are given by the structure “result“ as will be defined later.

We define the Jones’coefficient J, associated to the order m by

其中，γ是一个复数，PWm是由PWm = Am exp（ikm bottom rbottom）在每个点定义的平面波，其中Am是平面波在M = Obottom处的电磁场（6个分量），而km bottom是第m个透射级别的波矢量。向量Am和Km = kmbottom / kmbottom由结构“result”给出，稍后将进行定义。

我们通过定义与阶数m相关联的Jones系数J来完成：

待添加

​                 







## Using symmetries to accelerate the computational speed

`使用对称性来加快计算速度`

When the grating possesses some mirror symmetry for the plane x=x0, one may define “parm.sym.x= x0. Then

when k_parallel =0, the code will use the symmetry property for speeding up the calculation.

当光栅在x = x0平面处具有某些镜像对称性时，可以定义“parm.sym.x = x0”。然后，当k_parallel = 0时，代码将使用对称性属性加快计算速度。

Note that the code does not verify if the symmetries of the grating defined by the user are in agreement with the “textures” parameters. It is up to the user to define carefully the parameters parm.sym.x. All textures used in the calculation must possess the same symmetry.

请注意，代码不验证用户定义的光栅的对称性是否与“textures”参数一致。用户必须仔细定义参数parm.sym.x。计算中使用的所有纹理必须具有相同的对称性。

 

## Plotting the electromagnetic field and calculating the absorption loss

### res3程序

`绘制电磁场并计算吸收损耗`

Computation of the electromagnetic fields 计算电磁场

Once the eigenmodes associated to all textures are known, the calculation of the electromagnetic fields everywhere in the grating can be performed. This calculation is done by the function “**res3.m**”, following the instruction:

一旦知道了所有纹理的本征模式，就可以计算光栅中各处的电磁场。这个计算是由函数“ res3.m”按照指令完成的:

```matlab
[e,z,index] = res3(x,aa,Profile, inc,parm);
```

The function“res3.m” can be called without calling “res2.m”. This subroutine has 5 input arguments:
-the “x” variable is a vector containing the locations where the fields will be calculated in the x-direction [for
instance we may set x = linspace(-period_x/2, period_x/2, 51); for allocating 51 sampling points in the xdirection],
the “aa” variable contains all the information on the eigenmodes of all textures and is computed by the subroutine
res1.m,
-the variable “Profile” is defined in Section 4.2; note that it can be redefined,
-the variable “inc” defines the y component of the complex amplitude of the incident electric (in TE polarisation)
or magnetic field (in TM polarisation) field at O_top or O_bottom .
For illuminating the grating exactly by the TE-polarized incident PW defined above, one should set:
einc= result.inc_top PlaneWave_E(2) for TE polarisation; einc= result.inc_top PlaneWave_H(2) for TM
polarisation.
-the “parm” variable, already mentioned is discussed in the following.
There are three possible output arguments for the subroutine “res3.m”. The variable “e” contains all the
electromagnetic field quantities:  

函数“res3.m”可以在不调用“res2.m”的情况下调用。该子程序具有`5个输入`参数： 

1. “x”变量是一个向量，其中包含在x方向上计算场的位置[例如，我们可以将x = linspace（- period_x / 2，period_x / 2，51）;分配51个采样点以在x方向进行采样]，

2. “aa”变量包含所有纹理的特征模式信息，并由子程序res1.m计算

3. 变量“Profile”在第4.2节中定义。请注意，它可以重新定义

4. 变量“inc”定义入射电场的复振幅的y分量（在TE偏振中）或磁场（在TM偏振中）在O_top或O_bottom处。 为了精确地用上述TE偏振入射PW照明光栅，应设置： 对于TE偏振，einc = result.inc_top PlaneWave_E（2）;对于TM偏振，einc = result.inc_top PlaneWave_H（2）。 

5. “parm”变量是已经提到的，在下面进行了讨论。 

   

子程序“res3.m”有`三个`输出变量。

- “e”变量包含所有电磁场量：

```matlab
Ey=e(:,:,1); Hx=e(:,:,2); Hz=e(:,:,3); in TE polarization.
Hy=e(:,:,1); Ex=e(:,:,2); Ez=e(:,:,3); in TM polarization.
```

The second variable “z” is the vector containing the z-coordinate of the sampling points. Note that in the matrix Ex=e(:,:,1), the first index refer to the z coordinate, and the second to the x-coordinate. Thus Ex(i,j) is the Ex field component at the location {z(i), x(j)}. The third variable “index” is the complex refractive index of the considered grating. index(i,j) is the refractive index at the location {z(i), x(j)}. It can be useful to test the profile of the grating.

- 第二个变量“z”是包含采样点z坐标的向量。请注意，在矩阵Ex = e（：，：，1）中，第一个索引是z坐标，第二个是x坐标。 因此，Ex（i，j）是位于{z（i），x（j）}位置处的Ex场分量。第三个变量“index”是所考虑光栅的复折射率。 index（i，j）是在{z（i），x（j）}位置处的折射率。它可以用于测试光栅的轮廓。


 

Some **important** comments on the **parm**” variable : 关于“parm”变量的一些重要注释：



1. For calculating precisely the electromagnetics fields, one has to set : ”**parm.res1.champ=1”** before calling **res1.m.** This increases the calculation time and memory load, but it is highly recommended. If not, the computation of the field will be correct only in homogenous textures (for example in the top layer and in the bottom layer). 1.为了精确计算电磁场，必须在调用res1.m之前设置：“parm.res1.champ=1”。这会增加计算时间和内存负荷，但强烈建议这样做。否则，在均匀纹理（例如在顶层和底层）中才能正确计算场。
2. Illuminating the grating from the top or the bottom layer : As mentioned earlier, the code compute the diffraction efficiencies of the transmitted and reflected orders for an incident plane wave from the top and for an incident plane wave from the bottom at the same time. When plotting the field, the user must specify the direction of the incident plane wave. This is specified with variable **parm.res3.sens**. For **parm.res3.sens=1**, the grating is illuminated from the top and for **parm.res3.sens=-1**, the grating is illuminated from the bottom (default is **parm.res3.sens=1)**. 2.从顶层或底层照射光栅：如前所述，该代码同时计算从顶部和从底部入射平面波的透射和反射阶数的衍射效率。在绘制场时，用户必须指定入射平面波的方向。这是使用变量parm.res3.sens指定的。对于parm.res3.sens = 1，从顶部照亮光栅，而parm.res3.sens = -1则从底部照亮光栅（默认值为parm.res3.sens = 1）。
3. Specifying the z locations of the computed fields: This is provided by the variable **parm.res3.npts**. **parm.res3.npts** is a vector whose length is equal to the number of layers. For instance let us imagine, a grating defined by **Profile** = {[0.5,1,2,0.6],[1,2,3,4]}. Setting **parm.res3.npts=[2,3,4,5]** implies that the field will be computed in two z=constant plans in the top layer, in three z=constant plans in the first layer (texture 2), in four z=constant plans in the second layer (texture 3), and in five z=constant plans in the bottom layer. Default for **parm.res3.npts** is 10 z=constant plans per layer. 指定计算场的z位置：这由变量parm.res3.npts提供。parm.res3.npts是一个向量，其长度等于层数。例如，假设存在一个由Profile = {[0.5,1,2,0.6],[1,2,3,4]}定义的光栅。设置parm.res3.npts=[2,3,4,5]意味着将在顶层的两个z = constant平面中计算场，在第一层（纹理2）中的三个z = constant平面中计算场，在第二层（纹理3）中的四个z = constant平面中计算场，并在底层的五个z = constant平面中计算场。parm.res3.npts的默认值是每层10个z = constant平面。

`VERY IMPORTANT` 非常重要

where is the z=0 plan and what are the z-coordinates of the z=constant plan? The z=0 plan is defined at the bottom of the bottom layer. Thus, the field calculation is performed only for z>0 values. For the example **Profile** = {[0.5,1,2,0.6],[1,2,3,4]}, and if we refer to texture 4 as the substrate, the z=0 plan is located in the substrate at a distance 0.6 under the grating. The z=constant plans are located by an equidistant sampling in every layer. Always referring to the previous example, it implies that the five z=constant plans in the substrate are located at coordinate z=(p-0.5) 0.6/5, where p=1,2,…5. Note that the z coordinates for the z=constant plans are always given by the second output variable of res3.m.

z=0平面在底层底部定义。因此，场计算仅在z> 0值时执行。对于示例Profile = {[0.5,1,2,0.6]，[1,2,3,4]}，如果将纹理4称为基板，则z = 0平面位于光栅下0.6的距离处的基板上。 z = constant平面是在每个层中通过等距采样来定位的。始终参考之前的例子，意味着底层中的五个z = constant平面位于z =（p-0.5）0.6/5的坐标处，其中p = 1,2，… 5。请注意，z = constant平面的z坐标始终由res3.m的第二个输出变量给出。



4. How can one specify a given z=constant plan? First, one has to redefine the variable **Profile**. For the grating example with the two layers discussed above, let us imagine that one wants to plot the field at z=z0+0.6+0.2 in layer 2. Then one has to set: **Profile** = {[0.5,1-z0,0,z0,0.2,0.6],[1,2,2,2,3,4]} and set **parm.res3.npts=[0,0,1,0,0,0]**. Note that it is not necessary to redefine the variable **Profile** at the beginning of the program. One just needs to redefine this variable before calling subroutine res3.m. 如何指定给定的z = constant平面？首先，必须重新定义变量Profile。对于上面讨论的两个层的光栅示例，假设想要在第2层的z = z0 + 0.6 + 0.2处绘制场。然后，必须设置：Profile = {[0.5,1-z0,0,z0,0.2,0.6]，[1,2,2,2,3,4]}，并设置parm.res3.npts = [0,0,1,0,0,0]。请注意，在程序开头重新定义变量Profile是不必要的。只需要在调用子程序res3.m之前重新定义此变量即可。

 

5. Automatic plots: an automatic plot (showing all the components of the electromagnetic fields and the grating refractive index distribution) is provided by setting **parm.res3.trace**=1. If one wants to plot only some components of the fields, one can set for instance in TE polarization: **parm.res3.champs**=[1,0] to plot Ey and the objet, **parm.res3.champs**=[2] to plot only Hx. 自动绘图：通过设置parm.res3.trace = 1，可以提供自动绘图（显示电磁场和光栅折射率分布的所有组件）。如果只想绘制场的某些组件，则可以在TE偏振中设置例如parm.res3.champs = [1,0]绘制Ey和物体，parm.res3.champs = [2]只绘制Hx。



 

### Computation of the absorption loss

吸收损失的计算

Loss computation is performed with the subroutine “**res3.m**”.

损耗计算使用子程序“ res3.m”执行。

 

First approach based on integrals (not valid for homogeneous layers with non-diagonal anisotropy): The absorption loss in a surface 𝑆 is given by:

第一种基于积分的方法（不适用于具有非对角各向同性的均匀层）：

表面𝑆的吸收损耗由以下公式给出：


 𝐿 = 𝜋 ∫ 𝐼𝑚 𝜀(𝑀) |𝐸 (𝑀)|2 𝑑𝑆 for TE polarization.

𝐿 = 𝜋 ∫ 𝐼𝑚 (𝜀𝑋𝑋(𝑀)|𝐸𝑋(𝑀)|2 + 𝜀𝑍𝑍(𝑀)|𝐸𝑧(𝑀)|2) 𝑑𝑆 for TM polarization.

```matlab
[e, Z, index, wZ, loss_per_layer, loss_of_Z, loss_of_Z_X, X, wX] = res3(x,aa,Profile,einc,parm);
```

The important ouput arguments are: 重要的输出参数是:

**loss_per_layer**: the loss in every layer defined by **Profile**, **loss_per_layer**(1) is the loss in the top layer, loss_per_layer(2) is the loss in layer 2, ... and loss_per_layer(end) is the loss in the bottom layer 

loss_of_Z: the absorption loss density (integrated over X) as a function of Z (like for X, the sampling points Z are not equidistant. You may plot this loss density as follows: plot(Z, loss_of_Z), xlabel('Z'), ylabel('absorption') 

loss_of_Z_X(Z,X) = π/λ Im(index(Z,X).^2) |e(Z,X,1)|2 in TE polarization 

loss_of_Z_X(Z,X) = π/λ Im(index(Z,X).^2) ( e(Z,X,2)|2+|e(Z,X,3)|2) in TM polarization 

index: index(i,j) is the complex refractive index at the location {z(i), x(j)}.

每层损耗: 由 Profile 定义的每层损耗，每层损耗(1)是顶层损耗，每层损耗(2)是第2层损耗，... 每层损耗(末端)是底层损耗(z) : 吸收损耗密度(在 x 上积分)与 z 的函数关系(如 x，取样点 z 不等距)。您可以将这个损失密度绘制如下: 绘图(z，_ z 的损失) ，xlabel (‘ z’) ，ylabel (‘吸收’) _ z _ x (z，x)的损失 _ = π/λim (指数(z，x)。_ z _ x (z，x) = π/λim (index (z，x)的 TE 偏振损耗 _ 中的 ^ 2) | e (z，x，1) | 2。TM 偏振指数中的 ^ 2)(e (z，x，2) | 2 + | e (z，x，3) | 2) : 指数(i，j)是{ z (i) ，x (j)}处的复折射率。

 

Second approach based on Poynting theorem (always valid, even for homogeneous layers with non-diagonal anisotropy):

基于 Poynting 定理的第二种方法(总是有效的，即使对于非对角各向异性的均匀层) :

An alternative approach to compute the losses in the layers consists in calculating the difference in the flux of the incoming and outgoing Poynting vectors. This approach is faster, but in some cases, the computation of the integral can be more accurate. In homogeneous layers with non-diagonal anisotropy, only this approach is possible.

另一种计算各层损耗的方法是计算输入和输出 Poynting 向量的通量差。这种方法更快，但在某些情况下，积分的计算可以更精确。在非对角各向异性的均匀层中，只有这种方法是可行的。

To specify which approach used per layer, we define a vector parm.res3.pertes_poynting = [0,0,0,1,0]; % for instance for a 5-layer grating with “0”, the integral approach is used (default option) and with “1”, the Poynting approach is used. The length of parm.res3.pertes_poynting is equal to the number of layers. We may set parm.res3.pertes_poynting = 0 or 1; the scalar is then repeated for all layers.

为了指定每层使用的方法，我们定义了一个向量 parm.res3.pertes _ Poynting = [0,0,0,1,0] ; 例如，对于5层光栅，使用“0”，使用积分方法(默认选项) ，对于“1”，使用 Poynting 方法。Parm.res3.pertes _ poynting 的长度等于层数。我们可以设置 parm.res3.pertes _ poynting = 0或1; 然后对所有层重复标量。

We may then compute the flux of the Poynting vector in the layer-boundary planes [e, Z, index, wZ,loss_per_layer,loss_of_Z,loss_of_Z_X,X,wX,Flux_Poynting] = res3(x,aa,Profile,einc,parm);

然后我们可以计算 Poynting 向量在层边界面[ e，z，index，wz，loss _ per _ layer，loss _ z，loss _ of _ zx，x，wx，flux _ Poynting ] = res3(x，aa，Profile，einc，parm)中的通量;

**Flux_Poynting** is a vector. **Flux_Poynting(1)** corresponds to the upper interface of the top layer. The flux is computed for a normal vector equal to the 𝐳̂vector. If **Flux_Poynting(p)** > 0, the energy flows toward the top and if it is negative, the energy flows toward the bottom.

**Flux _ poynting 是一个矢量。Flux _ poynting (1)对应于顶层的上层界面。通量是针对一个等于 something 矢量的法向量计算的。如果 Flux _ poynting (p) > 0，能量流向顶部，如果它是负的，能量流向底部。**

For an illumination from the top and a lossy substrate, the substrate absorption is **-****Flux_Poynting (end)/(0.5\*period)**. For an illumination from the bottom and a lossy superstrate, the superstrate absorption is **Flux_Poynting (1)/(0.5\*period)**.

对于来自顶部和有耗基板的照明，基板的吸收是 Flux _ poynting (end)/(0.5 * period)。对于来自底部和有耗上层的照明，上层吸收是 Flux _ poynting (1)/(0.5 * period)。



`Note on the computation accuracy of the integral approach` 关于积分法计算精度的注意事项

To compute integrals like the loss or the electromagnetic energy, RETICOLO uses a Gauss-Legendre integration method. This method, which is very powerful for 'regular' functions, becomes inaccurate for discontinuous functions. Thus, the integration domain should be divided into subdomains where the electric field **E** is continuous. For the integration in **X**, this difficult task is performed by the program, so that the user should only define the limits of integration: the input “**x**” argument is now a vector of length 2, which represent the limits of the x interval (to compute the loss over the entire period, we may take **x**(2)=**x**(1)+**period**. The integration domain is then divided into subintervals where the permittivity is continuous, each subinterval having a length less than l/(2p). For every subinterval, a Gauss-Legendre integration method of degree 10 is used. This default value can be changed by setting **parm.res3.gauss_x**=. The actual points of computation of the field are returned in the output argument

为了计算像损耗或电磁能这样的积分，RETICOLO 使用了 Gauss-Legendre 积分法。这种方法对于“正则”函数非常有效，但是对于不连续的函数就不准确了。因此，积分域应该被划分为电场 e 是连续的子域。对于 x 中的积分，这个困难的任务是由程序执行的，因此用户只需要定义积分的极限: 输入“ x”参数现在是一个长度为2的向量，它表示 x 区间的极限(为了计算整个周期的损失，我们可以采用 x (2) = x (1) + 周期)。然后将积分域划分为介电常数连续的子区间，每个子区间的长度小于/(2)。对于每个子区间，使用10度的 Gauss-Legendre 积分方法。这个默认值可以通过设置 parm.res3.gauss _ x = 来改变。字段的实际计算点在输出参数中返回X.

For the z integration, the discontinuity points are more easily determined by the variable 'Profile'. The user

may choose the number of subintervals and the degree in every layer using the parameter parm.res3.npts, which is now an array with two lines (in subsection 8.1 this variable is a line vector): the first line defines the degree and the second line the numbers of subintervals of every layer. For example: parm.res3.npts = [ [10,0,12] ; [3,1,5] ]; means that 3 subintervals with 10-degree points are used in the first layer, 1 subintervals with 0 point in the second layer, 5 subintervals with 12degree points in the third layer.

对于z积分，不连续点可以更轻松地通过变量“Profile”确定。用户可以使用参数parm.res3.npts选择每个层中的子区间数和度数，该参数现在是一个带有两行的数组（在第8.1小节中，此变量是线向量）：第一行定义度数，第二行定义每个层的子区间数。例如：parm.res3.npts =[ [10,0,12];[3,1,5]]; 表示在第一层中使用3个子区间和10度点，第二层中使用1个子区间和0点，第三层中使用5个子区间和12度点。

The actual z-points of computation of the field are returned in the output variable **Z**, and the vector **wZ** represents the weights and we have sum(**loss_of_Z**.***wZ**)=sum(**loss_per_layer**). Although the maximum degree that can be handled by reticolo is 1000, it is recommended to limit the degree values to modest numbers (10-30 maximum) and to increase the number of subintervals (the larger the degree, the denser the sampling points in the vicinity of the subinterval boundaries).

字段计算的实际 z 点在输出变量 z 中返回，向量 wZ 表示权重，我们有 _ z 的总和(损失 _)。wZ) = 总和(每层损失)。尽管 reticolo 可以处理的最大程度是1000，但建议将程度值限制为适度数(最大10-30) ，并增加子区间的数目(程度越大，子区间边界附近的采样点越密集)。

Note that if **einc**= **result. inc_top PlaneWave_E(2)**, in TE ploarization, or **einc**= **result. inc_top PlaneWave_H(2)**, in TE ploarization **,** the energie conservation test for an incident plane wave from the top is sum(result. inc_top_reflected.efficiency)+ sum(result. inc_top_transmitted.efficiency)+ sum(loss_per_layer) / (.5*period) = 1.

注意，如果 einc = result。Inc _ top PlaneWave _ e (2) ，TE 极化，或 einc = result。在 TE 极化条件下，从顶部入射的平面波的能量守恒实验是求和(结果)。反射。效率) + 总和(结果)。传输。效率) + 总和(每层损失)/(. 5周期) = 1。

Usually, this equality is achieved with an absolute error of <10-5.

通常，这种等式是在绝对误差 < 105时实现的。

` For specialists: 对于专家`:

1. -loss_of_Z_X =pi/ wavelength*imag(index.^2).* abs(e(:,:,1)).^2; in TE polarization
2. -loss_of_Z_X =pi/ wavelength*imag(index.^2).*sum(abs(e(:,:,2:3)).^2,3); in TM polarization
3. -loss_of_Z =(loss_of_Z_X*wX(:)).';
4. -by setting index(index ~= index_chosen)=0 in the previous formulas, one may calculate the absorption loss in the medium of refractive index index_chosen.  

通过在先前的公式中设置index（index〜=index_chosen）= 0，可以计算折射率为index_chosen的介质中的吸收损耗。

## Bloch-mode effective indices

`Bloch模式有效指数`

RETICOLO gives access to another output: the Bloch mode associated to all textures. The Bloch mode k of the

texture l can be written

RETICOLO提供了另一种输出：与所有纹理相关联的布洛赫模。纹理l的布洛赫模k可以写成：

$\left|\Phi_k{}^l\right\rangle=\sum_m a_m^{k,l}exp\left[i(k_x^{inc}+mK_x)x\right]exp\left(i\frac{2\pi}{\lambda}n_{eff}^{k,l}z\right)$,

where $n_{\textit{eff}}^{k,l}$ is the effective index of the Bloch mode *k* of the texture *l*.

其中，$n_{\textit{eff}}^{k,l}$是纹理l的布洛赫模k的有效指数。



`Instruction:`说明:

```matlab
[aa, n_eff] = res1(wavelength,period,textures,nn,kparallel, parm);
```

Note that the “n_eff” variable is a Matlab cell array: “n_eff{ii}” is a column vector containing all the Bloch-mode effective indices associated to the texture “textures{ii}”. The element number 5 of this vector, for example, is called by the instruction “n_eff{ii}(5);”. An attenuated Bloch-mode has a complex effective index.

请注意，“n_eff”变量是Matlab单元数组：“n_eff {ii}”是包含所有与纹理“textures {ii}”相关联的布洛赫模有效指数的列向量。例如，此向量的第5个元素由指令“n_eff {ii}（5）;”调用。衰减的布洛赫模具有复有效指数。



`Bloch mode profile visualization` Bloch 模式剖面可视化:



To plot the profile of Bloch mode Num_mode of the texture Num_texture:

要绘制纹理Num_texture的Bloch模Num_mode的轮廓：

```matlab
res1(aa, neff, Num_texture, Num_mode);
```

To obtain the profile datas in the format given by res3:

要以res3给出的格式获取轮廓数据：

```matlab
[e,o,x] = res1(aa, neff, Num_texture, Num_mode); % by default, |x| < period/2
[e,o] = res1(aa, neff, Num_texture, Num_mode, x); % by specifying the x vector, x=linspace(0, 3*period(1),100)
for example.
```

## 10 Annex 附件

### 10.1 Checking that the textures are correctly set up

检查纹理设置是否正确

Setting “**parm.res1.trace = 1**;” generates a Matlab figure which represents the refractive-index distribution of all the textures.

设置“ parm.res1.trace = 1;”生成一个代表所有纹理折射率分布的 Matlab 图形。

 

### 10.2 The “retio” & “retefface” instructions

RETICOLO automatically creates temporary files in order to save memory. These temporary files are of the form “abcd0.mat”, “abcd1.mat” … with abcd are randomly chosen) .They are created in the current directory. In general RETICOLO automatically erases these files when they are no longer needed, but it is recommended to finish all programs by the instruction “retio;”, which erases all temporary files. Also, if a program anormally stopsone may execute the instruction “retio” before restarting the program.

RETICOLO会自动创建临时文件以节省内存。这些临时文件的格式为“abcd0.mat”，“abcd1.mat”……其中abcd是随机选择的）。它们在当前目录中创建。一般情况下，RETICOLO在不再需要这些文件时会自动删除它们，但建议通过指令“retio;”结束所有程序，该指令将删除所有临时文件。此外，如果程序异常停止，可以在重新启动程序之前执行指令“retio”。

 

The “retefface” instruction allows to know all the “abcd0.mat” files and to erase them if wanted.

“ reteface”指令允许知道所有“ abcd0.mat”文件，并在需要时删除它们。

 

If we are not limited by memory (this is often the case with modern computers), we can prevent the writing of intermediate files on the hard disk by the setting

如果我们不受内存的限制(现代计算机通常就是这种情况) ，我们可以通过设置来防止在硬盘上写入中间文件

```matlab
parm.not_io = 1;
```

before the call to res1. Then it is no longer necessary to use the retio instruction at the end of the programs to erase the files.

在调用 res1之前。然后就不再需要在程序结束时使用 retio 指令来删除文件了。

`Important`: to use parfor loops, it is imperative to take the option parm.not_io = 1.

重要提示: 要使用 parfor 循环，必须使用选项 parm.not _ io = 1。

 

### **10.3.**   How to save and to reload the “aa” variable

如何保存和重新加载“ aa”变量

To save the “**aa**” variable in a “.mat” file, the user has to define a new parameter containing the name of the file he or she wants to create : “**parm.res1.fperm = 'file_name'**;”. field_name is a char string with at least one letter. The program will automatically save “**aa**” in the file “**file_name.mat**”. In a new utilisation it is sufficient to write aa=**= 'file_name'**;.

将“ aa”变量保存到“。在 mat”文件中，用户必须定义一个新参数，其中包含他或她想要创建的文件的名称: “ parm.res1.fperm = ‘ file _ name’;”。Field _ name 是一个至少有一个字母的字符串。程序会自动将“ aa”保存到文件“ file _ name”中。马特。在一个新的应用程序中，写 aa = = ‘ file _ name’就足够了;。

 

Example of a program which calculates and saves the “aa” variable [...] % Definition of the input parameters, see Section 3 **parm.res1.fperm = 'toto'**;

计算并保存输入参数的“ aa”变量[ ... ]% 定义的程序示例，参见第3节 parm.res1.fperm = ‘ toto’;

[...] % Definition of the textures, see Section 4.1

[ ... ]% 纹理的定义，参见第4.1节

**aa = res1(wavelength,period,textures,nn,k_parallel,parm)**;

**Aa = res1(波长，周期，纹理，nn，k 平行，parm) ;**

Example of a program which uses the “aa” variable and then calculates the diffracted waves [...]  % Definition of the profile, see Section 4.2. Note that the textures used to define the profile argument have to correspond to the textures defined in the program which has previously calculated the “aa” variable. aa=’toto’;

程序使用“ aa”变量，然后计算衍射波[ ... ]% 轮廓的定义，参见第4.2节。注意，用于定义配置文件参数的纹理必须与之前计算“ aa”变量的程序中定义的纹理相对应。Aa =’toto’;

### **10.4.**   Asymmetry of the Fourier harmonics retained in the computation

 nn = [-15;20]; % this defines the set of non-symmetric Fourier harmonics retained for the computation. In this

case, the Fourier harmonics from –15 to +20 are retained.

The instructions “nn = 10;” and “nn = [-10;10];” are equivalent.

Take care that the use of symmetry imposes symmetric Fourier harmonics if not the computation will be done

without any symmetry consideration.

nn = [-15; 20];% 这定义了计算中保留的非对称傅里叶谐波集。在这种情况下，保留从-15到+20的傅里叶谐波。 “nn = 10;”和“nn = [-10; 10];”指令是等价的。请注意，如果不使用对称性，则使用对称傅里叶谐波进行计算，否则将完全没有考虑对称性。

##  11  Summary

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230403230539759.png" alt="image-20230403230539759" style="zoom:50%;" />

```matlab
parm = res0( 1) for TE polarisation;
parm = res0(-1) for TM polarisation;
aa = res1(wavelength,period,textures,nn,k_parallel,parm);
result = res2(aa,Profile);
J = result.Jones.inc_top_transmitted {m}
[e,z,o] = res3(x,aa,Profile, inc,parm);
```

## 12 Examples  例子

 The following example can be copied and executed in Matlab ：

```matlab
%%%%%%%%%%%%%%%%%%%%%%%%%
% EXAMPLE 1D (TE or TM) %
%%%%%%%%%%%%%%%%%%%%%%%%%
wavelength=8;
period=10;% same unit as wavelength
n_incident_medium=1;% refractive index of the top layer
n_transmitted_medium=1.5;% refractive index of the bottom layer
angle_theta0=-10;k_parallel=n_incident_medium*sin(angle_theta0*pi/180);
parm=res0(1);% TE polarization. For TM : parm=res0(-1)
parm.res1.champ=1;% the electromagnetic field is calculated accurately
nn=40;% Fourier harmonics run from [-40,40]
% textures for all layers including the top and bottom layers
texture=cell(1,3);
textures{1}= n_incident_medium; % uniform texture
textures{2}= n_transmitted_medium; % uniform texture
textures{3}={[-2.5,2.5],[n_incident_medium,n_transmitted_medium] };

aa=res1(wavelength,period,textures,nn,k_parallel,parm);
Profile={[4.1,5.2,4.1],[1,3,2]};
one_D_TE=res2(aa,Profile)
eff=one_D_TE.inc_top_reflected.efficiency{-1}
J=one_D_TE.Jones.inc_top_reflected{-1};% Jones’coefficients
abs(J)^2 % first order efficiency for an illumination from the top layer
% field calculation
x=linspace(-period/2,period/2,51);% x coordinates(z-coordinates are determined by
res3.m)
einc=1;
parm.res3.trace=1; % plotting automatically
parm.res3.npts=[50,50,50];
[e,z,index]=res3(x,aa,Profile,einc,parm);
figure;pcolor(x,z,real(squeeze(e(:,:,1)))); % user plotting
shading flat;xlabel('x');ylabel('y');axis equal;title('Real(Ey)');

% Loss calculation
textures{3}={[-2.5,2.5],[n_incident_medium,.1+5i] };
aa_loss=res1(wavelength,period,textures,nn,k_parallel,parm);
one_D_loss=res2(aa_loss,Profile)
parm.res3.npts=[[0,10,0];[1,3,1]];
einc=one_D_loss.inc_top.PlaneWave_E(2);
[e,z,index,wZ,loss_per_layer,loss_of_Z,loss_of_Z_X,X,wX]=res3([-
period/2,period/2],aa_loss,Profile,einc,parm);
Energie_conservation=sum(one_D_loss.inc_top_reflected.efficiency)+sum(one_D_loss.in
c_top_transmitted.efficiency)+sum(loss_per_layer)/(.5* period)-1
retio % erase temporary files
```












# for the analysis of the diffraction by stacks of lamellar 1D gratings (conical diffraction)

`用于分析层状一维光栅的衍射(锥形衍射)`

 

 

Reticolo code 1D-conical is a free software for analyzing 1D gratings in classical and conical mountings. It operates under Matlab. To install it, copy the companion folder “reticolo_allege” and add the folder in the Matlab path. The code may also be used to analyze thin-film stacks with homogeneous and anisotropic materials, see the end of Section 3.1.

Reticolo 代码1d-锥是一个免费的软件，用于分析一维光栅在经典和锥形安装。它在 Matlab 下运行。要安装它，复制伴随文件夹“ reticolo _ allege”，并将该文件夹添加到 Matlab 路径中。该代码也可用于分析均质和各向异性材料的薄膜堆栈，参见第3.1节的结尾。

 

## Outline 大纲

## Generality 概括

RETICOLO is a code written in the language MATLAB 9.0. It computes the diffraction efficiencies and the diffracted amplitudes of gratings composed of stacks of lamellar structures. It incorporates routines for the calculation and visualisation of the electromagnetic fields inside and outside the grating. With this version, 2D periodic (crossed) gratings cannot be analysed.

RETICOLO 是用 MATLAB 9.0语言编写的代码。它计算由层状结构堆叠组成的光栅的衍射效率和衍射振幅。它包含了用于计算和可视化光栅内外电磁场的例程。有了这个版本，二维周期(交叉)光栅不能被分析。

 

As free alternative to MATLAB, RETICOLO can also be run in GNU Octave with minimal code changes. For further information, please contact tina.mitteramskogler@profactor.at.

作为 MATLAB 的免费替代品，RETICOLO 也可以在 GNU Octave 中运行，代码变化很小。欲了解更多信息，请联系 tina.mitteramskogler@profactor.at。

 

In brief, RETICOLO implements a frequency-domain modal method (known as the Rigorous Coupled wave Analysis/RCWA). To get an overview of the RCWA, the interested readers may refer to the following articles:

简而言之，RETICOLO 实现了一种频域模态方法(称为严格耦合波分析/RCWA)。为了得到 RCWA 的概述，感兴趣的读者可以参考以下文章:

1D-classical and conical diffraction

1d-经典和圆锥衍射

 

**Scattering matrix approach:** The code incorporates many refinements that we have not published and that we do not plan to publish. For instance, although it is generally admitted that the S-matrix is inconditionnally stable, it is not always the case. We have developed an in-house transfer matrix method which is more stable and accurate. The new transfer matrix approach is also more general and can handle perfect metals. The essence of the method has been rapidly published in "J.-P. Hugonin, M. Besbes and P. Lalanne, Op. Lett. **33**, 1590 (2008)".

**散射矩阵方法: 该代码包含了许多我们没有发表过也不打算发表的改进。例如，尽管人们普遍承认 s 矩阵是无条件稳定的，但事实并非总是如此。我们开发了一种更稳定和准确的内部转移矩阵方法。新的转移矩阵方法也更加通用，可以处理完美的金属。这种方法的精髓已经在《日报》上迅速发表。作者: Hugonin，m. Besbes and p。莱特。33,1590(2008)”。**

 

**Field calculation:** The calculation of the near-field electromagnetic fields everywhere in the grating is performed according to the method described in "P. Lalanne, M.P. Jurek, JMO **45**, 1357 (1998)" and to its generalization to crossed gratings (unpublished). Basically, no Gibbs phenomenon will be visible in the plots of the discontinuous electromagnetic quantities, but field singularities at corners will be correctly handled.

**场计算: 根据“ P.Lalanne，m.p. Jurek，JMO 45,1357(1998)”中描述的方法及其对交叉光栅的推广(未发表) ，计算了光栅内各处的近场电磁场。基本上，在不连续电磁量的图中不会看到吉布斯现象，但是在角落处的场奇异性将被正确处理。**

 

**Acknowledging the use of RETICOLO**: In publications and reports, acknowledgments have to be provided by referencing to J.P. Hugonin and P. Lalanne, RETICOLO software for grating analysis, Institut d'Optique, Orsay, France (2005), arXiv:2101:00901.

**承认 RETICOLO 的使用: 在出版物和报告中，承认必须参考 j.p. Hugonin 和 p. Lalanne，RETICOLO 光栅分析软件，法国 Orsay 光学研究所，arXiv: 2101:00901。**

 

In journal publications and in addition, one may fairly quote the following references:

在期刊出版物和另外，人们可以公正地引用下列参考文献:

-P. Lalanne and G.M. Morris, "Highly improved convergence of the coupled-wave method for TM polarization", J. Opt. Soc. Am. A **13**, 779-789 (1996).

拉兰内和莫里斯，“ TM 极化的耦合波方法的高度改进的收敛性”，J.Opt。Soc.译注:。13,779-789(1996).

-P. Lalanne and M.P. Jurek, "Computation of the near-field pattern with the coupled-wave method for TM polarization", J. Mod. Opt.**45**, 1357-1374 (1998), if near-field electromagnetic-field distributions are shown.

\- P.Lalanne 和 m.p. Jurek，“用 TM 极化的耦合波方法计算近场模式”，J.Mod。如果显示近场电磁场分布，则为 Opt. 45,1357-1374(1998)。

 

## The diffraction problem considered

考虑了衍射问题

In general terms, the code solves the diffraction problem by a grating defined by a stack of layers which have all identical periods in the x- directions and are invariant in the y direction see the following figure. In the following, the (x,y) plane and the z-direction will be referred to as the transverse plane and the longitudinal direction, respectively. To define the grating structure, first we have to define a top and a bottom. This is rather arbitrary since the top or the bottom can be the substrate or the cover of a real structure. It is up to the user. Once the top

一般来说，该代码通过一个光栅来解决衍射问题，这个光栅由一堆在 x 方向上具有相同周期且在 y 方向上不变的层所定义，如下图所示。接下来，(x，y)平面和 z 方向分别称为横向平面和纵向平面。为了定义光栅结构，首先我们必须定义一个顶部和一个底部。这是相当武断的，因为顶部或底部可以是一个真实结构的衬底或覆盖物。这取决于用户。一旦登顶



 and the bottom of the grating have been defined, the user can choose to illuminate the structure from the top or from the bottom. The z-axis is oriented from bottom to top.

光栅的底部已经确定，用户可以选择从顶部或从底部照明结构。Z 轴是从下到上定向的。

 

RETICOLO is written with the 𝑒𝑥𝑝(−𝑖𝜔𝑡) convention for the complex notation of the fields. So, if the materials are absorbant, one expects that all indices have a positive imaginary part. The Maxwell's equations are of the form

RETICOLO 是用 exp (- iωt)约定书写的，用于字段的复杂符号。因此，如果材料是吸收性的，人们期望所有的指数都有一个正虚部分。麦克斯韦方程组是这种形式

 

where 𝜀 = 𝑛2 is the relative permittivity, a complex number, and 𝜆 is the wavelength in a vacuum.

其中 ε = n2是相对电容率，一个复数 λ 是真空中的波长。

 

RETICOLO-1D returns the diffraction efficiencies of the transmitted and reflected orders for an incident plane wave from the top and for an incident plane wave from the bottom, both for TM and TE polarizations. The four results are obtained by the same calculation (incident TE wave from the top, incident TM wave from the top, incident TE wave from the bottom and incident TM wave from the bottom). Of course, the two incident plane waves must have identical parallel wave vector in the transverse plane [ kinc , kinc ]. This possibility which is not

RETICOLO-1D 返回了 TM 和 TE 偏振情况下从顶部入射的平面波和从底部入射的平面波的透射和反射阶的衍射效率。四个结果是通过相同的计算(从顶部入射的 TE 波，从顶部入射的 TM 波，从底部入射的 TE 波和从底部入射的 TM 波)得到的。当然，两个入射平面波在横向平面上必须有相同的平行波向量[ kinc，kinc ]。这种可能性不是

## 跑的通

```matlab
%   1  D    exemple10_1D
% 不同厚度仿真 exemple2_1D
% 不同波长仿真 exemple5_1D
clc;clear;close all;
addpath('reticolo_allege_v9');
t1 = clock;
incident_angle = 0;
wavelength_range(:,1) = 0.4:0.010:2; % 波长范围
grating_period = 1; % 光栅周期
grating_height = 1;
incident_refractive_index = 1; % 入射介质的折射率
beta0 = incident_refractive_index * sin(incident_angle * pi / 180); % 入射角的相位角
polarization = -1; % -1:TM   1:TE   
parm = res0(polarization); parm.not_io = 1; % 初始化参数
parm.sym.x = 0; % 利用对称性
fourier_series = 20; % Fourier series
%% 结构尺寸和折射率
%{ 
for ii = 1:12 textures{ii} = {[-ii * grating_period / 13, 0], [1, 1.5]}; end
% textures{12} = {[-12 * grating_period / 13, -4,0], [3.2, 1,1.5]}; 
textures{13} = 1;textures{14} = 2.5;
%}

%{ 
ii = 2;
textures{1} = {[0,10,25], [1.5,1.7, 1.9]}; 
textures{2} = {[0,10,15,25], [1.3,1.2, 1.4,1.1]}; 
textures{ii+1} = 1;
textures{ii+2} = 1.5;
%}
%{ 1
ii = 1;
textures{1} = {[0.25,0.75], [1, 2]}; 
% textures{2} = {[0,10,15,25], [1+3i,2, 1,2]}; 
textures{ii+1} = 1;
textures{ii+2} = 1;
%}

%%
%{ 1
for ix = 20
    fourier_series = ix;
    T = zeros(length(wavelength_range), 1);
    for wave_num = 1:length(wavelength_range)
        
        aa = res1(wavelength_range(wave_num), grating_period, textures, fourier_series, beta0, parm);
        profil = {[0,  (grating_height / 1), 0], [numel(textures)-1, 1:(numel(textures)-2), numel(textures)]};
        ef = res2(aa, profil);
        R(wave_num,1) = sum(ef.inc_top_reflected.efficiency);
        T(wave_num,1) = sum(ef.inc_top_transmitted.efficiency);
    end
    Transmission_M(:,ix) = T;
end

%}
%% 绘制折射率
wave_num = 1;
aa = res1(wavelength_range(wave_num), grating_period, textures, fourier_series, beta0, parm);
x = linspace(0, grating_period, 100); % 绘制的范围 两个周期 
parm.res3.cale = []; % signifie que l'on ne calcule pas le champ
profil = {[2,  grating_height, 2], [numel(textures)-1, 1:(numel(textures)-2), numel(textures)]};
[tab1, z, o] = res3(x, aa, profil, 1, parm); 

% plot_func(dimension,x,y,z,fontsize, linewidth, x_dis, y_dis, width, height,xlable, ylable, title)
plot_func(3,x,z,real(o),25, 1.5, -1000,500,500,400,'X label range (μm)','Z label (μm)','截面折射率');


%% 绘制透射谱
% plot_func(dimension,x,y,z,fontsize, linewidth, x_dis, y_dis, width, height,xlable, ylable, title)
if exist('Transmission_M') ~= 0
    plot_func(2,wavelength_range,Transmission_M,  0,25,1.5,  -500,500,500,400,'Wavelength (μm)','Transmission','透射率与阶数的关系');
end
t2 = clock; tc(t2,t1);

```





## 一维光栅结构-改之前

<img src="https://cdn.staticaly.com/gh/yangmulao/blogcdn@master/img/image-20230419103659141.png" alt="image-20230419103659141" style="zoom:80%;" />



```matlab
% 不同厚度仿真 exemple2_1D
clc;clear;close all;
addpath('reticolo_allege_v9'); addpath('shuju');addpath('script');addpath('RCWA');
t1 = clock;
incident_angle = 0;
wavelength_range(:,1) = 0.4:0.001:4; % 波长范围

grating_period = 1; % 光栅周期
incident_refractive_index = 1; % 入射介质的折射率
k_parallel = incident_refractive_index * sin(incident_angle * pi / 180); % 入射角的相位角
polarization = -1; % -1:TM   1:TE   
parm = res0(polarization); parm.not_io = 1; % 初始化参数
% parm.sym.x = 1; % 利用对称性
fourier_series_M = 20; % Fourier series
fourier_series = 20; 

% 1  MgF2     % 11 W       % 21 VO2-hot
% 2  SiO2     % 12 Ti      % 22 VO2-cool
% 3  Al2O3    % 13 Fe      % 23 VO2-hot
% 4  Si3N4    % 14 Cr      % 24 DAST-Voltage
% 5  Si3N41直 % 15 Mo*     % 25 ALON
% 6  TiO2     % 16 Au      % 26 ITO
% 7  SiN      % 17 Cu      % 27 Ag*
% 8  Ge       % 18 Al
% 9  PMMA     % 19 Ag 
% 10 SiO2     % 20 VO2-cool
nk_Martix = conj(nk_data(wavelength_range*1000));
%% 结构尺寸和折射率
struct.period = 1; 
struct.height(:,1) =  [1.00   1.00   1]; % h1 h2 ...
struct.width(:,1) =  [0.4    0.6    0.8];   % w1 w2 ...
struct.nkindex(:,1) = [19   19      19];
% FDTD
struct.unit = 1e-6; % 1e-6 μm; 1e-9 nm
struct.mesh = 0.02; % mesh 
struct.mesh_M = 0.01;
struct.wave_start = min(wavelength_range);
struct.wave_stop = max(wavelength_range);
struct.wave_step = wavelength_range(2,1)-wavelength_range(1,1);

%% 结构纹理 textures
x_bloack = 51;
for iz = 1:length(struct.height)
    textures{iz}(1) = {[-struct.width(iz,1)/2,struct.width(iz,1)/2]}; % 设置结构宽度
    struct.nk(:,iz) = nk_Martix(:,struct.nkindex(iz,1)); % 设置结构折射率
end

scale_one = grating_period / x_bloack;
for io = 1:x_bloack
    x_coordinate(io) = scale_one * (io - 1) - grating_period/2;
end
textures{3}(1) = {x_coordinate};
textures{iz+1} = 1;


for method = 1:1  % 1: RCWA 2:FDTD
switch method    
    case 1 %% 1 RCWA
        for ix = 1:length(fourier_series_M)
            fourier_series = fourier_series_M(ix);
            R = zeros(length(wavelength_range), 1); T = R; A = R; 
            textures_local = textures; aa_save = {}; profil_save = {}; textures_save = {1:length(wavelength_range)};
            parfor wave_num = 1:length(wavelength_range)                 
                textures = textures_local;
                for izz = 1:iz;textures{izz}(2) = {[1, struct.nk(wave_num,izz)]};end;
                b_ix = ones(1,length(textures{1, 3}{1, 1}));
                for ia = 1:length(textures{1, 3}{1, 1})
                    if rem(ia, 2) == 0
                        b_ix(ia) = 2;
                    end
                end
                textures{3}(2) = {b_ix};

                aa = res1(wavelength_range(wave_num), struct.period, textures, fourier_series, k_parallel, parm);
                profile = {[0,  struct.height', 0], [length(textures), 1:(numel(textures)-1), length(textures)]};
                % 计算
                ef = res2(aa, profile);
                R(wave_num,1) = sum(ef.inc_top_reflected.efficiency);
                T(wave_num,1) = sum(ef.inc_top_transmitted.efficiency);
                A(wave_num,1) = 1 - sum(ef.inc_top_reflected.efficiency) - sum(ef.inc_top_transmitted.efficiency);
                textures_save{wave_num} = textures; aa_save{wave_num} = aa; profil_save{wave_num} = profile;
            end
            RCWA.R(:,ix) = R; RCWA.T(:,ix) = T; RCWA.A(:,ix) = A;
            t2 = clock; tc(t2,t1);
            RCWA.T_matrix(:,ix) = T;
        end
        RCWA.RTA = [R T A]; RCWA.R = R; RCWA.T = T; RCWA.A = A; 

        textures = textures_save{1}; aa = aa_save{1};
        profile = profil_save{1}; profile{1}(1) = 2; profile{1}(end) = 2;
        x = linspace(-struct.period/2, struct.period/2, max(x_bloack*2, 100));
        [e, z, o] = res3(x, aa, profile, 1, parm);         
        plot_func(3,[1 3 1 1],x,z,real(o),15, 1.5, -1000,500,900,400,'X','Z','截面折射率');      
        %% 绘制透射谱
        plot_func(2,[1 3 2 0],wavelength_range,RCWA.T_matrix,0, 15,1.5,  -500,500,500,400,'Wavelength (μm)','Transmission','RCWA 透射');
        plot_func(3,[1 3 3 0],x,z,e(:,:,1).*conj(e(:,:,1)),15, 1.5, -1000,500,900,400,'X','Z','abs(E)^2');      
        
        t2 = clock; tc(t2,t1);

    %% 2 FDTD
    case 2
        for mesh_num = 1:length(struct.mesh_M)
            struct.mesh = struct.mesh_M(mesh_num); FDTD = fun_1D(struct); t2 = clock; tc(t2,t1);
        end
        plot_func(2, 0,FDTD.wave,FDTD.T,0, 25,1.5,  -500,500,500,400,'Wavelength (μm)','R/T/A','FDTD 透射');
end;end

```

