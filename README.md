# Adaptive-Wing-Loss
假设已知函数<script type="math/tex" id="MathJax-Element-1">y=f(x)</script>在<script type="math/tex" id="MathJax-Element-2">N+1</script>个点<script type="math/tex" id="MathJax-Element-3">x_1,x_2,\cdots,x_{N+1}</script>处的函数值<script type="math/tex" id="MathJax-Element-4">y_1,y_2,\cdots,y_{N+1}</script>，但函数的表达式<script type="math/tex" id="MathJax-Element-5">f(x)</script>未知，那么可以通过插值函数<script type="math/tex" id="MathJax-Element-6">p(x)</script>来逼近未知函数<script type="math/tex" id="MathJax-Element-7">f(x)</script>，并且<script type="math/tex" id="MathJax-Element-8">p(x)</script>必须满足
<script type="math/tex; mode=display" id="MathJax-Element-9">p(x_k)=y_k, k=1,2,\cdots,N+1. \tag 1</script>

常见的插值函数的形式有多项式函数、样条函数。

    多项式函数：令<script type="math/tex" id="MathJax-Element-10">p(x)</script>为<script type="math/tex" id="MathJax-Element-11">N</script>次多项式函数，于是<script type="math/tex" id="MathJax-Element-12">p(x)</script>有<script type="math/tex" id="MathJax-Element-13">N+1</script>个参数，而由公式(1)可知这<script type="math/tex" id="MathJax-Element-14">N+1</script>个参数满足<script type="math/tex" id="MathJax-Element-15">N+1</script>个约束条件，所以可以求出<script type="math/tex" id="MathJax-Element-16">p(x)</script>的表达式。

    样条函数：我们知道<script type="math/tex" id="MathJax-Element-17">N</script>阶多项式函数必然有<script type="math/tex" id="MathJax-Element-18">N-1</script>个极值点，所以得到的插值函数摆动会比较大，这有点像机器学习中的过拟合现象，可以用样条函数来避免这个问题。这里的样条函数其实就是分段函数，表示在相邻点<script type="math/tex" id="MathJax-Element-19">x_k</script>和<script type="math/tex" id="MathJax-Element-20">x_{k+1}</script>之间用低阶多项式函数<script type="math/tex" id="MathJax-Element-21">S_k(x)</script>进行插值。分段线性插值和三次样条插值都属于样条插值。

TPS

本文介绍的TPS针对的是插值问题的一种特殊情况，并且TSP插值函数的形式也比较新颖。
考虑这样一个插值问题：自变量<script type="math/tex" id="MathJax-Element-22">\bf x</script>是2维空间中的一点，函数值<script type="math/tex" id="MathJax-Element-23">\bf y</script>也是2维空间中的一点，并且都在笛卡尔坐标系下表示。给定<script type="math/tex" id="MathJax-Element-24">N</script>个自变量<script type="math/tex" id="MathJax-Element-25">{\bf x}_k</script>和对应的函数值<script type="math/tex" id="MathJax-Element-26">{\bf y}_k</script>，求插值函数
<script type="math/tex; mode=display" id="MathJax-Element-27">\Phi(\bf x)=\left[
Φ1(x)Φ2(x)
\right]，</script>

使得
<script type="math/tex; mode=display" id="MathJax-Element-28">{\bf y}_k= \Phi({\bf x}_k). \tag 2</script>

我们可以认为是求两个插值函数<script type="math/tex" id="MathJax-Element-29">\Phi_1(\bf x)</script>和<script type="math/tex" id="MathJax-Element-30">\Phi_2(\bf x)</script>。

TPS插值函数形式如下：
<script type="math/tex; mode=display" id="MathJax-Element-31">\Phi_1(\bf x)=c + \bf a^T \bf x + {\bf w}^T {\bf s}(\bf x) \tag 3</script>

其中<script type="math/tex" id="MathJax-Element-32">c</script>是标量，向量<script type="math/tex" id="MathJax-Element-33">\bf a \in \mathbb R^{2 \times 1}</script>，向量<script type="math/tex" id="MathJax-Element-34">\bf w\in \mathbb R^{N\times 1}</script>，函数向量
<script type="math/tex; mode=display" id="MathJax-Element-35">\bf s(\bf x)=(\sigma(\bf x -\bf x_1), \sigma(\bf x -\bf x_1), \cdots, \sigma(\bf x -\bf x_N))^T</script>

