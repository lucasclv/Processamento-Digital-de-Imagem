<!DOCTYPE html>
<html lang="pr-br">
<head>
	<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js?skin=doxy"></script>
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
<p>Aluno: Lucas da Cunha Lima Vale
</p>
<h2>Atividade 1 - Negativo e Trocar Regiões na diagonal</h2>
<h3>1.1 - Negativo</h3>
<p>
Utilizando a ideia apresentada pelo professor para o exercicio <br>
Imagem utilizada:<br>
<img src="\D:\Lucas\ufrn\2021.2\pdi\exercicios\jordan.jpeg" alt="Cachorro" style="width:35%"><br>
Imagem de saída do programa:<br>
<img src="\D:\Lucas\ufrn\2021.2\pdi\exercicios\negativo.jpeg" alt="Cachorro"style="width:35%"><br>
Código Utilizado:<br>
<pre class="prettyprint">
<code>
import cv2 as cv
import sys
import numpy as np
img = cv.imread("jordan.jpeg", cv.IMREAD_COLOR)
if img is None:
    sys.exit("Could not read the image.")
img[300:700, 500:900] = 255-img[300:700, 500:900]
cv.imshow("Negativo", img)
cv.imwrite("negativo.jpeg", img)
</code>
</pre>
</p>
<h3>1.2 - Trocar Regiões na Diagonal</h3>
<p>
Para essa parte da atividade fora a mesma imagem do item 1.1.<br>
Nesse caso a saída do programa foi:<br>
<img src="\D:\Lucas\ufrn\2021.2\pdi\exercicios\jordantrocado.png" alt="Um cachorro"style="width:35%"><br>
Código Utilizado:<br>
<pre class="prettyprint">
<code>
import cv2 as cv
import sys
import numpy as np
img = cv.imread(cv.samples.findFile("jordan.jpeg"))
if img2 is None:
    sys.exit("Could not read the image.")
print('Largura em pixels: ', end='')  
print(img.shape[1]) #largura da imagem
l=img.shape[1]
print('Altura em pixels: ', end='')  
print(img.shape[0]) #altura da imagem
a=img.shape[0]
print('Qtde de canais: ', end='')  
print(img.shape[2])
img2=img.copy()
ma=800
ml=450
for x in range(0,a):
    for y in range(0,l):
        if x<ml and y<ma:
            img2[x, y]=img[x+ml, y+ma]
        if x<ml and y>ma:
            img2[x, y]=img[x+ml, y-ma]
        if x>ml and y<ma:
            img2[x, y]=img[x-ml, y+ma]
        if x>ml and y>ma:
            img2[x, y]=img[x-ml, y-ma]
cv.imshow("cachorrotrocado", img2)
cv.imwrite("jordantrocado.png", img2)
</code>
</pre>
</p>
<h2>Atividade 2 - Detector de Objetos</h2>
<h3>2.1 - Detector</h3>
<p>
Para resolvermos o problema da contagem de objetos que seja acima de 255 podemos colocar um contador que conte quantas vezes o contador atual atingiu o 255, toda vez que atingir o 255 zera este contador, zerar o contador enquanto que armazenamos no número de vezes que ele chegou ao valor de 255, no final do laço somaríamos mais assim o contador que conta as vezes que o contador inicial chega até 255 multiplicado por 255 mais o valor do contador inicial daria o total de objetos na imagem.<br>
Utilizando a ideia apresentada pelo professor:<br>
Imagem de entrada:<br>
<img src="\D:\Lucas\ufrn\2021.2\pdi\exercicios\bolhas.png" alt="Objetos"style="width:35%"><br>
Imagem de saída:<br>
<img src="\D:\Lucas\ufrn\2021.2\pdi\exercicios\bolhas2.png" alt="Objetos"style="width:35%"><br>
Contagem:<br>
<img src="\D:\Lucas\ufrn\2021.2\pdi\exercicios\contador.png" alt="Janela CMD"style="width:35%"><br>
Código Utilizado:<br>
<pre class="prettyprint">
<code>
import cv2 as cv
import sys
import numpy as np
img = cv.imread(cv.samples.findFile("bolhas.png"))
if img is None:
    sys.exit("Could not read the image.")
