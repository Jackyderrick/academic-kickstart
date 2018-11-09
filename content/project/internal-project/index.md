+++
# Project title.
title = "实时情绪波动图谱"

# Date this page was created.
date = 2016-04-27T00:00:00

# Project summary to display on homepage.
summary = "通过Python通过与女朋友聊天获取她的实时情绪波动图谱."

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["gitbook"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Featured image
# To use, add an image named `featured.jpg/png` to your project's folder. 
[image]
  # Caption (optional)
  caption = "Photo by rawpixel on Unsplash"
  
  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = "Smart"
+++


<blockquote><p>Github : <a href="https://github.com/CasterWx">CasterWx</a> <a href="https://github.com/CasterWx/python-girlfriend-mood/blob/master/CS.jpg?raw=true" target="_blank" rel="noopener noreferrer"><img src="https://github.com/CasterWx/python-girlfriend-mood/raw/master/CS.jpg?raw=true" alt="todo" /></a></p></blockquote>
<p>&#x1f61a;&#x1f61a; 通过女朋友的一句话分析她的心情 。</p>
<p>Analyze her mood through her girlfriend&#8217;s words .</p>
<h2><a id="user-content-第一章-分词" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#%E7%AC%AC%E4%B8%80%E7%AB%A0-%E5%88%86%E8%AF%8D" aria-hidden="true"></a>第一章 分词</h2>
<h3><a id="user-content-1jieba库" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#1jieba%E5%BA%93" aria-hidden="true"></a>1、JieBa库</h3>
<blockquote><p>“结巴”中文分词：做最好的 Python 中文分词组件</p></blockquote>
<blockquote><p>&#8220;Jieba&#8221; (Chinese for &#8220;to stutter&#8221;) Chinese text segmentation: built to be the best Python Chinese word segmentation module.</p></blockquote>
<h3><a id="user-content-2特点" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#2%E7%89%B9%E7%82%B9" aria-hidden="true"></a>2、特点</h3>
<ul>
<li>支持三种分词模式：
<ul>
<li>精确模式，试图将句子最精确地切开，适合文本分析；</li>
<li>全模式，把句子中所有的可以成词的词语都扫描出来, 速度非常快，但是不能解决歧义；</li>
<li>搜索引擎模式，在精确模式的基础上，对长词再次切分，提高召回率，适合用于搜索引擎分词。</li>
</ul>
</li>
<li>支持繁体分词</li>
<li>支持自定义词典</li>
<li>MIT 授权协议</li>
</ul>
<h3><a id="user-content-3算法" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#3%E7%AE%97%E6%B3%95" aria-hidden="true"></a>3、算法</h3>
<ul>
<li>基于前缀词典实现高效的词图扫描，生成句子中汉字所有可能成词情况所构成的有向无环图 (DAG)</li>
<li>采用了动态规划查找最大概率路径, 找出基于词频的最大切分组合</li>
<li>对于未登录词，采用了基于汉字成词能力的 HMM 模型，使用了 Viterbi 算法</li>
</ul>
<h3><a id="user-content-4主要功能" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#4%E4%B8%BB%E8%A6%81%E5%8A%9F%E8%83%BD" aria-hidden="true"></a>4、主要功能</h3>
<h4><a id="user-content-1-分词" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#1-%E5%88%86%E8%AF%8D" aria-hidden="true"></a>1) 分词</h4>
<ul>
<li><code>jieba.cut</code> 方法接受三个输入参数: 需要分词的字符串；cut_all 参数用来控制是否采用全模式；HMM 参数用来控制是否使用 HMM 模型</li>
<li><code>jieba.cut_for_search</code> 方法接受两个参数：需要分词的字符串；是否使用 HMM 模型。该方法适合用于搜索引擎构建倒排索引的分词，粒度比较细</li>
<li>待分词的字符串可以是 unicode 或 UTF-8 字符串、GBK 字符串。注意：不建议直接输入 GBK 字符串，可能无法预料地错误解码成 UTF-8</li>
<li><code>jieba.cut</code> 以及 <code>jieba.cut_for_search</code> 返回的结构都是一个可迭代的 generator，可以使用 for 循环来获得分词后得到的每一个词语(unicode)，或者用</li>
<li><code>jieba.lcut</code> 以及 <code>jieba.lcut_for_search</code> 直接返回 list</li>
<li><code>jieba.Tokenizer(dictionary=DEFAULT_DICT)</code> 新建自定义分词器，可用于同时使用不同词典。<code>jieba.dt</code> 为默认分词器，所有全局分词相关函数都是该分词器的映射。</li>
</ul>
<div class="highlight highlight-source-python">
<pre>seg_list <span class="pl-k">=</span> jieba.cut(<span class="pl-s"><span class="pl-pds">"</span>我要有女朋友了<span class="pl-pds">"</span></span>, <span class="pl-v">cut_all</span><span class="pl-k">=</span><span class="pl-c1">True</span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>全模式: <span class="pl-pds">"</span></span> <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">"</span>/ <span class="pl-pds">"</span></span>.join(seg_list))  <span class="pl-c"># 全模式</span>

seg_list <span class="pl-k">=</span> jieba.cut(<span class="pl-s"><span class="pl-pds">"</span>我要有女朋友了<span class="pl-pds">"</span></span>, <span class="pl-v">cut_all</span><span class="pl-k">=</span><span class="pl-c1">False</span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>默认模式: <span class="pl-pds">"</span></span> <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">"</span>/ <span class="pl-pds">"</span></span>.join(seg_list))  <span class="pl-c"># 默认模式</span>

seg_list <span class="pl-k">=</span> jieba.cut(<span class="pl-s"><span class="pl-pds">"</span>我要有女朋友了<span class="pl-pds">"</span></span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>, <span class="pl-pds">"</span></span>.join(seg_list))

seg_list <span class="pl-k">=</span> jieba.cut_for_search(<span class="pl-s"><span class="pl-pds">"</span>我要有女朋友了，然后我要打爆室友的狗头<span class="pl-pds">"</span></span>)  <span class="pl-c"># 搜索引擎模式</span>
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>搜索引擎模式: <span class="pl-pds">"</span></span><span class="pl-k">+</span><span class="pl-s"><span class="pl-pds">"</span>, <span class="pl-pds">"</span></span>.join(seg_list))</pre>
</div>
<p>output :</p>
<pre><code>全模式: 我/ 要/ 有/ 女朋友/ 朋友/ 了
默认模式: 我要/ 有/ 女朋友/ 了
我要, 有, 女朋友, 了
搜索引擎模式: 我要, 有, 朋友, 女朋友, 了, ，, 然后, 我要, 打爆, 室友, 的, 狗头
</code></pre>
<h4><a id="user-content-2-添加自定义词典" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#2-%E6%B7%BB%E5%8A%A0%E8%87%AA%E5%AE%9A%E4%B9%89%E8%AF%8D%E5%85%B8" aria-hidden="true"></a>2) 添加自定义词典</h4>
<blockquote><p>载入词典</p></blockquote>
<ul>
<li>开发者可以指定自己自定义的词典，以便包含 jieba 词库里没有的词。虽然 jieba 有新词识别能力，但是自行添加新词可以保证更高的正确率</li>
<li>用法： jieba.load_userdict(file_name) # file_name 为文件类对象或自定义词典的路径</li>
<li>词典格式和 <code>dict.txt</code> 一样，一个词占一行；每一行分三部分：词语、词频（可省略）、词性（可省略），用空格隔开，顺序不可颠倒。<code>file_name</code> 若为路径或二进制方式打开的文件，则文件必须为 UTF-8 编码。</li>
<li>词频省略时使用自动计算的能保证分出该词的词频。</li>
</ul>
<div class="highlight highlight-source-python">
<pre><span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>/<span class="pl-pds">'</span></span>.join(jieba.cut(<span class="pl-s"><span class="pl-pds">'</span>这个东梨会不会被分开呢。<span class="pl-pds">'</span></span>, <span class="pl-v">HMM</span><span class="pl-k">=</span><span class="pl-c1">False</span>)))
<span class="pl-c"># 添加字典</span>
<span class="pl-c1">print</span>(jieba.suggest_freq((<span class="pl-s"><span class="pl-pds">'</span>东梨<span class="pl-pds">'</span></span>), <span class="pl-c1">True</span>)) <span class="pl-c"># 添加一个词语'东梨'</span>
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>/<span class="pl-pds">'</span></span>.join(jieba.cut(<span class="pl-s"><span class="pl-pds">'</span>这个东梨会不会被分开呢。<span class="pl-pds">'</span></span>, <span class="pl-v">HMM</span><span class="pl-k">=</span><span class="pl-c1">False</span>)))</pre>
</div>
<p>output :</p>
<pre><code>这个/东/梨/会/不会/被/分开/呢/。
这个/东梨/会/不会/被/分开/呢/。
</code></pre>
<blockquote><p>调整词典</p></blockquote>
<ul>
<li>使用 <code>add_word(word, freq=None, tag=None)</code> 和 <code>del_word(word)</code> 可在程序中动态修改词典。</li>
<li>使用 <code>suggest_freq(segment, tune=True)</code> 可调节单个词语的词频，使其能（或不能）被分出来。</li>
<li>注意：自动计算的词频在使用 HMM 新词发现功能时可能无效。</li>
</ul>
<h4><a id="user-content-3-关键词提取" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#3-%E5%85%B3%E9%94%AE%E8%AF%8D%E6%8F%90%E5%8F%96" aria-hidden="true"></a>3) 关键词提取</h4>
<blockquote><p>基于 TF-IDF 算法的关键词抽取</p></blockquote>
<p><code>import jieba.analyse</code></p>
<ul>
<li>jieba.analyse.extract_tags(sentence, topK=20, withWeight=False, allowPOS=())
<ul>
<li>sentence 为待提取的文本</li>
<li>topK 为返回几个 TF/IDF 权重最大的关键词，默认值为 20</li>
<li>withWeight 为是否一并返回关键词权重值，默认值为 False</li>
<li>allowPOS 仅包括指定词性的词，默认值为空，即不筛选</li>
</ul>
</li>
<li>jieba.analyse.TFIDF(idf_path=None) 新建 TFIDF 实例，idf_path 为 IDF 频率文件</li>
</ul>
<div class="highlight highlight-source-python">
<pre>s <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>操作系统（Operation System，简称OS）是管理计算机硬件与软件资源的程序，是计算机系统的内核与基石；操作系统本质上是运行在计算机上的软件程序 ；为用户提供一个与系统交互的操作界面 ；操作系统分内核与外壳（我们可以把外壳理解成围绕着内核的应用程序，而内核就是能操作硬件的程序）。<span class="pl-pds">"</span></span>
<span class="pl-k">for</span> x, w <span class="pl-k">in</span> jieba.analyse.extract_tags(s, <span class="pl-v">withWeight</span><span class="pl-k">=</span><span class="pl-c1">True</span>):
    <span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span><span class="pl-c1">%s</span> <span class="pl-c1">%s</span><span class="pl-pds">'</span></span> <span class="pl-k">%</span> (x, w))

<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>-<span class="pl-pds">'</span></span><span class="pl-k">*</span><span class="pl-c1">40</span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span> TextRank<span class="pl-pds">'</span></span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>-<span class="pl-pds">'</span></span><span class="pl-k">*</span><span class="pl-c1">40</span>)

<span class="pl-k">for</span> x, w <span class="pl-k">in</span> jieba.analyse.textrank(s, <span class="pl-v">withWeight</span><span class="pl-k">=</span><span class="pl-c1">True</span>):
    <span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span><span class="pl-c1">%s</span> <span class="pl-c1">%s</span><span class="pl-pds">'</span></span> <span class="pl-k">%</span> (x, w))</pre>
</div>
<p>output :</p>
<pre><code>内核 1.0625279118105262
操作系统 0.7315222629276317
外壳 0.4645002019336842
软件程序 0.36580730663157895
软件资源 0.34756659135263157
程序 0.3333060550794737
操作界面 0.32345367735526315
Operation 0.31459914481315787
System 0.31459914481315787
OS 0.31459914481315787
计算机硬件 0.2800679240526316
应用程序 0.2763021123763158
计算机系统 0.23982068182078944
交互 0.23731251919447366
基石 0.23595272944342105
硬件 0.22168984473789474
本质 0.18271527055526315
用户 0.1795351598005263
计算机 0.1790732744968421
围绕 0.177282393885
----------------------------------------
 TextRank
----------------------------------------
内核 1.0
程序 0.5362199524590612
系统 0.48948949335129555
提供 0.48602227553244165
围绕 0.4446670737747918
运行 0.4225011310851474
管理 0.4151898395341863
基石 0.4131936048253403
计算机系统 0.38302557644090945
硬件 0.36775003601316436
操作 0.36615155530109056
本质 0.3554627436547271
计算机硬件 0.3491604047032015
理解 0.3433887505596043
外壳 0.3419635842574655
应用程序 0.33616306371021853
用户 0.33122514947879544
交互 0.3287196036788538
计算机 0.23122054865622482
简称 0.22777433887730136
</code></pre>
<h4><a id="user-content-4-词性标注" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#4-%E8%AF%8D%E6%80%A7%E6%A0%87%E6%B3%A8" aria-hidden="true"></a>4) 词性标注</h4>
<ul>
<li><code>jieba.posseg.POSTokenizer(tokenizer=None)</code> 新建自定义分词器，<code>tokenizer</code> 参数可指定内部使用的 <code>jieba.Tokenizer</code> 分词器。<code>jieba.posseg.dt</code> 为默认词性标注分词器。</li>
<li>标注句子分词后每个词的词性，采用和 ictclas 兼容的标记法。</li>
<li>用法示例</li>
</ul>
<div class="highlight highlight-source-python">
<pre>words <span class="pl-k">=</span> jieba.posseg.cut(<span class="pl-s"><span class="pl-pds">"</span>我爱北京天安门<span class="pl-pds">"</span></span>)
<span class="pl-k">for</span> word, flag <span class="pl-k">in</span> words:
    <span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span><span class="pl-c1">%s</span> <span class="pl-c1">%s</span><span class="pl-pds">'</span></span> <span class="pl-k">%</span> (word, flag))
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>=<span class="pl-pds">'</span></span><span class="pl-k">*</span><span class="pl-c1">40</span>)</pre>
</div>
<p>output :</p>
<pre><code>我 r
爱 v
北京 ns
天安门 ns
</code></pre>
<h4><a id="user-content-5-并行分词" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#5-%E5%B9%B6%E8%A1%8C%E5%88%86%E8%AF%8D" aria-hidden="true"></a>5) 并行分词</h4>
<ul>
<li>原理：将目标文本按行分隔后，把各行文本分配到多个 Python 进程并行分词，然后归并结果，从而获得分词速度的可观提升</li>
<li>基于 python 自带的 multiprocessing 模块，目前暂不支持 Windows</li>
<li>用法：
<ul>
<li><code>jieba.enable_parallel(4)</code> # 开启并行分词模式，参数为并行进程数</li>
<li><code>jieba.disable_parallel()</code> # 关闭并行分词模式</li>
</ul>
</li>
</ul>
<h4><a id="user-content-6-tokenize返回词语在原文的起止位置" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#6-tokenize%E8%BF%94%E5%9B%9E%E8%AF%8D%E8%AF%AD%E5%9C%A8%E5%8E%9F%E6%96%87%E7%9A%84%E8%B5%B7%E6%AD%A2%E4%BD%8D%E7%BD%AE" aria-hidden="true"></a>6) Tokenize：返回词语在原文的起止位置</h4>
<ul>
<li>注意，输入参数只接受 unicode</li>
<li>默认模式</li>
</ul>
<div class="highlight highlight-source-python">
<pre><span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span> 默认模式<span class="pl-pds">'</span></span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>-<span class="pl-pds">'</span></span><span class="pl-k">*</span><span class="pl-c1">40</span>)
result <span class="pl-k">=</span> jieba.tokenize(<span class="pl-s"><span class="pl-pds">'</span>永和服装饰品有限公司<span class="pl-pds">'</span></span>)
<span class="pl-k">for</span> tk <span class="pl-k">in</span> result:
    <span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>word <span class="pl-c1">%s</span><span class="pl-cce">\t\t</span> start: <span class="pl-c1">%d</span> <span class="pl-cce">\t\t</span> end:<span class="pl-c1">%d</span><span class="pl-pds">"</span></span> <span class="pl-k">%</span> (tk[<span class="pl-c1">0</span>],tk[<span class="pl-c1">1</span>],tk[<span class="pl-c1">2</span>]))

<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>-<span class="pl-pds">'</span></span><span class="pl-k">*</span><span class="pl-c1">40</span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span> 搜索模式<span class="pl-pds">'</span></span>)
<span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">'</span>-<span class="pl-pds">'</span></span><span class="pl-k">*</span><span class="pl-c1">40</span>)

