---
title: chati-latex（数学公式显示测试）
category: Test
tags: test
updatedAt: 2024-02-08T13:49:22.939Z
date: 2024-02-08T13:47:49.251Z
---


## Markdown 公式指导手册


<!-- more -->


### 一、公式使用参考



#### 1．如何插入公式



LaTeX 的数学公式有两种：行中公式和独立公式。行中公式放在文中与其它文字混编，独立公式单独成行。



行内公式可用如下方法表示：



```

$$数学公式$$

```



独立公式可以用如下方法表示：



```

$$

数学公式

$$

```



- 例子：

```

$$ J_\alpha(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha} \text {，独立公式示例} $$

```

- 显示：$$ J_\alpha(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m! \Gamma (m + \alpha + 1)} {\left({ \frac{x}{2} }\right)}^{2m + \alpha} \text {，独立公式示例} $$





#### 2．如何输入上下标



`^` 表示上标, `_` 表示下标。如果上下标的内容多于一个字符，需要用 `{}` 将这些内容括成一个整体。上下标可以嵌套，也可以同时使用。



- 例子：

```

$$ x^{y^z}=(1+{\rm e}^x)^{-2xy^w} $$

```

- 显示：$$ x^{y^z}=(1+{\rm e}^x)^{-2xy^w} $$



另外，如果要在左右两边都有上下标，可以使用 `\sideset` 命令；也可以简单地在符号前面多打一个上下标，此时会以行内公式渲染。



- 例子：

```

$$ \sideset{^1_2}{^3_4}\bigotimes \quad or \quad {^1_2}\bigotimes {^3_4} $$

```

- 显示：$$\sideset{^1_2}{^3_4}\bigotimes \quad or \quad {^1_2}\bigotimes {^3_4} $$



#### 3．如何输入括号和分隔符



`()`、`[]` 和 `|` 表示符号本身，使用 `\{\}` 来表示 `{}` 。当要显示大号的括号或分隔符时，要用 `\left` 和 `\right` 命令。



一些特殊的括号：



|  输入   |   显示    |  输入   |   显示    |

| :-----: | :-------: | :-----: | :-------: |

| \langle | $$\langle$$ | \rangle | $$\rangle$$ |

| \lceil  | $$\lceil$$  | \rceil  | $$\rceil$$  |

| \lfloor | $$\lfloor$$ | \rfloor | $$\rfloor$$ |

| \lbrace | $$\lbrace$$ | \rbrace | $$\rbrace$$ |

| \lvert  | $$\lvert$$  | \rvert  | $$\rvert$$  |

| \lVert  | $$\lVert$$  | \rVert  | $$\rVert$$  |



> 有时，我们需要在行内使用两个竖杠表示向量间的某种空间距离，可以这样写

> `\lVert \boldsymbol{X}_i - \boldsymbol{S}_j \rVert^2`

>  效果： 

>  $$\lVert \boldsymbol{X}_i - \boldsymbol{S}_j \rVert^2$$



- 例子：

```

$$ f(x,y,z) = 3y^2z \left( 3+\frac{7x+5}{1+y^2} \right) $$

```

- 显示：$$ f(x,y,z) = 3y^2z \left( 3+\frac{7x+5}{1+y^2} \right) $$



有时要用 `\left.` 或 `\right.` 进行匹配而不显示本身。



- 例子：

```

$$ \left. \frac{{\rm d}u}{{\rm d}x} \right| _{x=0} $$

```

- 显示：$$ \left. \frac{{\rm d}u}{{\rm d}x} \right| _{x=0} $$



#### 4．如何输入分数



通常使用 `\frac {分子} {分母}` 来生成一个分数，分数可多层嵌套。如果分式较为复杂，亦可使用 `分子 \over 分母` 此时分数仅有一层。



- 例子：

```

$$ \frac{a-1}{b-1} \quad or \quad {a+1 \over b+1} $$

```

- 显示：$$ \frac{a-1}{b-1} \quad or \quad {a+1 \over b+1} $$



当分式 **仅有两个字符时** 可直接输入 `\frac ab` 来快速生成一个 $$\large\frac ab$$ ：



```

$$\large\frac ab$$ 

```



- 例子：

```

$$ \frac 12,\frac 1a,\frac a2 \quad \mid \quad \text{2 letters only:} \quad \frac 12a \,, k\frac q{r^2} $$

```

- 显示：



$$ \frac 12,\frac 1a,\frac a2 \quad \mid \quad \text{2 letters only:} \quad \frac 12a \,, k\frac q{r^2} $$



#### 5．如何输入开方



使用 `\sqrt [根指数，省略时为2] {被开方数}` 命令输入开方。



- 例子：

```

$$ \sqrt{2} \quad or \quad \sqrt[n]{3} $$

```

- 显示：$$ \sqrt{2} \quad or \quad \sqrt[n]{3} $$



#### 6．如何输入省略号



数学公式中常见的省略号有两种，`\ldots` 表示与 **文本底线** 对齐的省略号，`\cdots` 表示与 **文本中线** 对齐的省略号。



- 例子：

```

$$ f(x_1,x_2,\underbrace{\ldots}_{\rm ldots} ,x_n) = x_1^2 + x_2^2 + \underbrace{\cdots}_{\rm cdots} + x_n^2 $$

```