imgflood = img.copy()
print('Largura em pixels: ', end='')  
print(img.shape[1]) #largura da imagem
l=img.shape[1]
print('Altura em pixels: ', end='')  
print(img.shape[0]) #altura da imagem
a=img.shape[0]
print('Qtde de canais: ', end='')  
print(img.shape[2])
mask = np.zeros((a+2, l+2), np.uint8)
c=0
cb=0
for x in range (0, a):
    cv.floodFill(imgflood, mask, (0,x), (0, 0, 0))
    cv.floodFill(imgflood, mask, (x,0), (0, 0, 0))
    cv.floodFill(imgflood, mask, (a-1,x), (0, 0, 0))
    cv.floodFill(imgflood, mask, (x,a-1), (0, 0, 0))
cv.imwrite("bolhas2.png", imgflood)
img=imgflood.copy()
for x in  range (0, a-1):
    for y in range (0, l-1):
       if imgflood[x, y, 2]==255:
            c+=1
            cv.floodFill(imgflood, mask, (y, x), (0, 0, 0))
cv.floodFill(img,None, (0, 0), (255, 255, 255));
cv.imshow("Display window", img)
cv.imwrite("bolhasvazias.png", img)
for x in  range (0, a-1):
    for y in range (0, l-1):
       if img[x, y, 2]==0:
            cb+=1
            cv.floodFill(img, mask, (y, x), (255, 255, 255))
print ('quantidade de objetos: ' ,c)
print ('quantidade de objetos sem buraco: ' ,cb)
print ('quantidade de objetos com buraco: ' ,c-cb)
cv.imwrite("bolhas3.png", imgflood)
</code>
</pre>
</p>
<h2>Atividade 3 - Equalizador de Histograma e Detector de Movimento</h2>
<h3>3.1 - Equalizador de Histograma</h3>	
<p>
Utilizando o programa histogram.cpp como base.<br>
Imagem utilizada:<br>
<img src="\Nova pasta\carro2.jpg" alt="Um carro"style="width:35%"><br>
Imagem de saída do programa em escala de cinza sem equalização:<br>
<img src="\Nova pasta\grayscalebe.jpg" alt="Um carro"style="width:35%"><br>
Imagem de saída do programa equalizada:<br>
<img src="\Nova pasta\equalizado.jpg" alt="Um carro"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
#include &#60iostream&#62
#include &#60opencv2/opencv.hpp&#62

using namespace cv;
using namespace std;