result <span class="pl-k">=</span> jieba.tokenize(<span class="pl-s"><span class="pl-pds">'</span>永和服装饰品有限公司<span class="pl-pds">'</span></span>, <span class="pl-v">mode</span><span class="pl-k">=</span><span class="pl-s"><span class="pl-pds">'</span>search<span class="pl-pds">'</span></span>)
<span class="pl-k">for</span> tk <span class="pl-k">in</span> result:
    <span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>word <span class="pl-c1">%s</span><span class="pl-cce">\t\t</span> start: <span class="pl-c1">%d</span> <span class="pl-cce">\t\t</span> end:<span class="pl-c1">%d</span><span class="pl-pds">"</span></span> <span class="pl-k">%</span> (tk[<span class="pl-c1">0</span>],tk[<span class="pl-c1">1</span>],tk[<span class="pl-c1">2</span>]))</pre>
</div>
<p>output :</p>
<pre><code>word 永和		 start: 0 		 end:2
word 服装		 start: 2 		 end:4
word 饰品		 start: 4 		 end:6
word 有限公司		 start: 6 		 end:10
----------------------------------------
 搜索模式
----------------------------------------
word 永和		 start: 0 		 end:2
word 服装		 start: 2 		 end:4
word 饰品		 start: 4 		 end:6
word 有限		 start: 6 		 end:8
word 公司		 start: 8 		 end:10
word 有限公司		 start: 6 		 end:10
</code></pre>
<h3><a id="user-content-5一个完整的分词可运行实例" class="anchor" href="https://github.com/CasterWx/python-girlfriend-mood#5%E4%B8%80%E4%B8%AA%E5%AE%8C%E6%95%B4%E7%9A%84%E5%88%86%E8%AF%8D%E5%8F%AF%E8%BF%90%E8%A1%8C%E5%AE%9E%E4%BE%8B" aria-hidden="true"></a>5、一个完整的分词可运行实例</h3>
<p>目录结构</p>
<blockquote><p>jieba是我们要导入的第三方库，在项目中我直接把它放在了里面。</p></blockquote>
<pre><code>│  run.py
│
└─jieba
    │  dict.txt
    │  _compat.py
    │  __init__.py
    │  __main__.py
    │
    ├─analyse
    │  │  analyzer.py
    │  │  idf.txt
    │  │  textrank.py
    │  │  tfidf.py
    │  │  __init__.py
    │  │
    │  └─__pycache__
    │          analyzer.cpython-37.pyc
    │          textrank.cpython-37.pyc
    │          tfidf.cpython-37.pyc
    │          __init__.cpython-37.pyc
    │
    ├─finalseg
    │  │  prob_emit.p
    │  │  prob_emit.py
    │  │  prob_start.p
    │  │  prob_start.py
    │  │  prob_trans.p
    │  │  prob_trans.py
    │  │  __init__.py
    │  │
    │  └─__pycache__
    │          prob_emit.cpython-37.pyc
    │          prob_start.cpython-37.pyc
    │          prob_trans.cpython-37.pyc
    │          __init__.cpython-37.pyc
    │
    ├─posseg
    │  │  char_state_tab.p
    │  │  char_state_tab.py
    │  │  prob_emit.p
    │  │  prob_emit.py
    │  │  prob_start.p
    │  │  prob_start.py
    │  │  prob_trans.p
    │  │  prob_trans.py
    │  │  viterbi.py
    │  │  __init__.py
    │  │
    │  └─__pycache__
    │          char_state_tab.cpython-37.pyc
    │          prob_emit.cpython-37.pyc
    │          prob_start.cpython-37.pyc
    │          prob_trans.cpython-37.pyc
    │          viterbi.cpython-37.pyc
    │          __init__.cpython-37.pyc
    │
    └─__pycache__
            _compat.cpython-37.pyc
            __init__.cpython-37.pyc
</code></pre>
<p>run.py中编写代码，并且调用jieba库实现分词。</p>
<p>run.py</p>
<div class="highlight highlight-source-python">
<pre><span class="pl-c">#encoding=utf-8</span>
<span class="pl-k">from</span> <span class="pl-c1">__future__</span> <span class="pl-k">import</span> unicode_literals
<span class="pl-k">import</span> jieba

<span class="pl-k">if</span> <span class="pl-c1">__name__</span><span class="pl-k">==</span><span class="pl-s"><span class="pl-pds">"</span>__main__<span class="pl-pds">"</span></span>:
    ch <span class="pl-k">=</span> <span class="pl-c1">input</span>()
    seg_list <span class="pl-k">=</span> jieba.cut(<span class="pl-c1">str</span>(ch))
    <span class="pl-c1">print</span>(<span class="pl-s"><span class="pl-pds">"</span>, <span class="pl-pds">"</span></span>.join(seg_list))</pre>
</div>
<p>在此处输入&#8221;我马上就要有女朋友了&#8221;。</p>
<p>即可得到输出结果如下。</p>
<blockquote><p>我, 马上, 就要, 有, 女朋友, 了</p></blockquote>
</article>