- 显示：$$ f(x_1,x_2,\underbrace{\ldots}_{\rm ldots} ,x_n) = x_1^2 + x_2^2 + \underbrace{\cdots}_{\rm cdots} + x_n^2 $$



#### 7．如何输入向量



使用 `\vec{向量}` 来自动产生一个向量。也可以使用 `\overrightarrow` 等命令自定义字母上方的符号。



- 例子：

```

$$ \vec{a} \cdot \vec{b}=0 $$

```

- 显示：$$ \vec{a} \cdot \vec{b}=0 $$



- 例子：

```

$$ xy \text{ with arrows:} \quad \overleftarrow{xy} \; \mid \; \overleftrightarrow{xy} \; \mid \; \overrightarrow{xy} $$

```

- 显示：$$ xy \text{ with arrows:} \quad \overleftarrow{xy} \; \mid \; \overleftrightarrow{xy} \; \mid \; \overrightarrow{xy} $$



#### 8．如何输入积分



使用 `\int_积分下限^积分上限 {被积表达式}` 来输入一个积分。



例子：

```

$$ \int_0^1 {x^2} \,{\rm d}x $$

```

显示：$$ \int_0^1 {x^2} \,{\rm d}x $$



本例中 `\,` 和 `{\rm d}` 部分可省略，但加入能使式子更美观。



#### 9．如何输入极限运算



使用 `\lim_{变量 \to 表达式} 表达式` 来输入一个极限。如有需求，可以更改 `\to` 符号至任意符号。



例子：

```

$$ \lim_{n \to \infty} \frac{1}{n(n+1)} \quad and \quad \lim_{x\leftarrow{示例}} \frac{1}{n(n+1)} $$

```

显示：$$ \lim_{n \to \infty} \frac{1}{n(n+1)} \quad and \quad \lim_{x\leftarrow{示例}} \frac{1}{n(n+1)} $$



#### 10．如何输入累加、累乘运算



使用 `\sum_{下标表达式}^{上标表达式} {累加表达式}` 来输入一个累加。与之类似，使用 `\prod` `\bigcup` `\bigcap` 来分别输入累乘、并集和交集。

此类符号在行内显示时上下标表达式将会移至右上角和右下角，如 $$\sum_{i=1}^n \frac{1}{i^2}$$:



```

$$\sum_{i=1}^n \frac{1}{i^2}$$

```



- 例子：

```

$$ \sum_{i=1}^n \frac{1}{i^2} \quad and \quad \prod_{i=1}^n \frac{1}{i^2} \quad and \quad \bigcup_{i=1}^{2} \Bbb{R} $$

```

- 显示：$$ \sum_{i=1}^n \frac{1}{i^2} \quad and \quad \prod_{i=1}^n \frac{1}{i^2} \quad and \quad \bigcup_{i=1}^{2} \Bbb{R} $$



#### 11．如何输入希腊字母



输入 `\小写希腊字母英文全称` 和 `\首字母大写希腊字母英文全称` 来分别输入小写和大写希腊字母。

**对于大写希腊字母与现有字母相同的，直接输入大写字母即可。**



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :------: | :--------: | :-----: | :-------: | :------: | :--------: | :------: | :--------: |

| \alpha | $$\alpha$$ | A | $$A$$ | \beta | $$\beta$$ | B | $$B$$ |

| \gamma | $$\gamma$$ | \Gamma | $$\Gamma$$ | \delta | $$\delta$$ | \Delta | $$\Delta$$ |

| \epsilon | $$\epsilon$$ | E | $$E$$ | \zeta | $$\zeta$$ | Z | $$Z$$ |

| \eta | $$\eta$$ | H | $$H$$ | \theta | $$\theta$$ | \Theta | $$\Theta$$ |

| \iota | $$\iota$$ | I | $$I$$ | \kappa | $$\kappa$$ | K | $$K$$ |

| \lambda | $$\lambda$$ | \Lambda | $$\Lambda$$ | \mu | $$\mu$$ | M | $$M$$ |

| \nu | $$\nu$$ | N | $$N$$ | \xi | $$\xi$$ | \Xi | $$\Xi$$ |

| o | $$o$$ | O | $$O$$ | \pi | $$\pi$$ | \Pi | $$\Pi$$ |

| \rho | $$\rho$$ | P | $$P$$ | \sigma | $$\sigma$$ | \Sigma | $$\Sigma$$ |

| \tau | $$\tau$$ | T | $$T$$ | \upsilon | $$\upsilon$$ | \Upsilon | $$\Upsilon$$ |

| \phi | $$\phi$$ | \Phi | $$\Phi$$ | \chi | $$\chi$$ | X | $$X$$ |

| \psi | $$\psi$$ | \Psi | $$\Psi$$ | \omega | $$\omega$$ | \Omega | $$\Omega$$ |



**部分字母有变量专用形式，以 `\var-` 开头。**



| 小写形式 | 大写形式 |  变量形式  |  显示  |

| :------: | :------: | :---------: | :---------------------------: |

| \epsilon |  E  | \varepsilon | $$\epsilon \mid E \mid \varepsilon$$  |

|  \theta  |  \Theta  |  \vartheta  | $$\theta \mid \Theta \mid \vartheta$$ |

|  \rho  |  P  |  \varrho  |  $$\rho \mid P \mid \varrho$$  |

