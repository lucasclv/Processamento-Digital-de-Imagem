# test
<html lang="pr-br"><head>
	<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/google/code-prettify@master/loader/skins/doxy.css">
<style>
body {
    background-color: rgb(11, 12, 20);
	margin-left: 150px;
	margin-right: 150px;
}
img{
	display: block;
	margin-left: auto;
    margin-right: auto;
}
h1 {
	color: white;
	font-family: "Times New Roman";
}
h2 {
	color: white;
	font-family: "Times New Roman";
}
h3 {
	color: white;
	font-family: "Times New Roman";
}
p {
	border-bottom-style: solid;
	color: white;
	font-family: "Times New Roman";
}

<title>Page Title</title>
</style>
</head>
<body>
<h1>Processamento Digital de Imagens</h1>
<p>Aluno: Vitor Fassanaro Cortez de Carvalho
</p>
<h2>Atividade 1 - Inverter Cores e Trocar Regiões</h2>
<h3>1.1 - Inverter Cores</h3>
<p>
Utilizando como base o regions.cpp.<br>
Imagem utilizada:<br>
<img src="\Nova pasta\carro2.jpg" alt="Um carro" style="width:35%"><br>
Imagem de saída do programa:<br>
<img src="\Nova pasta\invertido.jpg" alt="Um carro" style="width:35%"><br>
Código Utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> img </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">);</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> imgo </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">);</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> ai</span><span class="pun">,</span><span class="pln"> li</span><span class="pun">,</span><span class="pln">af</span><span class="pun">,</span><span class="pln">lf</span><span class="pun">;</span><span class="pln">
	</span><span class="com">//Criando a matriz para inverter as cores numa imagem colorida</span><span class="pln">
	</span><span class="typ">Vec3b</span><span class="pln"> val</span><span class="pun">;</span><span class="pln">
	val</span><span class="pun">[</span><span class="lit">0</span><span class="pun">]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="lit">255</span><span class="pun">;</span><span class="pln">
	val</span><span class="pun">[</span><span class="lit">1</span><span class="pun">]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="lit">255</span><span class="pun">;</span><span class="pln">
	val</span><span class="pun">[</span><span class="lit">2</span><span class="pun">]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="lit">255</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Altura "</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">rows </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Largura "</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">cols </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Digite Altura inicial"</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cin </span><span class="pun">&gt;&gt;</span><span class="pln"> ai</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Digite Altura final"</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cin </span><span class="pun">&gt;&gt;</span><span class="pln"> af</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Digite Largura inicial"</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cin </span><span class="pun">&gt;&gt;</span><span class="pln"> li</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Digite Largura final"</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cin </span><span class="pun">&gt;&gt;</span><span class="pln"> lf</span><span class="pun">;</span><span class="pln">
	</span><span class="com">//Negativando a imagem no local selecionado</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i</span><span class="pun">=</span><span class="pln">ai</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> af</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j</span><span class="pun">=</span><span class="pln">li</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> lf</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			img</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> val </span><span class="pun">-</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	namedWindow</span><span class="pun">(</span><span class="str">"imagemod"</span><span class="pun">,</span><span class="pln"> WINDOW_AUTOSIZE</span><span class="pun">);</span><span class="pln">
	imshow</span><span class="pun">(</span><span class="str">"imagemod"</span><span class="pun">,</span><span class="pln"> img</span><span class="pun">);</span><span class="pln">
	namedWindow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> WINDOW_AUTOSIZE</span><span class="pun">);</span><span class="pln">
	imshow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> imgo</span><span class="pun">);</span><span class="pln">
	imwrite</span><span class="pun">(</span><span class="str">"invertido.jpg"</span><span class="pun">,</span><span class="pln"> img</span><span class="pun">);</span><span class="pln">
	waitKey</span><span class="pun">();</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></code>
</pre>
<p></p>
<h3>1.2 - Trocar Regiões</h3>
<p>
Para essa parte da atividade fora utilizado o mesmo regions.cpp e a mesma imagem do item 1.1.<br>
Nesse caso a saída do programa foi:<br>
<img src="\Nova pasta\trocado.jpg" alt="Um carro" style="width:35%"><br>
Código Utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> img </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">);</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> a</span><span class="pun">,</span><span class="pln"> l</span><span class="pun">,</span><span class="pln">am</span><span class="pun">,</span><span class="pln">lm</span><span class="pun">;</span><span class="pln">
	a </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">;</span><span class="pln">
	am </span><span class="pun">=</span><span class="pln"> a </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2</span><span class="pun">;</span><span class="pln">
	l </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">;</span><span class="pln">
	lm </span><span class="pun">=</span><span class="pln"> l </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2</span><span class="pun">;</span><span class="pln">
	</span><span class="com">//Criada uma matriz para ser a imagem de saida</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> imgout </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="pln">img</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">,</span><span class="pln"> CV_8UC3</span><span class="pun">);</span><span class="pln">
	</span><span class="com">//Aqui as regiões da imagem são trocadas</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> a</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> l</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">&lt;</span><span class="pln"> am </span><span class="pun">&amp;&amp;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> lm</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				imgout</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i </span><span class="pun">+</span><span class="pln"> am</span><span class="pun">,</span><span class="pln"> j </span><span class="pun">+</span><span class="pln"> lm</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
			</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">&lt;</span><span class="pln"> am </span><span class="pun">&amp;&amp;</span><span class="pln"> j </span><span class="pun">&gt;</span><span class="pln">  lm</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				imgout</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i </span><span class="pun">+</span><span class="pln"> am</span><span class="pun">,</span><span class="pln"> j </span><span class="pun">-</span><span class="pln"> lm</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
			</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">&gt;</span><span class="pln"> am </span><span class="pun">&amp;&amp;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> lm</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				imgout</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i </span><span class="pun">-</span><span class="pln"> am</span><span class="pun">,</span><span class="pln"> j </span><span class="pun">+</span><span class="pln"> lm</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
			</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">&gt;</span><span class="pln"> am </span><span class="pun">&amp;&amp;</span><span class="pln"> j </span><span class="pun">&gt;</span><span class="pln"> lm</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				imgout</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">i </span><span class="pun">-</span><span class="pln"> am</span><span class="pun">,</span><span class="pln"> j </span><span class="pun">-</span><span class="pln"> lm</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">

		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	namedWindow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> WINDOW_AUTOSIZE</span><span class="pun">);</span><span class="pln">
	imshow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> imgout</span><span class="pun">);</span><span class="pln">
	imwrite</span><span class="pun">(</span><span class="str">"trocado.jpg"</span><span class="pun">,</span><span class="pln"> imgout</span><span class="pun">);</span><span class="pln">
	waitKey</span><span class="pun">();</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></code>