int main() {
	Mat image = imread("DIR da IMAGEM");
	Mat imageout = image;
	int width, height;
	Mat hist,hist2;
	int nbins = 64;
	float range[] = { 0, 256 };
	const float *histrange = { range };
	bool uniform = true;
	bool acummulate = false;

	width = image.rows;
	height = image.cols;

	int histw = nbins, histh = nbins / 2;
	Mat histImg(histh, histw, CV_8UC1, Scalar(0, 0, 0));
	Mat histImg2(histh, histw, CV_8UC1, Scalar(0, 0, 0));
	//A função ctvColor torna a transforma a imagem de RGB para tom de cinza
	cvtColor(image, image, CV_BGR2GRAY);
	//A função equalizeHist é quem proporciona a equalização do histograma
	equalizeHist(image, imageout);
	//Essa parte do código é duplicada para imprimir os histogramas da imagem em tom de cinza
	//com e sem equalização.
	calcHist(&imageout, 1, 0, Mat(), hist, 1,
		&nbins, &histrange,
		uniform, acummulate);
	calcHist(&image, 1, 0, Mat(), hist2, 1,
		&nbins, &histrange,
		uniform, acummulate);
	normalize(hist2, hist2, 0, histImg2.rows, NORM_MINMAX, -1, Mat());
	histImg2.setTo(Scalar(0));
	for (int i = 0; i < nbins; i++) {
		line(histImg2,
			Point(i, histh),
			Point(i, histh - cvRound(hist2.at&#60float&#62(i))),
			Scalar(255, 255, 255), 1, 8, 0);
	}
	histImg2.copyTo(image(Rect(10, 10, nbins, histh)));
	normalize(hist, hist, 0, histImg.rows, NORM_MINMAX, -1, Mat());
	histImg.setTo(Scalar(0));
	for (int i = 0; i < nbins; i++) {
		line(histImg,
			Point(i, histh),
			Point(i, histh - cvRound(hist.at&#60float&#62(i))),
			Scalar(255, 255, 255), 1, 8, 0);
	}
	histImg.copyTo(imageout(Rect(10, 10, nbins, histh)));
	namedWindow("imagemod", WINDOW_AUTOSIZE);
	imshow("imagemod", image);
	namedWindow("image", WINDOW_AUTOSIZE);
	imshow("image", imageout);
	//Cria as imagens baseado no Mat selecionado e como é dado o arquivo de saida.
	imwrite("equalizado.jpg", imageout);
	imwrite("grayscalebe.jpg", image);
	waitKey();
	return 0;
}
</code>
</pre>
</p>
<h3>3.2 - Detector de Movimento</h3>
<p>
Utilizando o programa histogram.cpp como base.<br>
Temos como imagem de entrada o vídeo capturado pela câmera. Toda vez que é detectado movimento é impresso na tela a mensagem "Movimento Detectado":<br>
<img src="\Nova pasta\motion.jpg" alt="Movimento Detectado" width="800" height="350"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
#include &#60iostream&#62
#include &#60cmath&#62
#include &#60opencv2/opencv.hpp&#62

using namespace cv;
using namespace std;

int main(int argc, char** argv) {
	Mat frameA, frameB;
	double teste;
	int width, height;
	VideoCapture cap;
	vector<Mat> planes;
	Mat hist, histB;
	int nbins = 64;
	float range[] = { 0, 256 };
	const float *histrange = { range };
	bool uniform = true;
	bool acummulate = false;

	cap.open(0);

	if (!cap.isOpened()) {
		cout << "cameras indisponiveis";
		return -1;
	}

	width = cap.get(CV_CAP_PROP_FRAME_WIDTH);
	height = cap.get(CV_CAP_PROP_FRAME_HEIGHT);

	int histw = nbins, histh = nbins / 2;
	Mat histImg(histh, histw, CV_8UC1, Scalar(0, 0, 0));
	//Aqui fazemos o calculo do primeiro frame para fazermos a primeira comparação de histogramas
	cap >> frameA;
	cvtColor(frameA, frameA, CV_BGR2GRAY);
	calcHist(&frameA, 1, 0, Mat(), hist, 1,
		&nbins, &histrange,
		uniform, acummulate);
	normalize(hist, hist, 0, histImg.rows, NORM_MINMAX, -1, Mat());
	while (1) {
		cap >> frameB;
		cvtColor(frameB	, frameB, CV_BGR2GRAY);
		calcHist(&frameB, 1, 0, Mat(), histB, 1,
			&nbins, &histrange,
			uniform, acummulate);
		normalize(histB, histB, 0, histImg.rows, NORM_MINMAX, -1, Mat());
		//Aqui fazemos o uso da função compareHist com o parametro CV_COMP_CORREL.
		//Isso encontrara uma correlação entre os dois histogramas calculados.
		teste = compareHist(hist, histB, CV_COMP_CORREL);
		if (teste < 0.993) {
			cout << "Movimento Detectado" << endl;
		}
		//Aqui o frameA recebe o frame atual da camera e calcula o histograma para a proxima iteração.
		cap >> frameA;
		cvtColor(frameA, frameA, CV_BGR2GRAY);
		calcHist(&frameA, 1, 0, Mat(), hist, 1,
			&nbins, &histrange,
			uniform, acummulate);
		normalize(hist, hist, 0, histImg.rows, NORM_MINMAX, -1, Mat());
		imshow("image", frameB);
		if (waitKey(30) >= 0) break;
	}
}
</code>
</pre>
</p>
<h2>Atividade 4 - Laplaciano do Gaussiano</h2>
<p>
Utilizando o programa filtroespacial.cpp como base.<br>
Imagem Utilizada:<br>
<img src="\Nova pasta\carro2.jpg" alt="Um carro"style="width:35%"><br>
Imagem de saída do programa com o filtro laplaciano:<br>
<img src="\Nova pasta\laplaciano.jpg" alt="Um carro"style="width:35%"><br>
Imagem de saída do programa com o filtro laplaciano do gaussiano:<br>
<img src="\Nova pasta\lapgauss.jpg" alt="Um carro"style="width:35%"><br>
Podemos observar um melhor detalhamento das bordas dos objetos na imagem.<br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
#include &#60iostream&#62
#include &#60opencv2/opencv.hpp&#62

using namespace cv;
using namespace std;

void printmask(Mat &m) {
	for (int i = 0; i < m.size().height; i++) {
		for (int j = 0; j < m.size().width; j++) {
			cout << m.at&#60float&#62(i, j) << ",";
		}
		cout << endl;
	}
}

void menu() {
	cout << "\npressione a tecla para ativar o filtro: \n"
		"a - calcular modulo\n"
		"m - media\n"
		"g - gauss\n"
		"v - vertical\n"
		"h - horizontal\n"
		"l - laplaciano\n"
		"k - laplgauss\n"
		"esc - sair\n";
}

int main(int argvc, char** argv) {
	VideoCapture video;
	float media[] = { 1,1,1,
		1,1,1,
		1,1,1 };
	float gauss[] = { 1,2,1,
		2,4,2,
		1,2,1 };
	float horizontal[] = { -1,0,1,
		-2,0,2,
		-1,0,1 };
	float vertical[] = { -1,-2,-1,
		0,0,0,
		1,2,1 };
	float laplacian[] = { 0,-1,0,
		-1,4,-1,
		0,-1,0 };
	//Aqui é criado a mascara 5x5 (matriz) do filtro laplaciano do gaussiano.
	float laplgauss[] = {0,0,1,0,0,
		 0,1,2,1,0,
		1,2,-16,2,1,
		 0,1,2,1,0,
		 0,0,1,0,0};
	Mat cap = imread("DIR da IMAGEM");
	Mat  frame, frame32f, frameFiltered;
	Mat mask(3, 3, CV_32F), mask1;
	Mat result, result1;
	double width, height, min, max;
	int absolut;
	char key;

	width = cap.cols;
	height = cap.rows;
	std::cout << "largura=" << width << "\n";;
	std::cout << "altura =" << height << "\n";;

	namedWindow("filtroespacial", 1);

	mask = Mat(3, 3, CV_32F, media);
	scaleAdd(mask, 1 / 9.0, Mat::zeros(3, 3, CV_32F), mask1);
	swap(mask, mask1);
	absolut = 1; // calcs abs of the image

	menu();
	for (;;) {
		cvtColor(cap, frame, CV_BGR2GRAY);
		flip(frame, frame, 1);
		imshow("original", frame);
		frame.convertTo(frame32f, CV_32F);
		filter2D(frame32f, frameFiltered, frame32f.depth(), mask, Point(1, 1), 0);
		if (absolut) {
			frameFiltered = abs(frameFiltered);
		}
		frameFiltered.convertTo(result, CV_8U);
		imshow("filtroespacial", result);
		key = (char)waitKey(10);
		if (key == 27) break; // esc pressed!
		switch (key) {
		case 'a':
			menu();
			absolut = !absolut;
			break;
		case 'm':
			menu();
			mask = Mat(3, 3, CV_32F, media);
			scaleAdd(mask, 1 / 9.0, Mat::zeros(3, 3, CV_32F), mask1);
			mask = mask1;
			printmask(mask);
			break;
		case 'g':
			menu();
			mask = Mat(3, 3, CV_32F, gauss);
			scaleAdd(mask, 1 / 16.0, Mat::zeros(3, 3, CV_32F), mask1);
			mask = mask1;
			printmask(mask);
			break;
		case 'h':
			menu();
			mask = Mat(3, 3, CV_32F, horizontal);
			printmask(mask);
			break;
		case 'v':
			menu();
			mask = Mat(3, 3, CV_32F, vertical);
			printmask(mask);
			break;
		case 'l':
			menu();
			mask = Mat(3, 3, CV_32F, laplacian);
			printmask(mask);
			//Criamos a imagem do laplaciano
			imwrite("laplaciano.jpg", frameFiltered);
			break;
			//Aqui é atribuido a letra k para fazer o Laplaciano do Gaussiano
		case 'k':
			menu();
			mask = Mat(5, 5, CV_32F, laplgauss);
			printmask(mask);
			//Criamos a imagem do laplaciano do gaussiano
			imwrite("lapgauss.jpg", frameFiltered);
			break;
		default:
			break;
		}
	}
	return 0;
}
</code>
</pre>
</p>
<h2>Atividade 5 - Tilt-shift em Imagem e Vídeo</h2>
<h3>5.1 - Imagem</h3>
<p>
Utilizando o programa addweighted.cpp como base.<br>
Imagem Utilizada:<br>
<img src="\Nova pasta\bridge.jpg" alt="Uma ponte"style="width:35%"><br>
Resuldado da saída do programa:<br>
<img src="\Nova pasta\tiltshifted.jpg" alt="Uma ponte"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
#include &#60iostream&#62
#include &#60opencv2/opencv.hpp&#62
#include &#60cmath&#62

using namespace cv;
using namespace std;

int pslider = 0;
int aslider = 0;
int dslider = 1;
int dslidermax = 100;
double l1, l2,alfa;
//Criamos a mascara para o borramento da imagem
float gauss[] = { 1,2,1,
2,4,2,
1,2,1 };


void on_trackbar_a(int, void*) {
	l1 = aslider - pslider;
	l2 = aslider + pslider;
}

void on_trackbar_p(int, void*) {
	l1 = aslider - pslider;
	l2 = aslider + pslider;
}

Mat image1, image2, blended;

char TrackbarName[50];

int main() {
	image1 = imread("DIR da IMAGEM");
	image1.copyTo(image2);
	image2.convertTo(image2, CV_32F);

	Mat mask = Mat(3, 3, CV_32F, gauss);
	scaleAdd(mask, 1 / 16.0, Mat::zeros(3, 3, CV_32F), mask);
	for (int i = 0; i < 10; i++) {
		filter2D(image2, image2, image2.depth(), mask, Point(1, 1), 0);
	}
	image2.convertTo(image2, CV_8U);
	cout << image1.rows << endl;
	cout << image1.cols << endl;
	namedWindow("addweighted", 1);
	sprintf_s(TrackbarName, "Altura %d", image1.rows);
	createTrackbar(TrackbarName, "addweighted",
		&aslider,
		image1.rows,
		on_trackbar_a);
	on_trackbar_a(aslider, 0);

	sprintf_s(TrackbarName, "Posição %d", image1.rows);
	createTrackbar(TrackbarName, "addweighted",
		&pslider,
		image1.rows,
		on_trackbar_p);
	on_trackbar_p(pslider, 0);

	sprintf_s(TrackbarName, "Decaimento %d", dslidermax);
	createTrackbar(TrackbarName, "addweighted",
		&dslider,
		dslidermax);

	blended = Mat::zeros(image1.rows, image1.cols, CV_8UC3);
	while (1) {
		for (int i = 0; i &#60 image1.rows; i++) {
			double d = (double)dslider;
			alfa = 0.5*(tanh((i - l1) / d) - tanh((i - l2) / d));
			addWeighted(image1.row(i), alfa, image2.row(i), 1 - alfa, 0, blended.row(i));
		}
		imshow("addweighted", blended);
		if (waitKey(30) == 27) break;
	}
	imwrite("tiltshifted.jpg", blended);
	return 0;
}
</code>
</pre>
</p>
<h3>5.2 - Vídeo</h3>
<p>
</p>
<h2>Atividade 6 - Filtro Homomórfico</h2>
<p>
Utilizando os programas exemplos/dft.cpp como base.<br>

Imagem Utilizada:<br>
<img src="\Nova pasta\maliluminada2.jpg" alt="Uma rua"style="width:35%"><br>
Resuldado da saída do programa:<br>
<img src="\Nova pasta\filtradahm.JPG" alt="Uma rua"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
#include &#60iostream&#62
#include &#60opencv2/opencv.hpp&#62
#include &#60opencv2/imgproc/imgproc.hpp&#62

#define RADIUS 20

using namespace cv;
using namespace std;

// troca os quadrantes da imagem da DFT
void deslocaDFT(Mat& image) {
	Mat tmp, A, B, C, D;

	// se a imagem tiver tamanho impar, recorta a regiao para
	// evitar cópias de tamanho desigual
	image = image(Rect(0, 0, image.cols & -2, image.rows & -2));
	int cx = image.cols / 2;
	int cy = image.rows / 2;

	// reorganiza os quadrantes da transformada
	// A B   ->  D C
	// C D       B A
	A = image(Rect(0, 0, cx, cy));
	B = image(Rect(cx, 0, cx, cy));
	C = image(Rect(0, cy, cx, cy));
	D = image(Rect(cx, cy, cx, cy));

	// A <-> D
	A.copyTo(tmp);  D.copyTo(A);  tmp.copyTo(D);

	// C <-> B
	C.copyTo(tmp);  B.copyTo(C);  tmp.copyTo(B);
}

int main() {
	Mat imaginaryInput, complexImage, multsp;
	Mat padded, filter, mag;
	Mat imagegray, tmp;
	Mat_<float> realInput, zeros;
	vector<Mat> planos;
	Mat image = imread("DIR da imagem",CV_LOAD_IMAGE_GRAYSCALE);

	// valores ideais dos tamanhos da imagem
	// para calculo da DFT
	int dft_M, dft_N;

	// identifica os tamanhos otimos para
	// calculo do FFT
	dft_M = getOptimalDFTSize(image.rows);
	dft_N = getOptimalDFTSize(image.cols);

	// realiza o padding da imagem
	copyMakeBorder(image, padded, 0,
		dft_M - image.rows, 0,
		dft_N - image.cols,
		BORDER_CONSTANT, Scalar::all(0));

	// parte imaginaria da matriz complexa (preenchida com zeros)
	zeros = Mat_&#60float&#62::zeros(padded.size());

	// prepara a matriz complexa para ser preenchida
	complexImage = Mat(padded.size(), CV_32FC2, Scalar(0));

	// a função de transferência (filtro frequencial) deve ter o
	// mesmo tamanho e tipo da matriz complexa
	filter = complexImage.clone();

	// cria uma matriz temporária para criar as componentes real
	// e imaginaria do filtro ideal
	tmp = Mat(dft_M, dft_N, CV_32F);

	float gamah, gamal, c, D0;
	gamah = 200;
	gamal = 100;
	c = 20;
	D0 = 40;
	int M = dft_M;
	int N = dft_N;

	//filtro homomórfico
	for (int i = 0; i < dft_M; i++) {
		for (int j = 0; j < dft_N; j++) {
			tmp.at&#60float&#62(i, j) = (gamah - gamal)*(1.0 - exp(-1.0*(float)c*((((float)i - M / 2.0)*((float)i - M / 2.0) + ((float)j - N / 2.0)*((float)j - N / 2.0)) / (D0*D0)))) + gamal;
		}
	}
	
	// cria a matriz com as componentes do filtro e junta
	// ambas em uma matriz multicanal complexa
	Mat comps[] = { tmp, tmp };
	merge(comps, 2, filter);

		// limpa o array de matrizes que vao compor a
		// imagem complexa
		planos.clear();
		// cria a compoente real
		realInput = Mat_&#60float&#62(padded);
		// insere as duas componentes no array de matrizes
		planos.push_back(realInput);
		planos.push_back(zeros);

		// combina o array de matrizes em uma unica
		// componente complexa
		merge(planos, complexImage);

		// calcula o dft
		dft(complexImage, complexImage);

		// realiza a troca de quadrantes
		deslocaDFT(complexImage);

		// aplica o filtro frequencial
		mulSpectrums(complexImage, filter, complexImage, 0);

		// limpa o array de planos
		planos.clear();
		// separa as partes real e imaginaria para modifica-las
		split(complexImage, planos);

		// recompoe os planos em uma unica matriz complexa
		merge(planos, complexImage);

		// troca novamente os quadrantes
		deslocaDFT(complexImage);

		cout << complexImage.size().height << endl;
		// calcula a DFT inversa
		idft(complexImage, complexImage);

		// limpa o array de planos
		planos.clear();

		// separa as partes real e imaginaria da
		// imagem filtrada
		split(complexImage, planos);

		// normaliza a parte real para exibicao
		normalize(planos[0], planos[0], 0, 1, CV_MINMAX);
		imshow("original", image);
		imshow("filtrada", planos[0]);
		waitKey();
	return 0;
}
</code>
</pre>
</p>
<h2>Atividade 7 - Canny e a arte do Pontilhismo</h2>
<p>
Utilizando os programas canny.cpp e pontilhismo.cpp como base.<br>

Imagem Utilizada:<br>
<img src="\Nova pasta\carro.jpeg" alt="Um carro"style="width:35%"><br>
Resuldado da saída do programa:<br>
<img src="\Nova pasta\pontos.jpg" alt="Um carro"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
  #include &#60iostream&#62
  #include &#60opencv2/opencv.hpp&#62
  #include &#60fstream&#62
  #include &#60iomanip&#62
  #include &#60vector&#62
  #include &#60algorithm&#62
  #include &#60numeric&#62
  #include &#60ctime&#62
  #include &#60cstdlib&#62

  using namespace std;
  using namespace cv;


  #define STEP 5
  #define JITTER 3
  #define RAIO 2

  int main(int argc, char** argv){
  Mat Original, borderOriginalImage;
  Mat Pontilhismo;
  int x, y, width, height, gray;

  vector&#60int&#62 yrange;
  vector&#60int&#62 xrange;

  srand(time(0));

  Original= imread("DIR da imagem" ,CV_LOAD_IMAGE_GRAYSCALE);

  width = Original.size().width;
  height = Original.size().height;
  xrange.resize(height/STEP);
  yrange.resize(width/STEP);
  iota(xrange.begin(), xrange.end(), 0);
  iota(yrange.begin(), yrange.end(), 0);

  for(uint i=0; i&#60xrange.size(); i++){
    xrange[i]= xrange[i]*STEP+STEP/2;
  }

  for(uint i=0; i&#60yrange.size(); i++){
    yrange[i]= yrange[i]*STEP+STEP/2;
  }

  Original.copyTo(Pontilhismo);

  //Executa o pontilhismo;
  for(auto i : xrange){
    random_shuffle(yrange.begin(), yrange.end());
    for(auto j : yrange){
      x = i+rand()%(2*JITTER)-JITTER+1;
      y = j+rand()%(2*JITTER)-JITTER+1;
      gray = Original.at&#60uchar&#62(x,y);
      circle(Pontilhismo, cv::Point(y,x), RAIO, CV_RGB(gray,gray,gray), -1, CV_AA);
    }
  }

  imshow("Imagem Pontilhista", Pontilhismo);
  imwrite("imagemComPontilhismo.jpg", Pontilhismo);

   //Aplica Canny
   for(int z=0; z &#60 5; z++){
     Canny(Original, borderOriginalImage, 10*z, 50*z);
     int raio = 10-z;

     for(int i=0; i &#60 height; i++ ){
        for(int j=0; j &#60 width; j++){
           if(borderOriginalImage.at&#60uchar&#62(i,j) == 255){
              gray = Original.at&#60uchar&#62(i,j);
              circle(Pontilhismo, cv::Point(j,i), raio, CV_RGB(gray,gray,gray), -1, CV_AA);
             }
        }
    }


  }
  imshow("Pontilhismo", Pontilhismo);
  imwrite("imagemComPontilhismo.jpg", Pontilhismo);

   waitKey();
  return 0;
}
</code>
</pre>
</p>
<h2>Atividade 8 - Kmeans clustering</h2>
<p>
O agrupamento k-means (k-means clustering) é um método de agrupamento que visa dividir n observações em k grupos, no caso do programa utilizado ele agrupa os pixels da imagens em k cores (k grupos) diferentes; com o uso do parâmetro KMEANS_RANDOM_CENTERS no lugar do KMEANS_PP_CENTERS os k grupos são escolhidos aleatoriamente, fazendo várias rodadas podemos ver que a imagem de saída pode variar por causa dos agrupamentos feitos com cores diferentes.<br>
Utilizando o programa kmeans.cpp como base.<br>

Imagem Utilizada:<br>
<img src="\Nova pasta\paisagem.jpg" alt="Uma montanha"style="width:35%"><br>
Resuldado da saída do programa juntos num gif:<br>
<img src="\Nova pasta\clusteredf.gif" alt="Uma montanha"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
#include &#60opencv2/opencv.hpp&#62
#include &#60cstdlib&#62
#include &#60iostream&#62

using namespace std;
using namespace cv;

int main() {
	int nClusters = 6;
	Mat rotulos;
	int nRodadas = 1;
	Mat centros;

	Mat img = imread("C:/Users/vitor/Desktop/Faculdade/Processamento Digital de Imagens/paisagem.jpg", CV_LOAD_IMAGE_COLOR);
	Mat samples(img.rows * img.cols, 3, CV_32F);

	for (int i = 0; i < 10; i++) {
		for (int y = 0; y < img.rows; y++) {
			for (int x = 0; x < img.cols; x++) {
				for (int z = 0; z < 3; z++) {
					samples.at&#60float&#62(y + x * img.rows, z) = img.at<Vec3b>(y, x)[z];
				}
			}
		}
		kmeans(samples,
			nClusters,
			rotulos,
			TermCriteria(CV_TERMCRIT_ITER | CV_TERMCRIT_EPS, 10000, 0.0001),
			nRodadas,
			KMEANS_RANDOM_CENTERS,
			centros);


		Mat rotulada(img.size(), img.type());
		for (int y = 0; y < img.rows; y++) {
			for (int x = 0; x < img.cols; x++) {
				int indice = rotulos.at<int>(y + x * img.rows, 0);
				rotulada.at&#60Vec3b&#62(y, x)[0] = (uchar)centros.at&#60float&#62(indice, 0);
				rotulada.at&#60Vec3b&#62(y, x)[1] = (uchar)centros.at&#60float&#62(indice, 1);
				rotulada.at&#60Vec3b&#62(y, x)[2] = (uchar)centros.at&#60float&#62(indice, 2);
			}
		}
		//Aqui salvamos as imagens para o gif
		if (i == 0) {
			imshow("clustered image", rotulada);
			imwrite("clutered1.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 1) {
			imshow("clustered image", rotulada);
			imwrite("clutered2.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 2) {
			imshow("clustered image", rotulada);
			imwrite("clutered3.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 3) {
			imshow("clustered image", rotulada);
			imwrite("clutered4.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 4) {
			imshow("clustered image", rotulada);
			imwrite("clutered5.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 5) {
			imshow("clustered image", rotulada);
			imwrite("clutered6.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 6) {
			imshow("clustered image", rotulada);
			imwrite("clutered7.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 7) {
			imshow("clustered image", rotulada);
			imwrite("clutered8.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 8) {
			imshow("clustered image", rotulada);
			imwrite("clutered9.jpeg", rotulada);
		//	waitKey(0);
		}
		if (i == 9) {
			imshow("clustered image", rotulada);
			imwrite("clutered10.jpeg", rotulada);
		//	waitKey(0);
		}
	}
}
</code>
</pre>
</p>
</body>
</html>