|  \sigma  |  \Sigma  |  \varsigma  | $$\sigma \mid \Sigma \mid \varsigma$$ |

|  \phi  |  \Phi  |  \varphi  |  $$\phi \mid \Phi \mid \varphi$$  |



#### 12．如何输入其它特殊字符



> 完整的 $\LaTeX$ 可用符号列表可以在 [这份文档](https://mirror.its.dal.ca/ctan/info/symbols/comprehensive/symbols-a4.pdf) 中查阅（极长，共 348 页），大部分常用符号可以参阅 [这份精简版文档](https://pic.plover.com/MISC/symbols.pdf) 查询。



> 若需要显示更大或更小的字符，在符号前插入 `\large` 或 `\small` 命令。



> [若找不到需要的符号，推荐使用 $$\large\rm{Detexify}$$ 来画出想要的符号](http://detexify.kirelabs.org/classify.html)

> ![detexify_t](https://cdn.ericp.cn/img/202009/b0fe4b234a3fc.png)

>

> 



##### (1)．关系运算符



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :------: | :--------: | :--------: | :----------: | :-------: | :---------: | :--------: | :----------: |

| \pm | $$\pm$$ | \times | $$\times$$ | \div | $$\div$$ | \mid | $$\mid$$ |

| \nmid | $$\nmid$$ | \cdot | $$\cdot$$ | \circ | $$\circ$$ | \ast | $$\ast$$ |

| \bigodot | $$\bigodot$$ | \bigotimes | $$\bigotimes$$ | \bigoplus | $$\bigoplus$$ | \leq | $$\leq$$ |

| \geq | $$\geq$$ | \neq | $$\neq$$ | \approx | $$\approx$$ | \equiv | $$\equiv$$ |

| \sum | $$\sum$$ | \prod | $$\prod$$ | \coprod | $$\coprod$$ | \backslash | $$\backslash$$ |



##### (2)．集合运算符



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :-------: | :---------: | :-----: | :-------: | :---------: | :-----------: |

| \emptyset | $$\emptyset$$ | \in | $$\in$$ | \notin | $$\notin$$ |

| \subset | $$\subset$$ | \supset | $$\supset$$ | \subseteq | $$\subseteq$$ |

| \supseteq | $$\supseteq$$ | \cap | $$\cap$$ | \cup | $$\cup$$ |

| \vee | $$\vee$$ | \wedge | $$\wedge$$ | \uplus | $$\uplus$$ |

| \top | $$\top$$ | \bot | $$\bot$$ | \complement | $$\complement$$ |



##### (3)．对数运算符



| 输入 |  显示  | 输入 | 显示  | 输入 | 显示  |

| :--: | :----: | :--: | :---: | :--: | :---: |

| \log | $$\log$$ | \lg  | $$\lg$$ | \ln  | $$\ln$$ |



##### (4)．三角运算符



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :------: | :--------: | :---: | :-----: | :------: | :--------: |

| \backsim | $$\backsim$$ | \cong | $$\cong$$ | \angle A | $$\angle A$$ |

| \sin | $$\sin$$ | \cos | $$\cos$$ | \tan | $$\tan$$ |

| \csc | $$\csc$$ | \sec | $$\sec$$ | \cot | $$\cot$$ |



##### (5)．微积分运算符



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :------: | :--------: | :----: | :------: | :----: | :------: |

| \int | $$\int$$ | \iint | $$\iint$$ | \iiint | $$\iiint$$ |

| \partial | $$\partial$$ | \oint | $$\oint$$ | \prime | $$\prime$$ |

| \lim | $$\lim$$ | \infty | $$\infty$$ | \nabla | $$\nabla$$ |



##### (6)．逻辑运算符



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :------: | :--------: | :--------: | :----------: | :---------: | :-----------: |

| \because | $$\because$$ | \therefore | $$\therefore$$ | \neg | $$\neg$$ |

| \forall | $$\forall$$ | \exists | $$\exists$$ | \not\subset | $$\not\subset$$ |

| \not< | $$\not<$$ | \not> | $$\not>$$ | \not= | $$\not=$$ |



##### (7)．戴帽符号



| 输入 | 显示 | 输入 | 显示 | 输入 | 显示 |

| :--------: | :----------: | :-------------: | :---------------: | :-------: | :---------: |

| \hat{xy} | $$\hat{xy}$$ | \widehat{xyz} | $$\widehat{xyz}$$ | \bar{y} | $$\bar{y}$$ |

| \tilde{xy} | $$\tilde{xy}$$ | \widetilde{xyz} | $$\widetilde{xyz}$$ | \acute{y} | $$\acute{y}$$ |

| \breve{y} | $$\breve{y}$$ | \check{y} | $$\check{y}$$ | \grave{y} | $$\grave{y}$$ |

| \dot{x} | $$\dot{x}$$ | \ddot{x} | $$\ddot{x}$$ | \dddot{x} | $$\dddot{x}$$ |







##### (8)．连线符号



其它可用的文字修饰符可参见官方文档 ["Additional decorations"](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference#answer-13081)。



|                             输入                             |                       显示                       |

| :----------------------------------------------------------: | :----------------------------------------------: |

| \fbox{a+b+c+d} <span style="display: block">**高级框选需[声明 `enclose` 标签](#5添加删除线)**</span> |                  $$\fbox{a+b+c+d} $$                 |

|                   \overleftarrow{a+b+c+d}                    |             $$\overleftarrow{a+b+c+d} $$             |

|                   \overrightarrow{a+b+c+d}                   |             $$\overrightarrow{a+b+c+d} $$            |

|                 \overleftrightarrow{a+b+c+d}                 |           $$\overleftrightarrow{a+b+c+d} $$          |

|                   \underleftarrow{a+b+c+d}                   |             $$\underleftarrow{a+b+c+d} $$            |

|                  \underrightarrow{a+b+c+d}                   |            $$\underrightarrow{a+b+c+d} $$            |

|                \underleftrightarrow{a+b+c+d}                 |          $$\underleftrightarrow{a+b+c+d} $$          |

|                      \overline{a+b+c+d}                      |                $$\overline{a+b+c+d} $$               |

|                     \underline{a+b+c+d}                      |               $$\underline{a+b+c+d} $$               |

|                 \overbrace{a+b+c+d}^{Sample}                 |           $$\overbrace{a+b+c+d}^{Sample} $$          |

|                \underbrace{a+b+c+d}_{Sample}                 |          $$\underbrace{a+b+c+d}_{Sample} $$          |

|         \overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0}         |   $$\overbrace{a+\underbrace{b+c}_{1.0}+d}^{2.0} $$  |

|        \underbrace{a\cdot a\cdots a}_{b\text{ times}}        |  $$\underbrace{a\cdot a\cdots a}_{b\text{ times}} $$ |



##### (9)．箭头符号



- 推荐使用符号：



|   输入   |    显示    |  输入   |   显示    |           输入           |            显示            |

| :------: | :--------: | :-----: | :-------: | :----------------------: | :------------------------: |

|   \to    |   $$\to$$    | \mapsto | $$\mapsto$$ | \underrightarrow{1℃/min} | $$\underrightarrow{1℃/min}$$ |

| \implies | $$\implies$$ |  \iff   |  $$\iff$$   |        \impliedby        |        $$\impliedby$$        |





- 其它可用符号：



|        输入         |         显示          |        输入         |         显示          |

| :-----------------: | :-------------------: | :-----------------: | :-------------------: |

|      \uparrow       |      $$\uparrow$$       |      \Uparrow       |      $$\Uparrow$$       |

|     \downarrow      |     $$\downarrow$$      |     \Downarrow      |     $$\Downarrow$$      |

|     \leftarrow      |     $$\leftarrow$$      |     \Leftarrow      |     $$\Leftarrow$$      |

|     \rightarrow     |     $$\rightarrow$$     |     \Rightarrow     |     $$\Rightarrow$$     |

|   \leftrightarrow   |   $$\leftrightarrow$$   |   \Leftrightarrow   |   $$\Leftrightarrow$$   |

|   \longleftarrow    |   $$\longleftarrow$$    |   \Longleftarrow    |   $$\Longleftarrow$$    |

|   \longrightarrow   |   $$\longrightarrow$$   |   \Longrightarrow   |   $$\Longrightarrow$$   |

| \longleftrightarrow | $$\longleftrightarrow$$ | \Longleftrightarrow | $$\Longleftrightarrow$$ |



#### 13．如何进行字体转换



若要对公式的某一部分字符进行字体转换，可以用 `{\字体 {需转换的部分字符}}` 命令，其中 `\字体` 部分可以参照下表选择合适的字体。一般情况下，公式默认为斜体字 $italic$ 。



示例中 **全部大写** 的字体仅大写可用。



| 输入  | 全字母可用 |      显示       |     输入     |        仅大写可用        |        显示        |

| :---: | :--------: | :-------------: | :----------: | :----------------------: | :----------------: |

|  \rm  |   罗马体   |  $$\rm{Sample}$$  | **\mathcal** |  **花体（数学符号等）**  | $$\mathcal{SAMPLE}$$ |

|  \it  |    斜体    |  $$\it{Sample}$$  | **\mathbb**  | **黑板粗体（定义域等）** | $$\mathbb{SAMPLE}$$  |

|  \bf  |    粗体    |  $$\bf{Sample}$$  |              |                          |                      |

|  \sf  |   等线体   |  $$\sf{Sample}$$  |              |                          |                      |

|  \tt  |  打字机体  |  $$\tt{Sample}$$  |              |                          |                    |

| \frak | 旧德式字体 | $$\frak{Sample}$$ |              |                          |                    |



> `\boldsymbol{\alpha}` 用来表示向量或者矩阵的加粗斜体，如向量 $$\boldsymbol{\vec\alpha}$$ :

>

> `$$\boldsymbol{\vec\alpha}$$`



#### 14．大括号和行标的使用



如果你需要将大括号里面显示的分隔符也变大，可以使用 `\middle` 命令，此处分别使用单竖线 `|` 和双竖线 `\\|` 。



- 例子：

```

$$

\left\langle  

    q \; \middle|

        \frac{\frac xy}{\frac uv}

    \middle\| p 

\right\rangle

$$

```

- 显示：

$$

\left\langle  

    q \; \middle|

        \frac{\frac xy}{\frac uv}

    \middle\| p 

\right\rangle

$$



#### 15．其它命令



##### (1)．添加注释文字 \text



在 `\text {文字}` 中仍可以使用 `$$公式$$` 插入其它公式。



- 例子：

```

$$ f(n)= \begin{cases} n/2, & \text {if $n$ is even} \\ 3n+1, & \text{if $n$ is odd} \end{cases} $$

```

- 显示：

$$ f(n)= \begin{cases} n/2, & \text {if $n$ is even} \\ 3n+1, & \text{if $n$ is odd} \end{cases} $$



##### (2)．在字符间加入空格



有四种宽度的空格可以使用： `\,`、`\;`、`\quad` 和 `\qquad`，灵活使用 `\text{n个空格}` 也可以在任意位置实现空格。

同时存在一种负空格 `\!` 用来减小字符间距，一般在物理单位中使用。

**反复使用 `\!` 命令能够实现不同元素的叠加渲染，如    $$\wedge\!\!\!\!\!\!\!\!\;\bigcirc$$      和     $$ \}\!\!\!\!\!\div $$     **，公式：



```

$$\wedge\!\!\!\!\!\!\!\!\;\bigcirc$$



$$ \}\!\!\!\!\!\div $$

```



一些常见的公式单位可表达如下：



- 例子：

```

$$ \mu_0=4\pi\times10^{-7} \ \left.\mathrm{\mathrm{T}\!\cdot\!\mathrm{m}}\middle/\mathrm{A}\right. $$

$$ 180^\circ=\pi \ \mathrm{rad} $$

$$ \mathrm{N_A} = 6.022\times10^{23} \ \mathrm{mol}^{-1} $$

```

- 显示：



$$ \mu_0=4\pi\times10^{-7} \ \left.\mathrm{\mathrm{T}\!\cdot\!\mathrm{m}}\middle/\mathrm{A}\right. $$ $$ 180^\circ=\pi \ \mathrm{rad} $$ $$ \mathrm{N_A} = 6.022\times10^{23} \ \mathrm{mol}^{-1} $$



### 二、矩阵使用参考



#### 1．如何输入无框矩阵



在开头使用 `\begin{matrix}`，在结尾使用 `\end{matrix}`，在中间插入矩阵元素，每个元素之间插入 `&` ，并在每行结尾处使用 `\\` 。

使用矩阵时必须声明 `$` 或 `$$` 符号。



- 例子：

```

$$

\begin{matrix}

    1 & x & x^2 \\

    1 & y & y^2 \\

    1 & z & z^2 \\

\end{matrix}

$$

```

- 显示：

$$

\begin{matrix}

    1 & x & x^2 \\

    1 & y & y^2 \\

    1 & z & z^2 \\

\end{matrix}

$$



#### 2．如何输入边框矩阵



在开头将 `matrix` 替换为 `pmatrix` `bmatrix` `Bmatrix` `vmatrix` `Vmatrix` 。



- 例子：



```

$$ \begin{matrix} 1 & 2 \\ 3 & 4 \\ \end{matrix} $$

$$ \begin{pmatrix} 1 & 2 \\ 3 & 4 \\ \end{pmatrix} $$

$$ \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ \end{bmatrix} $$

$$ \begin{Bmatrix} 1 & 2 \\ 3 & 4 \\ \end{Bmatrix} $$

$$ \begin{vmatrix} 1 & 2 \\ 3 & 4 \\ \end{vmatrix} $$

$$ \begin{Vmatrix} 1 & 2 \\ 3 & 4 \\ \end{Vmatrix} $$

```



- 显示：



|                      matrix                       |                       pmatrix                       |                       bmatrix                       |                       Bmatrix                       |                       vmatrix                       |                       Vmatrix                       |

| :-----------------------------------------------: | :-------------------------------------------------: | :-------------------------------------------------: | :-------------------------------------------------: | :-------------------------------------------------: | :-------------------------------------------------: |

| $$ \begin{matrix} 1 & 2 \\ 3 & 4 \\ \end{matrix} $$ | $$ \begin{pmatrix} 1 & 2 \\ 3 & 4 \\ \end{pmatrix} $$ | $$ \begin{bmatrix} 1 & 2 \\ 3 & 4 \\ \end{bmatrix} $$ | $$ \begin{Bmatrix} 1 & 2 \\ 3 & 4 \\ \end{Bmatrix} $$ | $$ \begin{vmatrix} 1 & 2 \\ 3 & 4 \\ \end{vmatrix} $$ | $$ \begin{Vmatrix} 1 & 2 \\ 3 & 4 \\ \end{Vmatrix} $$ |



#### 3．如何输入带省略符号的矩阵



使用 `\cdots` , `\ddots` , `\vdots` 来输入省略符号：



> $$\cdots$$



> $$\ddots$$



> $$\vdots$$



- 例子：

```

$$

\begin{pmatrix}

    1 & a_1 & a_1^2 & \cdots & a_1^n \\

    1 & a_2 & a_2^2 & \cdots & a_2^n \\

    \vdots & \vdots & \vdots & \ddots & \vdots \\

    1 & a_m & a_m^2 & \cdots & a_m^n \\

\end{pmatrix}

$$

```

- 显示：

$$

\begin{pmatrix}

    1 & a_1 & a_1^2 & \cdots & a_1^n \\

    1 & a_2 & a_2^2 & \cdots & a_2^n \\

    \vdots & \vdots & \vdots & \ddots & \vdots \\

    1 & a_m & a_m^2 & \cdots & a_m^n \\

\end{pmatrix}

$$



#### 4．如何输入带分割符号的矩阵



- 例子：

```

$$

\left[

    \begin{array}{cc|c}

        1 & 2 & 3 \\

        4 & 5 & 6 \\

    \end{array}

\right]

$$

```

- 显示：

$$

\left[

    \begin{array}{cc|c}

        1 & 2 & 3 \\

        4 & 5 & 6 \\

    \end{array}

\right]

$$



其中 `cc|c` 代表在一个三列矩阵中的第二和第三列之间插入分割线。



#### 5．如何输入行中矩阵



若想在一行内显示矩阵，

使用`\bigl(\begin{smallmatrix} ... \end{smallmatrix}\bigr)`。



- 例子：

```

这是一个行中矩阵的示例 $$\bigl(\begin{smallmatrix} a & b \\ c & d \end{smallmatrix}\bigr)$$ 。

```



- 显示：这是一个行中矩阵的示例 $$\bigl(\begin{smallmatrix} a & b \\ c & d \end{smallmatrix}\bigr)$$ 。







### 三、条件表达式使用参考



#### 1．如何输入一个条件表达式



使用 `\begin{cases}…\end{cases}` 来创造一组条件表达式，在每一行条件中插入 `&` 来指定需要对齐的内容，并在每一行结尾处使用 `\\`。



- 例子：



```

$$

    f(n) =

        \begin{cases}

            n/2,  & \text{if $n$ is even} \\

            3n+1, & \text{if $n$ is odd} \\

        \end{cases}

$$

```

- 显示：

$$

    f(n) =

        \begin{cases}

            n/2,  & \text{if $n$ is even} \\

            3n+1, & \text{if $n$ is odd} \\

        \end{cases}

$$



> 用 markdown+math 编辑时 `\text` 内需用 `\(equation\)`



#### 2．如何输入一个左侧对齐的条件表达式



若想让文字在**左侧对齐显示**，则有如下方式：



- 例子：





```

$$

    \left.

        \begin{array}{l}

            \text{if $n$ is even:} & n/2 \\

            \text{if $n$ is odd:} & 3n+1 \\

        \end{array}

    \right\}

    =f(n)

$$

```



- 显示：



$$

    \left.

        \begin{array}{l}

            \text{if $n$ is even:} & n/2 \\

            \text{if $n$ is odd:} & 3n+1 \\

        \end{array}

    \right\}

    =f(n)

$$



#### 3．如何使条件表达式适配行高



在一些情况下，条件表达式中某些行的行高为非标准高度，此时使用 `\\[2ex]` 语句代替该行末尾的 `\\` 来让编辑器适配。



- 例子：



不适配[2ex]：



```

$$

f(n) = 

    \begin{cases}

        \frac{n}{2}, & \text{if $n$ is even} \\

        3n+1,        & \text{if $n$ is odd} \\

    \end{cases}

$$

```



适配[2ex]：



```

$$

f(n) = 

    \begin{cases}

        \frac{n}{2}, & \text{if $n$ is even} \\[2ex]

        3n+1,        & \text{if $n$ is odd} \\

    \end{cases}

$$

```



- 显示：



不适配[2ex]：



$$

  f(n) = 

  \begin{cases}

        \frac{n}{2}, & \text{if $n$ is even} \\

      3n+1, & \text{if $n$ is odd} \\

    \end{cases}

$$



适配[2ex]：



$$

f(n) = 

  \begin{cases}

        \frac{n}{2}, & \text{if $n$ is even} \\[2ex]

      3n+1, & \text{if $n$ is odd} \\

    \end{cases}

$$



**一个 `[ex]` 指一个 "X-Height"，即 x 字母高度。可以根据情况指定多个 `[ex]`，如 `[3ex]`、`[4ex]` 等。**

其实可以在任意换行处使用 `\\[2ex]` 语句，只要你觉得合适。



### 四、数组与表格使用参考



#### 1．如何输入一个数组或表格



通常，一个格式化后的表格比单纯的文字或排版后的文字更具有可读性。

数组和表格均以 `\begin{array}` 开头，并在其后定义列数及每一列的文本对齐属性，`c` `l` `r` 分别代表居中、左对齐及右对齐。若需要插入垂直分割线，在定义式中插入 `|` ，若要插入水平分割线，在下一行输入前插入 `\hline` 。

与矩阵相似，每行元素间均须要插入 `&` ，每行元素以 `\\` 结尾，最后以 `\ end{array}` 结束数组。

使用单个数组或表格时无需声明 `$` 或 `$$` 符号。



- 例子：



```

$$

\begin{array}{c|lcr}

    n & \text{左对齐} & \text{居中对齐} & \text{右对齐} \\

    \hline

    1 & 0.24 & 1 & 125 \\

    2 & -1 & 189 & -8 \\

    3 & -20 & 2000 & 1+10i \\

  \end{array}

$$

```



- 显示：



$$

\begin{array}{c|lcr}

    n & \text{左对齐} & \text{居中对齐} & \text{右对齐} \\

    \hline

    1 & 0.24 & 1 & 125 \\

    2 & -1 & 189 & -8 \\

    3 & -20 & 2000 & 1+10i \\

  \end{array}

$$



#### 2．如何输入一个嵌套的数组或表格



多个数组\表格可 **互相嵌套** 并组成一组数组或表格。

使用嵌套前必须声明 `$$` 符号。



- 例子：



```

$$

\begin{array}{c} % 总表格

    \begin{array}{cc} % 第一行内分成两列

        \begin{array}{c|cccc} % 第一列"最小值"数组

            \text{min} & 0 & 1 & 2 & 3 \\

            \hline

            0 & 0 & 0 & 0 & 0 \\

            1 & 0 & 1 & 1 & 1 \\

            2 & 0 & 1 & 2 & 2 \\

            3 & 0 & 1 & 2 & 3 \\

        \end{array}

        &

        \begin{array}{c|cccc} % 第二列"最大值"数组

            \text{max} & 0 & 1 & 2 & 3 \\

            \hline

            0 & 0 & 1 & 2 & 3 \\

            1 & 1 & 1 & 2 & 3 \\

            2 & 2 & 2 & 2 & 3 \\

            3 & 3 & 3 & 3 & 3 \\

        \end{array}

    \end{array} % 第一行表格组结束

    \\

    \begin{array}{c|cccc} % 第二行 Delta 值数组

        \Delta & 0 & 1 & 2 & 3 \\

        \hline

        0 & 0 & 1 & 2 & 3 \\

        1 & 1 & 0 & 1 & 2 \\

        2 & 2 & 1 & 0 & 1 \\

        3 & 3 & 2 & 1 & 0 \\

    \end{array} % 第二行表格结束

\end{array} % 总表格结束

$$

```



- 显示：



$$

\begin{array}{c} % 总表格

    \begin{array}{cc} % 第一行内分成两列

        \begin{array}{c|cccc} % 第一列"最小值"数组

            \text{min} & 0 & 1 & 2 & 3 \\

            \hline

            0 & 0 & 0 & 0 & 0 \\

            1 & 0 & 1 & 1 & 1 \\

            2 & 0 & 1 & 2 & 2 \\

            3 & 0 & 1 & 2 & 3 \\

        \end{array}

        &

        \begin{array}{c|cccc} % 第二列"最大值"数组

            \text{max} & 0 & 1 & 2 & 3 \\

            \hline

            0 & 0 & 1 & 2 & 3 \\

            1 & 1 & 1 & 2 & 3 \\

            2 & 2 & 2 & 2 & 3 \\

            3 & 3 & 3 & 3 & 3 \\

        \end{array}

    \end{array} % 第一行表格组结束

    \\

    \begin{array}{c|cccc} % 第二行 Delta 值数组

        \Delta & 0 & 1 & 2 & 3 \\

        \hline

        0 & 0 & 1 & 2 & 3 \\

        1 & 1 & 0 & 1 & 2 \\

        2 & 2 & 1 & 0 & 1 \\

        3 & 3 & 2 & 1 & 0 \\

    \end{array} % 第二行表格结束

\end{array} % 总表格结束

$$



#### 3．如何输入一个方程组



可以使用 `\begin{array} … \end{array}` 和 `\left\{ … \right.` 来创建一个方程组：



- 例子：



```

$$

\left\{ 

    \begin{array}{c}

        a_1x+b_1y+c_1z=d_1 \\ 

        a_2x+b_2y+c_2z=d_2 \\ 

        a_3x+b_3y+c_3z=d_3 \\

    \end{array}

\right. 

$$

```



- 显示：



$$

\left\{ 

    \begin{array}{c}

        a_1x+b_1y+c_1z=d_1 \\ 

        a_2x+b_2y+c_2z=d_2 \\ 

        a_3x+b_3y+c_3z=d_3 \\

    \end{array}

\right. 

$$



或使用条件表达式组 `\begin{cases} … \end{cases}` 来实现相同效果：



- 例子：



```

$$

\begin{cases}

    a_1x+b_1y+c_1z=d_1 \\ 

    a_2x+b_2y+c_2z=d_2 \\ 

    a_3x+b_3y+c_3z=d_3 \\

\end{cases}

$$

```



- 显示：



$$

\begin{cases}

    a_1x+b_1y+c_1z=d_1 \\ 

    a_2x+b_2y+c_2z=d_2 \\ 

    a_3x+b_3y+c_3z=d_3 \\

\end{cases}

$$



### 五、连分数使用参考



#### 1．如何输入一个连分式



就像输入分式时使用 `\frac` 一样，使用 `\cfrac` 来创建一个连分数。



- 例子：



```

$$

x = a_0 + \cfrac{1^2}{a_1 +

            \cfrac{2^2}{a_2 +

              \cfrac{3^2}{a_3 +

                \cfrac{4^4}{a_4 + 

                  \cdots

                }

              }

            }

          }

$$

```



- 显示：



$$

x = a_0 + \cfrac{1^2}{a_1 +

            \cfrac{2^2}{a_2 +

              \cfrac{3^2}{a_3 +

                \cfrac{4^4}{a_4 + 

                  \cdots

                }

              }

            }

          }

$$



不要使用普通的 `\frac` 或 `\over` 来生成连分数，这样会看起来**很恶心**。



- 反例：



```

$$

x = a_0 + \frac{1^2}{a_1 +

            \frac{2^2}{a_2 +

              \frac{3^2}{a_3 +

                \frac{4^4}{a_4 + 

                  \cdots

                }

              }

            }

          }

$$

```



- 显示：



$$

x = a_0 + \frac{1^2}{a_1 +

            \frac{2^2}{a_2 +

              \frac{3^2}{a_3 +

                \frac{4^4}{a_4 + 

                  \cdots

                }

              }

            }

          }

$$



当然，你可以使用 `\frac` 来表达连分数的**紧缩记法**。



- 例子：



```

$$

x = a_0 + \frac{1^2}{a_1 +}

          \frac{2^2}{a_2 +}

          \frac{3^2}{a_3 +}

          \frac{4^4}{a_4 +}

          \cdots

$$

```



- 显示：



$$

x = a_0 + \frac{1^2}{a_1 +}

          \frac{2^2}{a_2 +}

          \frac{3^2}{a_3 +}

          \frac{4^4}{a_4 +}

          \cdots

$$



连分数通常都太大以至于不易排版，所以建议在连分数前后声明 `$$` 符号，或使用像 `[a0,a1,a2,a3,…]` 一样的紧缩记法。



### 六、一些特殊的注意事项



These are issues that won't affect the correctness of formulas, but might make them look significantly better or worse. Beginners should feel free to ignore this advice; someone else will correct it for them, or more likely nobody will care.



现在指出的小问题并不会影响公式的正确显示，但能让它们看起来明显更好看。初学者可无视这些建议，自然会有强迫症患者替你们改掉它的，或者更可能地，不会有人在意这些细节。



Don't use `\frac` in exponents or limits of integrals; it looks bad and can be confusing, which is why it is rarely done in professional mathematical typesetting. Write the fraction horizontally, with a slash:



在以 $$e$$ 为底的指数函数、极限和积分中尽量不要使用 `\frac` 符号——它会使整段函数看起来很奇怪并可能产生歧义，因此它在专业数学排版中几乎从不出现。可试着横着写这些分式，中间使用斜线间隔 `/` （用斜线代替分数线）。



- 例子：



```

$$

\begin{array}{cc}

    \mathrm{Bad} & \mathrm{Better} \\

    \hline \\

    \large e^{i\frac{\pi}2} \quad e^{\frac{i\pi}2}& \large e^{i\pi/2} \\[2ex]

    \int_{-\frac\pi2}^\frac\pi2 \sin x\,dx & \int_{-\pi/2}^{\pi/2}\sin x\,dx \\

\end{array}

$$

```



- 显示：



$$

  \begin{array}{cc}

      \mathrm{Bad} & \mathrm{Better} \\

      \hline \\

      \large e^{i\frac{\pi}2} \quad e^{\frac{i\pi}2}& \large e^{i\pi/2} \\[2ex]

      \int_{-\frac\pi2}^\frac\pi2 \sin x\,dx & \int_{-\pi/2}^{\pi/2}\sin x\,dx \\

  \end{array}

$$



The `|` symbol has the wrong spacing when it is used as a divider, for example in set comprehensions. Use `\mid` instead:



使用 `|` 符号作为分隔符时会产生错误的间距，因此在需要分隔时最好使用 `\mid` 来代替它。



- 例子:



```

$$

\begin{array}{cc}

    \mathrm{Bad} & \mathrm{Better} \\

    \hline \\

    \{x|x^2\in\Bbb Z\} & \{x\mid x^2\in\Bbb Z\} \\

\end{array}

$$

```



- 显示：

  

  $$

  \begin{array}{cc}

      \mathrm{Bad} & \mathrm{Better} \\

      \hline \\

      \{x|x^2\in\Bbb Z\} & \{x\mid x^2\in\Bbb Z\} \\

  \end{array}

  $$



For double and triple integrals, don't use `\int\int` or `\int\int\int`. Instead use the special forms `\iint` and `\iiint`:



使用多重积分符号时，不要多次使用 `\int` 来声明，直接使用 `\iint` 来表示**二重积分**，使用 `\iiint` 来表示**三重积分**。



Use `\,`, to insert a thin space before differentials; without this LeTeX will mash them together:



使用多重积分时，在被积变量后加入 `\,` （或在微分符号 $${\rm d}$$ 之前）来插入一个小的间距，否则各种被积变量将会挤成一团。注意比较 $${\rm d}z{\rm d} y{\rm d} x$$ 的不同。



- 例子：



```

$$

\begin{array}{cc}

    \mathrm{Bad} & \mathrm{Better} \\

    \hline \\

    \iiint_V f(x){\rm d}z {\rm d}y {\rm d}x & \iiint_{\boldsymbol{V}} f(x)\,{\rm d}z\,{\rm d}y\,{\rm d}x \\

\end{array}

$$

```



- 显示：

  

  $$

  \begin{array}{cc}

      \mathrm{Bad} & \mathrm{Better} \\

      \hline \\

      \iiint_V f(x){\rm d}z {\rm d}y {\rm d}x & \iiint_{\boldsymbol{V}} f(x)\,{\rm d}z\,{\rm d}y\,{\rm d}x \\

  \end{array}

  $$



---



感谢您花费时间阅读这份指导手册，本手册内容可能有疏漏之处，欢迎更改指正。



祝您记录、阅读、分享愉快！



XiaoBei/Write



2021-07-29