<script type="math/tex; mode=display" id="MathJax-Element-36">\sigma(\bf x)=||\bf x||^2_2\log||\bf x||_2.</script>

<script type="math/tex" id="MathJax-Element-37">\Phi_2(\bf x)</script>和<script type="math/tex" id="MathJax-Element-38">\Phi_1(\bf x)</script>有一样的形式。看到这里可能会产生疑问？插值函数的形式千千万，怎么就选择公式(3)这种形式呢？我们可以把一个插值函数想象成弯曲一个薄钢板，使得它穿过给定点，这样会需要一个弯曲能量：
<script type="math/tex; mode=display" id="MathJax-Element-39">J(\Phi) = \sum_{j=1}^2\iint_{\mathbb R^2}\left(\frac{\partial^2 \Phi_j}{\partial x^2}\right)^2 + 2\left( \frac{\partial^2 \Phi_j}{\partial x \partial y}\right)^2 + \left( \frac{\partial^2 \Phi_j}{\partial y^2}\right)^2dxdy</script>

那么可以证明公式(3)是使得弯曲能量最小的插值函数。参考文献[3]中给了证明过程。

TSP插值函数<script type="math/tex" id="MathJax-Element-40">\Phi_1</script>有<script type="math/tex" id="MathJax-Element-41">N+3</script>个参数，而条件(2)只给出了<script type="math/tex" id="MathJax-Element-42">N</script>个约束，我们再添加三个约束：
<script type="math/tex; mode=display" id="MathJax-Element-43">
∑k=1Nwk=∑k=1Nxxkwk=∑k=1Nxykwk=000
\tag 4</script>

<script type="math/tex" id="MathJax-Element-44">{\bf x}_k^x</script>和<script type="math/tex" id="MathJax-Element-45">{\bf x}_k^y</script>分别表示点<script type="math/tex" id="MathJax-Element-46">\bf x</script>的<script type="math/tex" id="MathJax-Element-47">x</script>坐标值和<script type="math/tex" id="MathJax-Element-48">y</script>坐标值。于是(2)和(4)可以写成
<script type="math/tex; mode=display" id="MathJax-Element-49">\left[
S1TNXT1N00X00
\right] \left[
wca
\right] = \left[
Yx00
\right] \tag 5</script>
其中， <script type="math/tex" id="MathJax-Element-50">(S)_{ij}=\sigma({\bf x}_i-\bf x_j)</script>， <script type="math/tex" id="MathJax-Element-51">1_N</script>表示值全为1的 <script type="math/tex" id="MathJax-Element-52">N</script>维列向量，
<script type="math/tex; mode=display" id="MathJax-Element-53">X = \left[
xx1xx2⋯xxNxy1xy2⋯xyN
\right] </script>

<script type="math/tex; mode=display" id="MathJax-Element-54">Y^x = \left[
yx1yx2⋯yxN
\right] </script>

我们可以令
<script type="math/tex; mode=display" id="MathJax-Element-55">\Gamma =\left[
S1TNXT1N00X00
\right]</script>

那么可知当<script type="math/tex" id="MathJax-Element-56">S</script>是非奇异矩阵时，<script type="math/tex" id="MathJax-Element-57">\Gamma</script>也是非奇异矩阵，于是参数为：
<script type="math/tex; mode=display" id="MathJax-Element-58">\left[
wca
\right]= \Gamma^{-1}\left[
Yx00
\right] \tag 6</script>

可以把<script type="math/tex" id="MathJax-Element-59">\Phi_1</script>和<script type="math/tex" id="MathJax-Element-60">\Phi_2</script>的参数通过一个矩阵运算计算出来：
<script type="math/tex; mode=display" id="MathJax-Element-61">\left[
wxcxaxwycyay
\right]= \Gamma^{-1}\left[
Yx00Yy00
\right] \tag 7</script>

我们把<script type="math/tex" id="MathJax-Element-62">\Gamma^{-1}</script>写成下面的形式：
<script type="math/tex; mode=display" id="MathJax-Element-63">\Gamma^{-1}=\left[
Γ11Γ21Γ12Γ22
\right]</script>

称矩阵<script type="math/tex" id="MathJax-Element-64">\Gamma{11}</script>为弯曲能量矩阵，其秩为<script type="math/tex" id="MathJax-Element-65">N-3</script>