</pre>
<p></p>
<h2>Atividade 2 - Detector de Objetos</h2>
<h3>2.1 - Detector</h3>
<p>
Para resolvermos o problema da contagem de objetos que seja acima de 255 podemos zerar o contador enquanto que armazenamos no número de vezes que ele chegou ao valor de 255, no final do laço somaríamos mais uma vezes o valor contido no contador a variável auxiliar para determinarmos o número de objetos na cena.<br>
Utilizando o programa labeling.cpp como base:<br>
Imagem de entrada:<br>
<img src="\Nova pasta\bolhas.png" alt="Varios Objetos" style="width:35%"><br>
Imagem de saída:<br>
<img src="\Nova pasta\bolhas2.png" alt="Varios Objetos" style="width:35%"><br>
Contagem de objetos:<br>
<img src="\Nova pasta\contador.JPG" alt="Janela CMD" style="width:35%"><br>
Código Utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> image</span><span class="pun">,</span><span class="pln"> mask</span><span class="pun">,</span><span class="pln"> imgalt</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> width</span><span class="pun">,</span><span class="pln"> height</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> nobjt</span><span class="pun">,</span><span class="pln"> nobjs</span><span class="pun">,</span><span class="pln"> nobjc</span><span class="pun">;</span><span class="pln">

	</span><span class="typ">CvPoint</span><span class="pln"> p</span><span class="pun">;</span><span class="pln">
	image </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">,</span><span class="pln"> CV_LOAD_IMAGE_GRAYSCALE</span><span class="pun">);</span><span class="pln">
	imgalt </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(!</span><span class="pln">image</span><span class="pun">.</span><span class="pln">data</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		std</span><span class="pun">::</span><span class="pln">cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"imagem nao carregou corretamente\n"</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">return</span><span class="pun">(-</span><span class="lit">1</span><span class="pun">);</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	width </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">width</span><span class="pun">;</span><span class="pln">
	height </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">height</span><span class="pun">;</span><span class="pln">

	p</span><span class="pun">.</span><span class="pln">x </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">	
	p</span><span class="pun">.</span><span class="pln">y </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">

	nobjt </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
	nobjs </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
	nobjc </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
	</span><span class="com">// Procura e preenche os objetos que estejam tocando nas bordas da imagem</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> height</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> width</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">0</span><span class="pln"> </span><span class="pun">||</span><span class="pln"> j </span><span class="pun">==</span><span class="pln"> </span><span class="lit">0</span><span class="pln"> </span><span class="pun">||</span><span class="pln"> i </span><span class="pun">==</span><span class="pln"> height </span><span class="pun">-</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="pun">||</span><span class="pln"> j </span><span class="pun">==</span><span class="pln"> width </span><span class="pun">-</span><span class="pln"> </span><span class="lit">1</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				p</span><span class="pun">.</span><span class="pln">x </span><span class="pun">=</span><span class="pln"> j</span><span class="pun">;</span><span class="pln">
				p</span><span class="pun">.</span><span class="pln">y </span><span class="pun">=</span><span class="pln"> i</span><span class="pun">;</span><span class="pln">
				floodFill</span><span class="pun">(</span><span class="pln">imgalt</span><span class="pun">,</span><span class="pln"> p</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span><span class="com">//Procura os objetos restantes</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i</span><height; i++)="" {="" for="" (int="" j="0;" j<width;="" j++)="" if="" (imgalt.at<uchar=""><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">==</span><span class="pln"> </span><span class="lit">255</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				</span><span class="com">// achou um objeto</span><span class="pln">
				nobjt</span><span class="pun">++;</span><span class="pln">
				p</span><span class="pun">.</span><span class="pln">x </span><span class="pun">=</span><span class="pln"> j</span><span class="pun">;</span><span class="pln">
				p</span><span class="pun">.</span><span class="pln">y </span><span class="pun">=</span><span class="pln"> i</span><span class="pun">;</span><span class="pln">
				floodFill</span><span class="pun">(</span><span class="pln">imgalt</span><span class="pun">,</span><span class="pln"> p</span><span class="pun">,</span><span class="pln"> nobjt</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	p</span><span class="pun">.</span><span class="pln">x </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
	p</span><span class="pun">.</span><span class="pln">y </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
	</span><span class="com">// Invertemos o fundo da imagem para determinar o número de objetos com buracos</span><span class="pln">
	floodFill</span><span class="pun">(</span><span class="pln">image</span><span class="pun">,</span><span class="pln"> p</span><span class="pun">,</span><span class="pln"> </span><span class="lit">255</span><span class="pun">);</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> height</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> width</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">image</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;uchar&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">==</span><span class="pln"> </span><span class="lit">0</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				</span><span class="com">// achou um objeto</span><span class="pln">
				nobjc</span><span class="pun">++;</span><span class="pln">
				p</span><span class="pun">.</span><span class="pln">x </span><span class="pun">=</span><span class="pln"> j</span><span class="pun">;</span><span class="pln">
				p</span><span class="pun">.</span><span class="pln">y </span><span class="pun">=</span><span class="pln"> i</span><span class="pun">;</span><span class="pln">
				floodFill</span><span class="pun">(</span><span class="pln">image</span><span class="pun">,</span><span class="pln"> p</span><span class="pun">,</span><span class="pln"> nobjc</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	nobjs </span><span class="pun">=</span><span class="pln"> nobjt </span><span class="pun">-</span><span class="pln"> nobjc</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"No Total de Objetos "</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> nobjt </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"No de Objetos sem Buracos "</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> nobjs </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"No de Objetos com Burados "</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> nobjc </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	imshow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">);</span><span class="pln">
	imwrite</span><span class="pun">(</span><span class="str">"labeling.png"</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">);</span><span class="pln">
	waitKey</span><span class="pun">();</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></height;></code>
</pre>
<p></p>
<h2>Atividade 3 - Equalizador de Histograma e Detector de Movimento</h2>
<h3>3.1 - Equalizador de Histograma</h3>	
<p>
Utilizando o programa histogram.cpp como base.<br>
Imagem utilizada:<br>
<img src="\Nova pasta\carro2.jpg" alt="Um carro" style="width:35%"><br>
Imagem de saída do programa em escala de cinza sem equalização:<br>
<img src="\Nova pasta\grayscalebe.jpg" alt="Um carro" style="width:35%"><br>
Imagem de saída do programa equalizada:<br>
<img src="\Nova pasta\equalizado.jpg" alt="Um carro" style="width:35%"><br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> image </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">);</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> imageout </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> width</span><span class="pun">,</span><span class="pln"> height</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln">hist2</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> nbins </span><span class="pun">=</span><span class="pln"> </span><span class="lit">64</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> range</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">256</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">const</span><span class="pln"> </span><span class="kwd">float</span><span class="pln"> </span><span class="pun">*</span><span class="pln">histrange </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> range </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">bool</span><span class="pln"> uniform </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">true</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">bool</span><span class="pln"> acummulate </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">false</span><span class="pun">;</span><span class="pln">

	width </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">;</span><span class="pln">
	height </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">;</span><span class="pln">

	</span><span class="kwd">int</span><span class="pln"> histw </span><span class="pun">=</span><span class="pln"> nbins</span><span class="pun">,</span><span class="pln"> histh </span><span class="pun">=</span><span class="pln"> nbins </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> histImg</span><span class="pun">(</span><span class="pln">histh</span><span class="pun">,</span><span class="pln"> histw</span><span class="pun">,</span><span class="pln"> CV_8UC1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">));</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> histImg2</span><span class="pun">(</span><span class="pln">histh</span><span class="pun">,</span><span class="pln"> histw</span><span class="pun">,</span><span class="pln"> CV_8UC1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">));</span><span class="pln">
	</span><span class="com">//A função ctvColor torna a transforma a imagem de RGB para tom de cinza</span><span class="pln">
	cvtColor</span><span class="pun">(</span><span class="pln">image</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">,</span><span class="pln"> CV_BGR2GRAY</span><span class="pun">);</span><span class="pln">
	</span><span class="com">//A função equalizeHist é quem proporciona a equalização do histograma</span><span class="pln">
	equalizeHist</span><span class="pun">(</span><span class="pln">image</span><span class="pun">,</span><span class="pln"> imageout</span><span class="pun">);</span><span class="pln">
	</span><span class="com">//Essa parte do código é duplicada para imprimir os histogramas da imagem em tom de cinza</span><span class="pln">
	</span><span class="com">//com e sem equalização.</span><span class="pln">
	calcHist</span><span class="pun">(&amp;</span><span class="pln">imageout</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(),</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">&amp;</span><span class="pln">nbins</span><span class="pun">,</span><span class="pln"> </span><span class="pun">&amp;</span><span class="pln">histrange</span><span class="pun">,</span><span class="pln">
		uniform</span><span class="pun">,</span><span class="pln"> acummulate</span><span class="pun">);</span><span class="pln">
	calcHist</span><span class="pun">(&amp;</span><span class="pln">image</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(),</span><span class="pln"> hist2</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">&amp;</span><span class="pln">nbins</span><span class="pun">,</span><span class="pln"> </span><span class="pun">&amp;</span><span class="pln">histrange</span><span class="pun">,</span><span class="pln">
		uniform</span><span class="pun">,</span><span class="pln"> acummulate</span><span class="pun">);</span><span class="pln">
	normalize</span><span class="pun">(</span><span class="pln">hist2</span><span class="pun">,</span><span class="pln"> hist2</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> histImg2</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> NORM_MINMAX</span><span class="pun">,</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">());</span><span class="pln">
	histImg2</span><span class="pun">.</span><span class="pln">setTo</span><span class="pun">(</span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">0</span><span class="pun">));</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> nbins</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		line</span><span class="pun">(</span><span class="pln">histImg2</span><span class="pun">,</span><span class="pln">
			</span><span class="typ">Point</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> histh</span><span class="pun">),</span><span class="pln">
			</span><span class="typ">Point</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> histh </span><span class="pun">-</span><span class="pln"> cvRound</span><span class="pun">(</span><span class="pln">hist2</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">))),</span><span class="pln">
			</span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">255</span><span class="pun">,</span><span class="pln"> </span><span class="lit">255</span><span class="pun">,</span><span class="pln"> </span><span class="lit">255</span><span class="pun">),</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">8</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	histImg2</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">image</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="lit">10</span><span class="pun">,</span><span class="pln"> nbins</span><span class="pun">,</span><span class="pln"> histh</span><span class="pun">)));</span><span class="pln">
	normalize</span><span class="pun">(</span><span class="pln">hist</span><span class="pun">,</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> histImg</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> NORM_MINMAX</span><span class="pun">,</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">());</span><span class="pln">
	histImg</span><span class="pun">.</span><span class="pln">setTo</span><span class="pun">(</span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">0</span><span class="pun">));</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> nbins</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		line</span><span class="pun">(</span><span class="pln">histImg</span><span class="pun">,</span><span class="pln">
			</span><span class="typ">Point</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> histh</span><span class="pun">),</span><span class="pln">
			</span><span class="typ">Point</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> histh </span><span class="pun">-</span><span class="pln"> cvRound</span><span class="pun">(</span><span class="pln">hist</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">))),</span><span class="pln">
			</span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">255</span><span class="pun">,</span><span class="pln"> </span><span class="lit">255</span><span class="pun">,</span><span class="pln"> </span><span class="lit">255</span><span class="pun">),</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">8</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	histImg</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">imageout</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="lit">10</span><span class="pun">,</span><span class="pln"> nbins</span><span class="pun">,</span><span class="pln"> histh</span><span class="pun">)));</span><span class="pln">
	namedWindow</span><span class="pun">(</span><span class="str">"imagemod"</span><span class="pun">,</span><span class="pln"> WINDOW_AUTOSIZE</span><span class="pun">);</span><span class="pln">
	imshow</span><span class="pun">(</span><span class="str">"imagemod"</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">);</span><span class="pln">
	namedWindow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> WINDOW_AUTOSIZE</span><span class="pun">);</span><span class="pln">
	imshow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> imageout</span><span class="pun">);</span><span class="pln">
	</span><span class="com">//Cria as imagens baseado no Mat selecionado e como é dado o arquivo de saida.</span><span class="pln">
	imwrite</span><span class="pun">(</span><span class="str">"equalizado.jpg"</span><span class="pun">,</span><span class="pln"> imageout</span><span class="pun">);</span><span class="pln">
	imwrite</span><span class="pun">(</span><span class="str">"grayscalebe.jpg"</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">);</span><span class="pln">
	waitKey</span><span class="pun">();</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></code>
</pre>
<p></p>
<h3>3.2 - Detector de Movimento</h3>
<p>
Utilizando o programa histogram.cpp como base.<br>
Temos como imagem de entrada o vídeo capturado pela câmera. Toda vez que é detectado movimento é impresso na tela a mensagem "Movimento Detectado":<br>
<img src="\Nova pasta\motion.jpg" alt="Movimento Detectado" width="800" height="350"><br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;cmath&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> argc</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">char</span><span class="pun">**</span><span class="pln"> argv</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> frameA</span><span class="pun">,</span><span class="pln"> frameB</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">double</span><span class="pln"> teste</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> width</span><span class="pun">,</span><span class="pln"> height</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">VideoCapture</span><span class="pln"> cap</span><span class="pun">;</span><span class="pln">
	vector</span><mat><span class="pln"> planes</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> histB</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> nbins </span><span class="pun">=</span><span class="pln"> </span><span class="lit">64</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> range</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">256</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">const</span><span class="pln"> </span><span class="kwd">float</span><span class="pln"> </span><span class="pun">*</span><span class="pln">histrange </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> range </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">bool</span><span class="pln"> uniform </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">true</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">bool</span><span class="pln"> acummulate </span><span class="pun">=</span><span class="pln"> </span><span class="kwd">false</span><span class="pun">;</span><span class="pln">

	cap</span><span class="pun">.</span><span class="pln">open</span><span class="pun">(</span><span class="lit">0</span><span class="pun">);</span><span class="pln">

	</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(!</span><span class="pln">cap</span><span class="pun">.</span><span class="pln">isOpened</span><span class="pun">())</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"cameras indisponiveis"</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">return</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">;</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">

	width </span><span class="pun">=</span><span class="pln"> cap</span><span class="pun">.</span><span class="kwd">get</span><span class="pun">(</span><span class="pln">CV_CAP_PROP_FRAME_WIDTH</span><span class="pun">);</span><span class="pln">
	height </span><span class="pun">=</span><span class="pln"> cap</span><span class="pun">.</span><span class="kwd">get</span><span class="pun">(</span><span class="pln">CV_CAP_PROP_FRAME_HEIGHT</span><span class="pun">);</span><span class="pln">

	</span><span class="kwd">int</span><span class="pln"> histw </span><span class="pun">=</span><span class="pln"> nbins</span><span class="pun">,</span><span class="pln"> histh </span><span class="pun">=</span><span class="pln"> nbins </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> histImg</span><span class="pun">(</span><span class="pln">histh</span><span class="pun">,</span><span class="pln"> histw</span><span class="pun">,</span><span class="pln"> CV_8UC1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">));</span><span class="pln">
	</span><span class="com">//Aqui fazemos o calculo do primeiro frame para fazermos a primeira comparação de histogramas</span><span class="pln">
	cap </span><span class="pun">&gt;&gt;</span><span class="pln"> frameA</span><span class="pun">;</span><span class="pln">
	cvtColor</span><span class="pun">(</span><span class="pln">frameA</span><span class="pun">,</span><span class="pln"> frameA</span><span class="pun">,</span><span class="pln"> CV_BGR2GRAY</span><span class="pun">);</span><span class="pln">
	calcHist</span><span class="pun">(&amp;</span><span class="pln">frameA</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(),</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">&amp;</span><span class="pln">nbins</span><span class="pun">,</span><span class="pln"> </span><span class="pun">&amp;</span><span class="pln">histrange</span><span class="pun">,</span><span class="pln">
		uniform</span><span class="pun">,</span><span class="pln"> acummulate</span><span class="pun">);</span><span class="pln">
	normalize</span><span class="pun">(</span><span class="pln">hist</span><span class="pun">,</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> histImg</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> NORM_MINMAX</span><span class="pun">,</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">());</span><span class="pln">
	</span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(</span><span class="lit">1</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		cap </span><span class="pun">&gt;&gt;</span><span class="pln"> frameB</span><span class="pun">;</span><span class="pln">
		cvtColor</span><span class="pun">(</span><span class="pln">frameB	</span><span class="pun">,</span><span class="pln"> frameB</span><span class="pun">,</span><span class="pln"> CV_BGR2GRAY</span><span class="pun">);</span><span class="pln">
		calcHist</span><span class="pun">(&amp;</span><span class="pln">frameB</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(),</span><span class="pln"> histB</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln">
			</span><span class="pun">&amp;</span><span class="pln">nbins</span><span class="pun">,</span><span class="pln"> </span><span class="pun">&amp;</span><span class="pln">histrange</span><span class="pun">,</span><span class="pln">
			uniform</span><span class="pun">,</span><span class="pln"> acummulate</span><span class="pun">);</span><span class="pln">
		normalize</span><span class="pun">(</span><span class="pln">histB</span><span class="pun">,</span><span class="pln"> histB</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> histImg</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> NORM_MINMAX</span><span class="pun">,</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">());</span><span class="pln">
		</span><span class="com">//Aqui fazemos o uso da função compareHist com o parametro CV_COMP_CORREL.</span><span class="pln">
		</span><span class="com">//Isso encontrara uma correlação entre os dois histogramas calculados.</span><span class="pln">
		teste </span><span class="pun">=</span><span class="pln"> compareHist</span><span class="pun">(</span><span class="pln">hist</span><span class="pun">,</span><span class="pln"> histB</span><span class="pun">,</span><span class="pln"> CV_COMP_CORREL</span><span class="pun">);</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">teste </span><span class="pun">&lt;</span><span class="pln"> </span><span class="lit">0.993</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"Movimento Detectado"</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="com">//Aqui o frameA recebe o frame atual da camera e calcula o histograma para a proxima iteração.</span><span class="pln">
		cap </span><span class="pun">&gt;&gt;</span><span class="pln"> frameA</span><span class="pun">;</span><span class="pln">
		cvtColor</span><span class="pun">(</span><span class="pln">frameA</span><span class="pun">,</span><span class="pln"> frameA</span><span class="pun">,</span><span class="pln"> CV_BGR2GRAY</span><span class="pun">);</span><span class="pln">
		calcHist</span><span class="pun">(&amp;</span><span class="pln">frameA</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(),</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln">
			</span><span class="pun">&amp;</span><span class="pln">nbins</span><span class="pun">,</span><span class="pln"> </span><span class="pun">&amp;</span><span class="pln">histrange</span><span class="pun">,</span><span class="pln">
			uniform</span><span class="pun">,</span><span class="pln"> acummulate</span><span class="pun">);</span><span class="pln">
		normalize</span><span class="pun">(</span><span class="pln">hist</span><span class="pun">,</span><span class="pln"> hist</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> histImg</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> NORM_MINMAX</span><span class="pun">,</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">());</span><span class="pln">
		imshow</span><span class="pun">(</span><span class="str">"image"</span><span class="pun">,</span><span class="pln"> frameB</span><span class="pun">);</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">waitKey</span><span class="pun">(</span><span class="lit">30</span><span class="pun">)</span><span class="pln"> </span><span class="pun">&gt;=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></mat></code>
</pre>
<p></p>
<h2>Atividade 4 - Laplaciano do Gaussiano</h2>
<p>
Utilizando o programa filtroespacial.cpp como base.<br>
Imagem Utilizada:<br>
<img src="\Nova pasta\carro2.jpg" alt="Um carro" style="width:35%"><br>
Imagem de saída do programa com o filtro laplaciano:<br>
<img src="\Nova pasta\laplaciano.jpg" alt="Um carro" style="width:35%"><br>
Imagem de saída do programa com o filtro laplaciano do gaussiano:<br>
<img src="\Nova pasta\lapgauss.jpg" alt="Um carro" style="width:35%"><br>
Podemos observar um melhor detalhamento das bordas dos objetos na imagem.<br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">void</span><span class="pln"> printmask</span><span class="pun">(</span><span class="typ">Mat</span><span class="pln"> </span><span class="pun">&amp;</span><span class="pln">m</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> m</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">height</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> m</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">width</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			cout </span><span class="pun">&lt;&lt;</span><span class="pln"> m</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">","</span><span class="pun">;</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		cout </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

</span><span class="kwd">void</span><span class="pln"> menu</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"\npressione a tecla para ativar o filtro: \n"</span><span class="pln">
		</span><span class="str">"a - calcular modulo\n"</span><span class="pln">
		</span><span class="str">"m - media\n"</span><span class="pln">
		</span><span class="str">"g - gauss\n"</span><span class="pln">
		</span><span class="str">"v - vertical\n"</span><span class="pln">
		</span><span class="str">"h - horizontal\n"</span><span class="pln">
		</span><span class="str">"l - laplaciano\n"</span><span class="pln">
		</span><span class="str">"k - laplgauss\n"</span><span class="pln">
		</span><span class="str">"esc - sair\n"</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> argvc</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">char</span><span class="pun">**</span><span class="pln"> argv</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">VideoCapture</span><span class="pln"> video</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> media</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> gauss</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">2</span><span class="pun">,</span><span class="lit">4</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> horizontal</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">-</span><span class="lit">2</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> vertical</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,-</span><span class="lit">2</span><span class="pun">,-</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> laplacian</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,-</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="lit">4</span><span class="pun">,-</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">0</span><span class="pun">,-</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pln"> </span><span class="pun">};</span><span class="pln">
	</span><span class="com">//Aqui é criado a mascara 5x5 (matriz) do filtro laplaciano do gaussiano.</span><span class="pln">
	</span><span class="kwd">float</span><span class="pln"> laplgauss</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		 </span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		</span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,-</span><span class="lit">16</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
		 </span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		 </span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">};</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> cap </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">);</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln">  frame</span><span class="pun">,</span><span class="pln"> frame32f</span><span class="pun">,</span><span class="pln"> frameFiltered</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> mask</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">),</span><span class="pln"> mask1</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> result</span><span class="pun">,</span><span class="pln"> result1</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">double</span><span class="pln"> width</span><span class="pun">,</span><span class="pln"> height</span><span class="pun">,</span><span class="pln"> min</span><span class="pun">,</span><span class="pln"> max</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> absolut</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">char</span><span class="pln"> key</span><span class="pun">;</span><span class="pln">

	width </span><span class="pun">=</span><span class="pln"> cap</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">;</span><span class="pln">
	height </span><span class="pun">=</span><span class="pln"> cap</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">;</span><span class="pln">
	std</span><span class="pun">::</span><span class="pln">cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"largura="</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> width </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"\n"</span><span class="pun">;;</span><span class="pln">
	std</span><span class="pun">::</span><span class="pln">cout </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"altura ="</span><span class="pln"> </span><span class="pun">&lt;&lt;</span><span class="pln"> height </span><span class="pun">&lt;&lt;</span><span class="pln"> </span><span class="str">"\n"</span><span class="pun">;;</span><span class="pln">

	namedWindow</span><span class="pun">(</span><span class="str">"filtroespacial"</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">);</span><span class="pln">

	mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> media</span><span class="pun">);</span><span class="pln">
	scaleAdd</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> </span><span class="lit">9.0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">),</span><span class="pln"> mask1</span><span class="pun">);</span><span class="pln">
	swap</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">,</span><span class="pln"> mask1</span><span class="pun">);</span><span class="pln">
	absolut </span><span class="pun">=</span><span class="pln"> </span><span class="lit">1</span><span class="pun">;</span><span class="pln"> </span><span class="com">// calcs abs of the image</span><span class="pln">

	menu</span><span class="pun">();</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(;;)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		cvtColor</span><span class="pun">(</span><span class="pln">cap</span><span class="pun">,</span><span class="pln"> frame</span><span class="pun">,</span><span class="pln"> CV_BGR2GRAY</span><span class="pun">);</span><span class="pln">
		flip</span><span class="pun">(</span><span class="pln">frame</span><span class="pun">,</span><span class="pln"> frame</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">);</span><span class="pln">
		imshow</span><span class="pun">(</span><span class="str">"original"</span><span class="pun">,</span><span class="pln"> frame</span><span class="pun">);</span><span class="pln">
		frame</span><span class="pun">.</span><span class="pln">convertTo</span><span class="pun">(</span><span class="pln">frame32f</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">);</span><span class="pln">
		filter2D</span><span class="pun">(</span><span class="pln">frame32f</span><span class="pun">,</span><span class="pln"> frameFiltered</span><span class="pun">,</span><span class="pln"> frame32f</span><span class="pun">.</span><span class="pln">depth</span><span class="pun">(),</span><span class="pln"> mask</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Point</span><span class="pun">(</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">),</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">absolut</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			frameFiltered </span><span class="pun">=</span><span class="pln"> abs</span><span class="pun">(</span><span class="pln">frameFiltered</span><span class="pun">);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		frameFiltered</span><span class="pun">.</span><span class="pln">convertTo</span><span class="pun">(</span><span class="pln">result</span><span class="pun">,</span><span class="pln"> CV_8U</span><span class="pun">);</span><span class="pln">
		imshow</span><span class="pun">(</span><span class="str">"filtroespacial"</span><span class="pun">,</span><span class="pln"> result</span><span class="pun">);</span><span class="pln">
		key </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">char</span><span class="pun">)</span><span class="pln">waitKey</span><span class="pun">(</span><span class="lit">10</span><span class="pun">);</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">key </span><span class="pun">==</span><span class="pln"> </span><span class="lit">27</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">break</span><span class="pun">;</span><span class="pln"> </span><span class="com">// esc pressed!</span><span class="pln">
		</span><span class="kwd">switch</span><span class="pln"> </span><span class="pun">(</span><span class="pln">key</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'a'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			absolut </span><span class="pun">=</span><span class="pln"> </span><span class="pun">!</span><span class="pln">absolut</span><span class="pun">;</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'m'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> media</span><span class="pun">);</span><span class="pln">
			scaleAdd</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> </span><span class="lit">9.0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">),</span><span class="pln"> mask1</span><span class="pun">);</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> mask1</span><span class="pun">;</span><span class="pln">
			printmask</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">);</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'g'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> gauss</span><span class="pun">);</span><span class="pln">
			scaleAdd</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> </span><span class="lit">16.0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">),</span><span class="pln"> mask1</span><span class="pun">);</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> mask1</span><span class="pun">;</span><span class="pln">
			printmask</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">);</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'h'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> horizontal</span><span class="pun">);</span><span class="pln">
			printmask</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">);</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'v'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> vertical</span><span class="pun">);</span><span class="pln">
			printmask</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">);</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'l'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> laplacian</span><span class="pun">);</span><span class="pln">
			printmask</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">);</span><span class="pln">
			</span><span class="com">//Criamos a imagem do laplaciano</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"laplaciano.jpg"</span><span class="pun">,</span><span class="pln"> frameFiltered</span><span class="pun">);</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
			</span><span class="com">//Aqui é atribuido a letra k para fazer o Laplaciano do Gaussiano</span><span class="pln">
		</span><span class="kwd">case</span><span class="pln"> </span><span class="str">'k'</span><span class="pun">:</span><span class="pln">
			menu</span><span class="pun">();</span><span class="pln">
			mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">5</span><span class="pun">,</span><span class="pln"> </span><span class="lit">5</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> laplgauss</span><span class="pun">);</span><span class="pln">
			printmask</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">);</span><span class="pln">
			</span><span class="com">//Criamos a imagem do laplaciano do gaussiano</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"lapgauss.jpg"</span><span class="pun">,</span><span class="pln"> frameFiltered</span><span class="pun">);</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="kwd">default</span><span class="pun">:</span><span class="pln">
			</span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></code>
</pre>
<p></p>
<h2>Atividade 5 - Tilt-shift em Imagem e Vídeo</h2>
<h3>5.1 - Imagem</h3>
<p>
Utilizando o programa addweighted.cpp como base.<br>
Imagem Utilizada:<br>
<img src="\Nova pasta\bridge.jpg" alt="Uma ponte" style="width:35%"><br>
Resuldado da saída do programa:<br>
<img src="\Nova pasta\tiltshifted.jpg" alt="Uma ponte" style="width:35%"><br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;cmath&gt;</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> pslider </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">int</span><span class="pln"> aslider </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">int</span><span class="pln"> dslider </span><span class="pun">=</span><span class="pln"> </span><span class="lit">1</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">int</span><span class="pln"> dslidermax </span><span class="pun">=</span><span class="pln"> </span><span class="lit">100</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">double</span><span class="pln"> l1</span><span class="pun">,</span><span class="pln"> l2</span><span class="pun">,</span><span class="pln">alfa</span><span class="pun">;</span><span class="pln">
</span><span class="com">//Criamos a mascara para o borramento da imagem</span><span class="pln">
</span><span class="kwd">float</span><span class="pln"> gauss</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pun">,</span><span class="pln">
</span><span class="lit">2</span><span class="pun">,</span><span class="lit">4</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="pln">
</span><span class="lit">1</span><span class="pun">,</span><span class="lit">2</span><span class="pun">,</span><span class="lit">1</span><span class="pln"> </span><span class="pun">};</span><span class="pln">


</span><span class="kwd">void</span><span class="pln"> on_trackbar_a</span><span class="pun">(</span><span class="kwd">int</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">void</span><span class="pun">*)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	l1 </span><span class="pun">=</span><span class="pln"> aslider </span><span class="pun">-</span><span class="pln"> pslider</span><span class="pun">;</span><span class="pln">
	l2 </span><span class="pun">=</span><span class="pln"> aslider </span><span class="pun">+</span><span class="pln"> pslider</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

</span><span class="kwd">void</span><span class="pln"> on_trackbar_p</span><span class="pun">(</span><span class="kwd">int</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">void</span><span class="pun">*)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	l1 </span><span class="pun">=</span><span class="pln"> aslider </span><span class="pun">-</span><span class="pln"> pslider</span><span class="pun">;</span><span class="pln">
	l2 </span><span class="pun">=</span><span class="pln"> aslider </span><span class="pun">+</span><span class="pln"> pslider</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

</span><span class="typ">Mat</span><span class="pln"> image1</span><span class="pun">,</span><span class="pln"> image2</span><span class="pun">,</span><span class="pln"> blended</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">char</span><span class="pln"> </span><span class="typ">TrackbarName</span><span class="pun">[</span><span class="lit">50</span><span class="pun">];</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	image1 </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da IMAGEM"</span><span class="pun">);</span><span class="pln">
	image1</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">image2</span><span class="pun">);</span><span class="pln">
	image2</span><span class="pun">.</span><span class="pln">convertTo</span><span class="pun">(</span><span class="pln">image2</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">);</span><span class="pln">

	</span><span class="typ">Mat</span><span class="pln"> mask </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">,</span><span class="pln"> gauss</span><span class="pun">);</span><span class="pln">
	scaleAdd</span><span class="pun">(</span><span class="pln">mask</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> </span><span class="lit">16.0</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="lit">3</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">),</span><span class="pln"> mask</span><span class="pun">);</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> </span><span class="lit">10</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		filter2D</span><span class="pun">(</span><span class="pln">image2</span><span class="pun">,</span><span class="pln"> image2</span><span class="pun">,</span><span class="pln"> image2</span><span class="pun">.</span><span class="pln">depth</span><span class="pun">(),</span><span class="pln"> mask</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Point</span><span class="pun">(</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">),</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	image2</span><span class="pun">.</span><span class="pln">convertTo</span><span class="pun">(</span><span class="pln">image2</span><span class="pun">,</span><span class="pln"> CV_8U</span><span class="pun">);</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> image1</span><span class="pun">.</span><span class="pln">rows </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	cout </span><span class="pun">&lt;&lt;</span><span class="pln"> image1</span><span class="pun">.</span><span class="pln">cols </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
	namedWindow</span><span class="pun">(</span><span class="str">"addweighted"</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">);</span><span class="pln">
	sprintf_s</span><span class="pun">(</span><span class="typ">TrackbarName</span><span class="pun">,</span><span class="pln"> </span><span class="str">"Altura %d"</span><span class="pun">,</span><span class="pln"> image1</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">);</span><span class="pln">
	createTrackbar</span><span class="pun">(</span><span class="typ">TrackbarName</span><span class="pun">,</span><span class="pln"> </span><span class="str">"addweighted"</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">&amp;</span><span class="pln">aslider</span><span class="pun">,</span><span class="pln">
		image1</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln">
		on_trackbar_a</span><span class="pun">);</span><span class="pln">
	on_trackbar_a</span><span class="pun">(</span><span class="pln">aslider</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">

	sprintf_s</span><span class="pun">(</span><span class="typ">TrackbarName</span><span class="pun">,</span><span class="pln"> </span><span class="str">"Posição %d"</span><span class="pun">,</span><span class="pln"> image1</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">);</span><span class="pln">
	createTrackbar</span><span class="pun">(</span><span class="typ">TrackbarName</span><span class="pun">,</span><span class="pln"> </span><span class="str">"addweighted"</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">&amp;</span><span class="pln">pslider</span><span class="pun">,</span><span class="pln">
		image1</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln">
		on_trackbar_p</span><span class="pun">);</span><span class="pln">
	on_trackbar_p</span><span class="pun">(</span><span class="pln">pslider</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">

	sprintf_s</span><span class="pun">(</span><span class="typ">TrackbarName</span><span class="pun">,</span><span class="pln"> </span><span class="str">"Decaimento %d"</span><span class="pun">,</span><span class="pln"> dslidermax</span><span class="pun">);</span><span class="pln">
	createTrackbar</span><span class="pun">(</span><span class="typ">TrackbarName</span><span class="pun">,</span><span class="pln"> </span><span class="str">"addweighted"</span><span class="pun">,</span><span class="pln">
		</span><span class="pun">&amp;</span><span class="pln">dslider</span><span class="pun">,</span><span class="pln">
		dslidermax</span><span class="pun">);</span><span class="pln">

	blended </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="pln">image1</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> image1</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">,</span><span class="pln"> CV_8UC3</span><span class="pun">);</span><span class="pln">
	</span><span class="kwd">while</span><span class="pln"> </span><span class="pun">(</span><span class="lit">1</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> image1</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			</span><span class="kwd">double</span><span class="pln"> d </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">double</span><span class="pun">)</span><span class="pln">dslider</span><span class="pun">;</span><span class="pln">
			alfa </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0.5</span><span class="pun">*(</span><span class="pln">tanh</span><span class="pun">((</span><span class="pln">i </span><span class="pun">-</span><span class="pln"> l1</span><span class="pun">)</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> d</span><span class="pun">)</span><span class="pln"> </span><span class="pun">-</span><span class="pln"> tanh</span><span class="pun">((</span><span class="pln">i </span><span class="pun">-</span><span class="pln"> l2</span><span class="pun">)</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> d</span><span class="pun">));</span><span class="pln">
			addWeighted</span><span class="pun">(</span><span class="pln">image1</span><span class="pun">.</span><span class="pln">row</span><span class="pun">(</span><span class="pln">i</span><span class="pun">),</span><span class="pln"> alfa</span><span class="pun">,</span><span class="pln"> image2</span><span class="pun">.</span><span class="pln">row</span><span class="pun">(</span><span class="pln">i</span><span class="pun">),</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="pun">-</span><span class="pln"> alfa</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> blended</span><span class="pun">.</span><span class="pln">row</span><span class="pun">(</span><span class="pln">i</span><span class="pun">));</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		imshow</span><span class="pun">(</span><span class="str">"addweighted"</span><span class="pun">,</span><span class="pln"> blended</span><span class="pun">);</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">waitKey</span><span class="pun">(</span><span class="lit">30</span><span class="pun">)</span><span class="pln"> </span><span class="pun">==</span><span class="pln"> </span><span class="lit">27</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">break</span><span class="pun">;</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	imwrite</span><span class="pun">(</span><span class="str">"tiltshifted.jpg"</span><span class="pun">,</span><span class="pln"> blended</span><span class="pun">);</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></code>
</pre>
<p></p>
<h3>5.2 - Vídeo</h3>
<p>
</p>
<h2>Atividade 6 - Filtro Homomórfico</h2>
<p>
Utilizando os programas exemplos/dft.cpp como base.<br>

Imagem Utilizada:<br>
<img src="\Nova pasta\maliluminada2.jpg" alt="Uma rua" style="width:35%"><br>
Resuldado da saída do programa:<br>
<img src="\Nova pasta\filtradahm.JPG" alt="Uma rua" style="width:35%"><br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/imgproc/imgproc.hpp&gt;</span><span class="pln">

</span><span class="com">#define</span><span class="pln"> RADIUS </span><span class="lit">20</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">

</span><span class="com">// troca os quadrantes da imagem da DFT</span><span class="pln">
</span><span class="kwd">void</span><span class="pln"> deslocaDFT</span><span class="pun">(</span><span class="typ">Mat</span><span class="pun">&amp;</span><span class="pln"> image</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> tmp</span><span class="pun">,</span><span class="pln"> A</span><span class="pun">,</span><span class="pln"> B</span><span class="pun">,</span><span class="pln"> C</span><span class="pun">,</span><span class="pln"> D</span><span class="pun">;</span><span class="pln">

	</span><span class="com">// se a imagem tiver tamanho impar, recorta a regiao para</span><span class="pln">
	</span><span class="com">// evitar cópias de tamanho desigual</span><span class="pln">
	image </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">cols </span><span class="pun">&amp;</span><span class="pln"> </span><span class="pun">-</span><span class="lit">2</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">rows </span><span class="pun">&amp;</span><span class="pln"> </span><span class="pun">-</span><span class="lit">2</span><span class="pun">));</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> cx </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">cols </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> cy </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">rows </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2</span><span class="pun">;</span><span class="pln">

	</span><span class="com">// reorganiza os quadrantes da transformada</span><span class="pln">
	</span><span class="com">// A B   -&gt;  D C</span><span class="pln">
	</span><span class="com">// C D       B A</span><span class="pln">
	A </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> cx</span><span class="pun">,</span><span class="pln"> cy</span><span class="pun">));</span><span class="pln">
	B </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="pln">cx</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> cx</span><span class="pun">,</span><span class="pln"> cy</span><span class="pun">));</span><span class="pln">
	C </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> cy</span><span class="pun">,</span><span class="pln"> cx</span><span class="pun">,</span><span class="pln"> cy</span><span class="pun">));</span><span class="pln">
	D </span><span class="pun">=</span><span class="pln"> image</span><span class="pun">(</span><span class="typ">Rect</span><span class="pun">(</span><span class="pln">cx</span><span class="pun">,</span><span class="pln"> cy</span><span class="pun">,</span><span class="pln"> cx</span><span class="pun">,</span><span class="pln"> cy</span><span class="pun">));</span><span class="pln">

	</span><span class="com">// A &lt;-&gt; D</span><span class="pln">
	A</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">tmp</span><span class="pun">);</span><span class="pln">  D</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">A</span><span class="pun">);</span><span class="pln">  tmp</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">D</span><span class="pun">);</span><span class="pln">

	</span><span class="com">// C &lt;-&gt; B</span><span class="pln">
	C</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">tmp</span><span class="pun">);</span><span class="pln">  B</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">C</span><span class="pun">);</span><span class="pln">  tmp</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="pln">B</span><span class="pun">);</span><span class="pln">
</span><span class="pun">}</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> imaginaryInput</span><span class="pun">,</span><span class="pln"> complexImage</span><span class="pun">,</span><span class="pln"> multsp</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> padded</span><span class="pun">,</span><span class="pln"> filter</span><span class="pun">,</span><span class="pln"> mag</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> imagegray</span><span class="pun">,</span><span class="pln"> tmp</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat_</span><float><span class="pln"> realInput</span><span class="pun">,</span><span class="pln"> zeros</span><span class="pun">;</span><span class="pln">
	vector</span><mat><span class="pln"> planos</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> image </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da imagem"</span><span class="pun">,</span><span class="pln">CV_LOAD_IMAGE_GRAYSCALE</span><span class="pun">);</span><span class="pln">

	</span><span class="com">// valores ideais dos tamanhos da imagem</span><span class="pln">
	</span><span class="com">// para calculo da DFT</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> dft_M</span><span class="pun">,</span><span class="pln"> dft_N</span><span class="pun">;</span><span class="pln">

	</span><span class="com">// identifica os tamanhos otimos para</span><span class="pln">
	</span><span class="com">// calculo do FFT</span><span class="pln">
	dft_M </span><span class="pun">=</span><span class="pln"> getOptimalDFTSize</span><span class="pun">(</span><span class="pln">image</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">);</span><span class="pln">
	dft_N </span><span class="pun">=</span><span class="pln"> getOptimalDFTSize</span><span class="pun">(</span><span class="pln">image</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">);</span><span class="pln">

	</span><span class="com">// realiza o padding da imagem</span><span class="pln">
	copyMakeBorder</span><span class="pun">(</span><span class="pln">image</span><span class="pun">,</span><span class="pln"> padded</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		dft_M </span><span class="pun">-</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln">
		dft_N </span><span class="pun">-</span><span class="pln"> image</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">,</span><span class="pln">
		BORDER_CONSTANT</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Scalar</span><span class="pun">::</span><span class="pln">all</span><span class="pun">(</span><span class="lit">0</span><span class="pun">));</span><span class="pln">

	</span><span class="com">// parte imaginaria da matriz complexa (preenchida com zeros)</span><span class="pln">
	zeros </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat_</span><span class="str">&lt;float&gt;</span><span class="pun">::</span><span class="pln">zeros</span><span class="pun">(</span><span class="pln">padded</span><span class="pun">.</span><span class="pln">size</span><span class="pun">());</span><span class="pln">

	</span><span class="com">// prepara a matriz complexa para ser preenchida</span><span class="pln">
	complexImage </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="pln">padded</span><span class="pun">.</span><span class="pln">size</span><span class="pun">(),</span><span class="pln"> CV_32FC2</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Scalar</span><span class="pun">(</span><span class="lit">0</span><span class="pun">));</span><span class="pln">

	</span><span class="com">// a função de transferência (filtro frequencial) deve ter o</span><span class="pln">
	</span><span class="com">// mesmo tamanho e tipo da matriz complexa</span><span class="pln">
	filter </span><span class="pun">=</span><span class="pln"> complexImage</span><span class="pun">.</span><span class="pln">clone</span><span class="pun">();</span><span class="pln">

	</span><span class="com">// cria uma matriz temporária para criar as componentes real</span><span class="pln">
	</span><span class="com">// e imaginaria do filtro ideal</span><span class="pln">
	tmp </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat</span><span class="pun">(</span><span class="pln">dft_M</span><span class="pun">,</span><span class="pln"> dft_N</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">);</span><span class="pln">

	</span><span class="kwd">float</span><span class="pln"> gamah</span><span class="pun">,</span><span class="pln"> gamal</span><span class="pun">,</span><span class="pln"> c</span><span class="pun">,</span><span class="pln"> D0</span><span class="pun">;</span><span class="pln">
	gamah </span><span class="pun">=</span><span class="pln"> </span><span class="lit">200</span><span class="pun">;</span><span class="pln">
	gamal </span><span class="pun">=</span><span class="pln"> </span><span class="lit">100</span><span class="pun">;</span><span class="pln">
	c </span><span class="pun">=</span><span class="pln"> </span><span class="lit">20</span><span class="pun">;</span><span class="pln">
	D0 </span><span class="pun">=</span><span class="pln"> </span><span class="lit">40</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> M </span><span class="pun">=</span><span class="pln"> dft_M</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> N </span><span class="pun">=</span><span class="pln"> dft_N</span><span class="pun">;</span><span class="pln">

	</span><span class="com">//filtro homomórfico</span><span class="pln">
	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> dft_M</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> dft_N</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			tmp</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln"> j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="pln">gamah </span><span class="pun">-</span><span class="pln"> gamal</span><span class="pun">)*(</span><span class="lit">1.0</span><span class="pln"> </span><span class="pun">-</span><span class="pln"> exp</span><span class="pun">(-</span><span class="lit">1.0</span><span class="pun">*(</span><span class="kwd">float</span><span class="pun">)</span><span class="pln">c</span><span class="pun">*((((</span><span class="kwd">float</span><span class="pun">)</span><span class="pln">i </span><span class="pun">-</span><span class="pln"> M </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2.0</span><span class="pun">)*((</span><span class="kwd">float</span><span class="pun">)</span><span class="pln">i </span><span class="pun">-</span><span class="pln"> M </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2.0</span><span class="pun">)</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> </span><span class="pun">((</span><span class="kwd">float</span><span class="pun">)</span><span class="pln">j </span><span class="pun">-</span><span class="pln"> N </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2.0</span><span class="pun">)*((</span><span class="kwd">float</span><span class="pun">)</span><span class="pln">j </span><span class="pun">-</span><span class="pln"> N </span><span class="pun">/</span><span class="pln"> </span><span class="lit">2.0</span><span class="pun">))</span><span class="pln"> </span><span class="pun">/</span><span class="pln"> </span><span class="pun">(</span><span class="pln">D0</span><span class="pun">*</span><span class="pln">D0</span><span class="pun">))))</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> gamal</span><span class="pun">;</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
	
	</span><span class="com">// cria a matriz com as componentes do filtro e junta</span><span class="pln">
	</span><span class="com">// ambas em uma matriz multicanal complexa</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> comps</span><span class="pun">[]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">{</span><span class="pln"> tmp</span><span class="pun">,</span><span class="pln"> tmp </span><span class="pun">};</span><span class="pln">
	merge</span><span class="pun">(</span><span class="pln">comps</span><span class="pun">,</span><span class="pln"> </span><span class="lit">2</span><span class="pun">,</span><span class="pln"> filter</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// limpa o array de matrizes que vao compor a</span><span class="pln">
		</span><span class="com">// imagem complexa</span><span class="pln">
		planos</span><span class="pun">.</span><span class="pln">clear</span><span class="pun">();</span><span class="pln">
		</span><span class="com">// cria a compoente real</span><span class="pln">
		realInput </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Mat_</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">padded</span><span class="pun">);</span><span class="pln">
		</span><span class="com">// insere as duas componentes no array de matrizes</span><span class="pln">
		planos</span><span class="pun">.</span><span class="pln">push_back</span><span class="pun">(</span><span class="pln">realInput</span><span class="pun">);</span><span class="pln">
		planos</span><span class="pun">.</span><span class="pln">push_back</span><span class="pun">(</span><span class="pln">zeros</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// combina o array de matrizes em uma unica</span><span class="pln">
		</span><span class="com">// componente complexa</span><span class="pln">
		merge</span><span class="pun">(</span><span class="pln">planos</span><span class="pun">,</span><span class="pln"> complexImage</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// calcula o dft</span><span class="pln">
		dft</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">,</span><span class="pln"> complexImage</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// realiza a troca de quadrantes</span><span class="pln">
		deslocaDFT</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// aplica o filtro frequencial</span><span class="pln">
		mulSpectrums</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">,</span><span class="pln"> filter</span><span class="pun">,</span><span class="pln"> complexImage</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// limpa o array de planos</span><span class="pln">
		planos</span><span class="pun">.</span><span class="pln">clear</span><span class="pun">();</span><span class="pln">
		</span><span class="com">// separa as partes real e imaginaria para modifica-las</span><span class="pln">
		split</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">,</span><span class="pln"> planos</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// recompoe os planos em uma unica matriz complexa</span><span class="pln">
		merge</span><span class="pun">(</span><span class="pln">planos</span><span class="pun">,</span><span class="pln"> complexImage</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// troca novamente os quadrantes</span><span class="pln">
		deslocaDFT</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">);</span><span class="pln">

		cout </span><span class="pun">&lt;&lt;</span><span class="pln"> complexImage</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">height </span><span class="pun">&lt;&lt;</span><span class="pln"> endl</span><span class="pun">;</span><span class="pln">
		</span><span class="com">// calcula a DFT inversa</span><span class="pln">
		idft</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">,</span><span class="pln"> complexImage</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// limpa o array de planos</span><span class="pln">
		planos</span><span class="pun">.</span><span class="pln">clear</span><span class="pun">();</span><span class="pln">

		</span><span class="com">// separa as partes real e imaginaria da</span><span class="pln">
		</span><span class="com">// imagem filtrada</span><span class="pln">
		split</span><span class="pun">(</span><span class="pln">complexImage</span><span class="pun">,</span><span class="pln"> planos</span><span class="pun">);</span><span class="pln">

		</span><span class="com">// normaliza a parte real para exibicao</span><span class="pln">
		normalize</span><span class="pun">(</span><span class="pln">planos</span><span class="pun">[</span><span class="lit">0</span><span class="pun">],</span><span class="pln"> planos</span><span class="pun">[</span><span class="lit">0</span><span class="pun">],</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">,</span><span class="pln"> CV_MINMAX</span><span class="pun">);</span><span class="pln">
		imshow</span><span class="pun">(</span><span class="str">"original"</span><span class="pun">,</span><span class="pln"> image</span><span class="pun">);</span><span class="pln">
		imshow</span><span class="pun">(</span><span class="str">"filtrada"</span><span class="pun">,</span><span class="pln"> planos</span><span class="pun">[</span><span class="lit">0</span><span class="pun">]);</span><span class="pln">
		waitKey</span><span class="pun">();</span><span class="pln">
	</span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></mat></float></code>
</pre>
<p></p>
<h2>Atividade 7 - Canny e a arte do Pontilhismo</h2>
<p>
Utilizando os programas canny.cpp e pontilhismo.cpp como base.<br>

Imagem Utilizada:<br>
<img src="\Nova pasta\carro.jpeg" alt="Um carro" style="width:35%"><br>
Resuldado da saída do programa:<br>
<img src="\Nova pasta\pontos.jpg" alt="Um carro" style="width:35%"><br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;fstream&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iomanip&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;vector&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;algorithm&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;numeric&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;ctime&gt;</span><span class="pln">
  </span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;cstdlib&gt;</span><span class="pln">

  </span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">
  </span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">


  </span><span class="com">#define</span><span class="pln"> STEP </span><span class="lit">5</span><span class="pln">
  </span><span class="com">#define</span><span class="pln"> JITTER </span><span class="lit">3</span><span class="pln">
  </span><span class="com">#define</span><span class="pln"> RAIO </span><span class="lit">2</span><span class="pln">

  </span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> argc</span><span class="pun">,</span><span class="pln"> </span><span class="kwd">char</span><span class="pun">**</span><span class="pln"> argv</span><span class="pun">){</span><span class="pln">
  </span><span class="typ">Mat</span><span class="pln"> </span><span class="typ">Original</span><span class="pun">,</span><span class="pln"> borderOriginalImage</span><span class="pun">;</span><span class="pln">
  </span><span class="typ">Mat</span><span class="pln"> </span><span class="typ">Pontilhismo</span><span class="pun">;</span><span class="pln">
  </span><span class="kwd">int</span><span class="pln"> x</span><span class="pun">,</span><span class="pln"> y</span><span class="pun">,</span><span class="pln"> width</span><span class="pun">,</span><span class="pln"> height</span><span class="pun">,</span><span class="pln"> gray</span><span class="pun">;</span><span class="pln">

  vector</span><span class="str">&lt;int&gt;</span><span class="pln"> yrange</span><span class="pun">;</span><span class="pln">
  vector</span><span class="str">&lt;int&gt;</span><span class="pln"> xrange</span><span class="pun">;</span><span class="pln">

  srand</span><span class="pun">(</span><span class="pln">time</span><span class="pun">(</span><span class="lit">0</span><span class="pun">));</span><span class="pln">

  </span><span class="typ">Original</span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"DIR da imagem"</span><span class="pln"> </span><span class="pun">,</span><span class="pln">CV_LOAD_IMAGE_GRAYSCALE</span><span class="pun">);</span><span class="pln">

  width </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Original</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">width</span><span class="pun">;</span><span class="pln">
  height </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Original</span><span class="pun">.</span><span class="pln">size</span><span class="pun">().</span><span class="pln">height</span><span class="pun">;</span><span class="pln">
  xrange</span><span class="pun">.</span><span class="pln">resize</span><span class="pun">(</span><span class="pln">height</span><span class="pun">/</span><span class="pln">STEP</span><span class="pun">);</span><span class="pln">
  yrange</span><span class="pun">.</span><span class="pln">resize</span><span class="pun">(</span><span class="pln">width</span><span class="pun">/</span><span class="pln">STEP</span><span class="pun">);</span><span class="pln">
  iota</span><span class="pun">(</span><span class="pln">xrange</span><span class="pun">.</span><span class="kwd">begin</span><span class="pun">(),</span><span class="pln"> xrange</span><span class="pun">.</span><span class="kwd">end</span><span class="pun">(),</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
  iota</span><span class="pun">(</span><span class="pln">yrange</span><span class="pun">.</span><span class="kwd">begin</span><span class="pun">(),</span><span class="pln"> yrange</span><span class="pun">.</span><span class="kwd">end</span><span class="pun">(),</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">

  </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">uint</span><span class="pln"> i</span><span class="pun">=</span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">&lt;</span><span class="pln">xrange</span><span class="pun">.</span><span class="pln">size</span><span class="pun">();</span><span class="pln"> i</span><span class="pun">++){</span><span class="pln">
    xrange</span><span class="pun">[</span><span class="pln">i</span><span class="pun">]=</span><span class="pln"> xrange</span><span class="pun">[</span><span class="pln">i</span><span class="pun">]*</span><span class="pln">STEP</span><span class="pun">+</span><span class="pln">STEP</span><span class="pun">/</span><span class="lit">2</span><span class="pun">;</span><span class="pln">
  </span><span class="pun">}</span><span class="pln">

  </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">uint</span><span class="pln"> i</span><span class="pun">=</span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">&lt;</span><span class="pln">yrange</span><span class="pun">.</span><span class="pln">size</span><span class="pun">();</span><span class="pln"> i</span><span class="pun">++){</span><span class="pln">
    yrange</span><span class="pun">[</span><span class="pln">i</span><span class="pun">]=</span><span class="pln"> yrange</span><span class="pun">[</span><span class="pln">i</span><span class="pun">]*</span><span class="pln">STEP</span><span class="pun">+</span><span class="pln">STEP</span><span class="pun">/</span><span class="lit">2</span><span class="pun">;</span><span class="pln">
  </span><span class="pun">}</span><span class="pln">

  </span><span class="typ">Original</span><span class="pun">.</span><span class="pln">copyTo</span><span class="pun">(</span><span class="typ">Pontilhismo</span><span class="pun">);</span><span class="pln">

  </span><span class="com">//Executa o pontilhismo;</span><span class="pln">
  </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">auto</span><span class="pln"> i </span><span class="pun">:</span><span class="pln"> xrange</span><span class="pun">){</span><span class="pln">
    random_shuffle</span><span class="pun">(</span><span class="pln">yrange</span><span class="pun">.</span><span class="kwd">begin</span><span class="pun">(),</span><span class="pln"> yrange</span><span class="pun">.</span><span class="kwd">end</span><span class="pun">());</span><span class="pln">
    </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">auto</span><span class="pln"> j </span><span class="pun">:</span><span class="pln"> yrange</span><span class="pun">){</span><span class="pln">
      x </span><span class="pun">=</span><span class="pln"> i</span><span class="pun">+</span><span class="pln">rand</span><span class="pun">()%(</span><span class="lit">2</span><span class="pun">*</span><span class="pln">JITTER</span><span class="pun">)-</span><span class="pln">JITTER</span><span class="pun">+</span><span class="lit">1</span><span class="pun">;</span><span class="pln">
      y </span><span class="pun">=</span><span class="pln"> j</span><span class="pun">+</span><span class="pln">rand</span><span class="pun">()%(</span><span class="lit">2</span><span class="pun">*</span><span class="pln">JITTER</span><span class="pun">)-</span><span class="pln">JITTER</span><span class="pun">+</span><span class="lit">1</span><span class="pun">;</span><span class="pln">
      gray </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Original</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;uchar&gt;</span><span class="pun">(</span><span class="pln">x</span><span class="pun">,</span><span class="pln">y</span><span class="pun">);</span><span class="pln">
      circle</span><span class="pun">(</span><span class="typ">Pontilhismo</span><span class="pun">,</span><span class="pln"> cv</span><span class="pun">::</span><span class="typ">Point</span><span class="pun">(</span><span class="pln">y</span><span class="pun">,</span><span class="pln">x</span><span class="pun">),</span><span class="pln"> RAIO</span><span class="pun">,</span><span class="pln"> CV_RGB</span><span class="pun">(</span><span class="pln">gray</span><span class="pun">,</span><span class="pln">gray</span><span class="pun">,</span><span class="pln">gray</span><span class="pun">),</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> CV_AA</span><span class="pun">);</span><span class="pln">
    </span><span class="pun">}</span><span class="pln">
  </span><span class="pun">}</span><span class="pln">

  imshow</span><span class="pun">(</span><span class="str">"Imagem Pontilhista"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Pontilhismo</span><span class="pun">);</span><span class="pln">
  imwrite</span><span class="pun">(</span><span class="str">"imagemComPontilhismo.jpg"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Pontilhismo</span><span class="pun">);</span><span class="pln">

   </span><span class="com">//Aplica Canny</span><span class="pln">
   </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> z</span><span class="pun">=</span><span class="lit">0</span><span class="pun">;</span><span class="pln"> z </span><span class="pun">&lt;</span><span class="pln"> </span><span class="lit">5</span><span class="pun">;</span><span class="pln"> z</span><span class="pun">++){</span><span class="pln">
     </span><span class="typ">Canny</span><span class="pun">(</span><span class="typ">Original</span><span class="pun">,</span><span class="pln"> borderOriginalImage</span><span class="pun">,</span><span class="pln"> </span><span class="lit">10</span><span class="pun">*</span><span class="pln">z</span><span class="pun">,</span><span class="pln"> </span><span class="lit">50</span><span class="pun">*</span><span class="pln">z</span><span class="pun">);</span><span class="pln">
     </span><span class="kwd">int</span><span class="pln"> raio </span><span class="pun">=</span><span class="pln"> </span><span class="lit">10</span><span class="pun">-</span><span class="pln">z</span><span class="pun">;</span><span class="pln">

     </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i</span><span class="pun">=</span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> height</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++</span><span class="pln"> </span><span class="pun">){</span><span class="pln">
        </span><span class="kwd">for</span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> j</span><span class="pun">=</span><span class="lit">0</span><span class="pun">;</span><span class="pln"> j </span><span class="pun">&lt;</span><span class="pln"> width</span><span class="pun">;</span><span class="pln"> j</span><span class="pun">++){</span><span class="pln">
           </span><span class="kwd">if</span><span class="pun">(</span><span class="pln">borderOriginalImage</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;uchar&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln">j</span><span class="pun">)</span><span class="pln"> </span><span class="pun">==</span><span class="pln"> </span><span class="lit">255</span><span class="pun">){</span><span class="pln">
              gray </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Original</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;uchar&gt;</span><span class="pun">(</span><span class="pln">i</span><span class="pun">,</span><span class="pln">j</span><span class="pun">);</span><span class="pln">
              circle</span><span class="pun">(</span><span class="typ">Pontilhismo</span><span class="pun">,</span><span class="pln"> cv</span><span class="pun">::</span><span class="typ">Point</span><span class="pun">(</span><span class="pln">j</span><span class="pun">,</span><span class="pln">i</span><span class="pun">),</span><span class="pln"> raio</span><span class="pun">,</span><span class="pln"> CV_RGB</span><span class="pun">(</span><span class="pln">gray</span><span class="pun">,</span><span class="pln">gray</span><span class="pun">,</span><span class="pln">gray</span><span class="pun">),</span><span class="pln"> </span><span class="pun">-</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> CV_AA</span><span class="pun">);</span><span class="pln">
             </span><span class="pun">}</span><span class="pln">
        </span><span class="pun">}</span><span class="pln">
    </span><span class="pun">}</span><span class="pln">


  </span><span class="pun">}</span><span class="pln">
  imshow</span><span class="pun">(</span><span class="str">"Pontilhismo"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Pontilhismo</span><span class="pun">);</span><span class="pln">
  imwrite</span><span class="pun">(</span><span class="str">"imagemComPontilhismo.jpg"</span><span class="pun">,</span><span class="pln"> </span><span class="typ">Pontilhismo</span><span class="pun">);</span><span class="pln">

   waitKey</span><span class="pun">();</span><span class="pln">
  </span><span class="kwd">return</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></code>
</pre>
<p></p>
<h2>Atividade 8 - Kmeans clustering</h2>
<p>
O agrupamento k-means (k-means clustering) é um método de agrupamento que visa dividir n observações em k grupos, no caso do programa utilizado ele agrupa os pixels da imagens em k cores (k grupos) diferentes; com o uso do parâmetro KMEANS_RANDOM_CENTERS no lugar do KMEANS_PP_CENTERS os k grupos são escolhidos aleatoriamente, fazendo várias rodadas podemos ver que a imagem de saída pode variar por causa dos agrupamentos feitos com cores diferentes.<br>
Utilizando o programa kmeans.cpp como base.<br>

Imagem Utilizada:<br>
<img src="\Nova pasta\paisagem.jpg" alt="Uma montanha" style="width:35%"><br>
Resuldado da saída do programa juntos num gif:<br>
<img src="\Nova pasta\clusteredf.gif" alt="Uma montanha" style="width:35%"><br>
Código utilizado:<br>
</p><pre class="prettyprint prettyprinted" style=""><code><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;opencv2/opencv.hpp&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;cstdlib&gt;</span><span class="pln">
</span><span class="com">#include</span><span class="pln"> </span><span class="str">&lt;iostream&gt;</span><span class="pln">

</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> std</span><span class="pun">;</span><span class="pln">
</span><span class="kwd">using</span><span class="pln"> </span><span class="kwd">namespace</span><span class="pln"> cv</span><span class="pun">;</span><span class="pln">

</span><span class="kwd">int</span><span class="pln"> main</span><span class="pun">()</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> nClusters </span><span class="pun">=</span><span class="pln"> </span><span class="lit">6</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> rotulos</span><span class="pun">;</span><span class="pln">
	</span><span class="kwd">int</span><span class="pln"> nRodadas </span><span class="pun">=</span><span class="pln"> </span><span class="lit">1</span><span class="pun">;</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> centros</span><span class="pun">;</span><span class="pln">

	</span><span class="typ">Mat</span><span class="pln"> img </span><span class="pun">=</span><span class="pln"> imread</span><span class="pun">(</span><span class="str">"C:/Users/vitor/Desktop/Faculdade/Processamento Digital de Imagens/paisagem.jpg"</span><span class="pun">,</span><span class="pln"> CV_LOAD_IMAGE_COLOR</span><span class="pun">);</span><span class="pln">
	</span><span class="typ">Mat</span><span class="pln"> samples</span><span class="pun">(</span><span class="pln">img</span><span class="pun">.</span><span class="pln">rows </span><span class="pun">*</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">,</span><span class="pln"> </span><span class="lit">3</span><span class="pun">,</span><span class="pln"> CV_32F</span><span class="pun">);</span><span class="pln">

	</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> i </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> i </span><span class="pun">&lt;</span><span class="pln"> </span><span class="lit">10</span><span class="pun">;</span><span class="pln"> i</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> y </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> y </span><span class="pun">&lt;</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">;</span><span class="pln"> y</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> x </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> x </span><span class="pun">&lt;</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">;</span><span class="pln"> x</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> z </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> z </span><span class="pun">&lt;</span><span class="pln"> </span><span class="lit">3</span><span class="pun">;</span><span class="pln"> z</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
					samples</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">y </span><span class="pun">+</span><span class="pln"> x </span><span class="pun">*</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> z</span><span class="pun">)</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">at</span><vec3b><span class="pun">(</span><span class="pln">y</span><span class="pun">,</span><span class="pln"> x</span><span class="pun">)[</span><span class="pln">z</span><span class="pun">];</span><span class="pln">
				</span><span class="pun">}</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		kmeans</span><span class="pun">(</span><span class="pln">samples</span><span class="pun">,</span><span class="pln">
			nClusters</span><span class="pun">,</span><span class="pln">
			rotulos</span><span class="pun">,</span><span class="pln">
			</span><span class="typ">TermCriteria</span><span class="pun">(</span><span class="pln">CV_TERMCRIT_ITER </span><span class="pun">|</span><span class="pln"> CV_TERMCRIT_EPS</span><span class="pun">,</span><span class="pln"> </span><span class="lit">10000</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0.0001</span><span class="pun">),</span><span class="pln">
			nRodadas</span><span class="pun">,</span><span class="pln">
			KMEANS_RANDOM_CENTERS</span><span class="pun">,</span><span class="pln">
			centros</span><span class="pun">);</span><span class="pln">


		</span><span class="typ">Mat</span><span class="pln"> rotulada</span><span class="pun">(</span><span class="pln">img</span><span class="pun">.</span><span class="pln">size</span><span class="pun">(),</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">type</span><span class="pun">());</span><span class="pln">
		</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> y </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> y </span><span class="pun">&lt;</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">;</span><span class="pln"> y</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			</span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="kwd">int</span><span class="pln"> x </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0</span><span class="pun">;</span><span class="pln"> x </span><span class="pun">&lt;</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">cols</span><span class="pun">;</span><span class="pln"> x</span><span class="pun">++)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
				</span><span class="kwd">int</span><span class="pln"> indice </span><span class="pun">=</span><span class="pln"> rotulos</span><span class="pun">.</span><span class="pln">at</span><int><span class="pun">(</span><span class="pln">y </span><span class="pun">+</span><span class="pln"> x </span><span class="pun">*</span><span class="pln"> img</span><span class="pun">.</span><span class="pln">rows</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
				rotulada</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">y</span><span class="pun">,</span><span class="pln"> x</span><span class="pun">)[</span><span class="lit">0</span><span class="pun">]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="pln">uchar</span><span class="pun">)</span><span class="pln">centros</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">indice</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">);</span><span class="pln">
				rotulada</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">y</span><span class="pun">,</span><span class="pln"> x</span><span class="pun">)[</span><span class="lit">1</span><span class="pun">]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="pln">uchar</span><span class="pun">)</span><span class="pln">centros</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">indice</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">);</span><span class="pln">
				rotulada</span><span class="pun">.</span><span class="pln">at</span><span class="pun">&lt;</span><span class="typ">Vec3b</span><span class="pun">&gt;(</span><span class="pln">y</span><span class="pun">,</span><span class="pln"> x</span><span class="pun">)[</span><span class="lit">2</span><span class="pun">]</span><span class="pln"> </span><span class="pun">=</span><span class="pln"> </span><span class="pun">(</span><span class="pln">uchar</span><span class="pun">)</span><span class="pln">centros</span><span class="pun">.</span><span class="pln">at</span><span class="str">&lt;float&gt;</span><span class="pun">(</span><span class="pln">indice</span><span class="pun">,</span><span class="pln"> </span><span class="lit">2</span><span class="pun">);</span><span class="pln">
			</span><span class="pun">}</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="com">//Aqui salvamos as imagens para o gif</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">0</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered1.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">1</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered2.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">2</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered3.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">3</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered4.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">4</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered5.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">5</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered6.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">6</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered7.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">7</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered8.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">8</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered9.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
		</span><span class="kwd">if</span><span class="pln"> </span><span class="pun">(</span><span class="pln">i </span><span class="pun">==</span><span class="pln"> </span><span class="lit">9</span><span class="pun">)</span><span class="pln"> </span><span class="pun">{</span><span class="pln">
			imshow</span><span class="pun">(</span><span class="str">"clustered image"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
			imwrite</span><span class="pun">(</span><span class="str">"clutered10.jpeg"</span><span class="pun">,</span><span class="pln"> rotulada</span><span class="pun">);</span><span class="pln">
		</span><span class="com">//	waitKey(0);</span><span class="pln">
		</span><span class="pun">}</span><span class="pln">
	</span><span class="pun">}</span><span class="pln">
</span><span class="pun">}</span><span class="pln">
</span></int></vec3b></code>
</pre>
<p></p>

</body></html>
