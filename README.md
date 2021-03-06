<html lang="pr-br">
<head>
</head>
<body>
<h1>Processamento Digital de Imagens</h1>
<p>Aluno: Lucas da Cunha Lima Vale
</p>
<h2>Atividade 1 - Negativo e Trocar Regiões na diagonal</h2>
<h3>1.1 - Negativo</h3>
Utilizando a ideia apresentada pelo professor para o exercicio <br>
Imagem utilizada:<br>
<img src="jordan.jpeg" alt="Cachorro" style="width:35%"/><br>
Imagem de saída do programa:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/negativo.jpeg?raw=true" alt="Cachorronegativo"style="width:35%"><br>
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
<h3>1.2 - Trocar Regiões na Diagonal</h3>
<p>
Para essa parte da atividade fora a mesma imagem do item 1.1.<br>
Nesse caso a saída do programa foi:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/jordantrocado.png?raw=true" alt="cachorro"style="width:35%"><br>
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
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/bolhas.png?raw=true" alt="Objetos"style="width:35%"><br>
Imagem sem objetos na borda:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/bolhas2.png?raw=true" alt="Objetos"style="width:35%"><br>
Contagem:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/contador.png?raw=true" alt="Janela CMD"style="width:35%"><br>
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
<h2>Atividade 3 - Equalizador de Histograma</h2>	
<p>
Utilizando a ideia apresentada pelo professor:<br>
Imagem utilizada:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/jordan3.jpeg?raw=true" alt="cachorro"style="width:35%"><br>
Imagem de saída do programa em escala de cinza a esquerda sem equalização e a direita com equalização:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/cachorros.png?raw=true" alt="cachorros"style="width:35%"><br>
Histograma:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/histograma.png?raw=true" alt="histograma"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
import sys
import numpy as np
from matplotlib import pyplot as plt
img = cv.imread(cv.samples.findFile("jordan3.jpeg"))
if img is None:
    sys.exit("Could not read the image.")
print('Largura em pixels: ', end='')  
print(img.shape[1]) #largura da imagem
l=img.shape[1]
print('Altura em pixels: ', end='')  
print(img.shape[0]) #altura da imagem
a=img.shape[0]
print('Qtde de canais: ', end='')  
print(img.shape[2])
img = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
hist = cv.calcHist([img], [0], None, [256], [0, 256])
equ = cv.equalizeHist(img)
res = np.hstack((img,equ))
hist2 = cv.calcHist([equ], [0], None, [256], [0, 256])
hist2 /= hist2.sum()
plt.figure()
plt.axis("off")
#plt.imshow(cv.cvtColor(img, cv.COLOR_GRAY2RGB))
# plot the histogram
#plt.figure()
plt.title("Histograma")
#plt.plot(hist)
plt.xlim([0, 256])
plt.plot(hist2)
plt.xlim([0, 256])
cv.imshow("Display window", res)
cv.imwrite("cachorros.png", res)
plt.show()
</code>
</pre>
</p>
<h2>Atividade 4 - Laplaciano do Gaussiano</h2>	
<p>
Utilizando a ideia apresentada pelo professor:<br>
Imagens obtidas:<br>
<img src="https://github.com/lucasclv/Processamento-Digital-de-Imagem/blob/main/laplace.png?raw=true" alt="cachorro"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
import numpy as np
import cv2 as cv
from matplotlib import pyplot as plt
img = cv.imread('jordan.jpeg',0)
laplacian = cv.Laplacian(img,cv.CV_16S,ksize=19)
blur = cv.GaussianBlur(img,(9,9),0)
laplacegauss = cv.Laplacian(blur,cv.CV_16S,ksize=19)
plt.subplot(2,2,1),plt.imshow(img,cmap = 'gray')
plt.title('Original'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,2),plt.imshow(laplacian,cmap = 'gray')
plt.title('Laplace'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,3),plt.imshow(blur,cmap = 'gray')
plt.title('Gaussiana'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,4),plt.imshow(laplacegauss,cmap = 'gray')
plt.title('LaPlace da Gaussiana'), plt.xticks([]), plt.yticks([])
plt.show()
</code>
</pre>
</p>
<h2>Atividade 8 - Canny e Pontilhismo</h2>	
<p>
Utilizando a ideia apresentada pelo professor:<br>
Utilizando a imagem do cachorro:<br>
<img src="jordan3.jpeg" alt="cachorro"style="width:35%"><br>
Imagem obtida:<br>
<img src="canny-point.png" alt="cachorrocannypontilhismo"style="width:35%"><br>
Código utilizado:<br>
<pre class="prettyprint">
<code>
import cv2
import numpy as np
from copy import copy
import random

STEP = 10
JITTER = 6
RADIUS = 5

T1 = 10 
edges = 0

image = cv2.imread("jordan3.jpeg", 0)
height, width = image.shape
points = copy(image)

for i in range(height):
    for j in range(width):
        points[i, j] = 255

xrange = np.zeros(int(height/STEP))
yrange = np.zeros(int(width/STEP))

for xvalue in range(len(xrange)):
    xrange[xvalue] = xvalue

for yvalue in range(len(yrange)):
    yrange[yvalue] = yvalue

xrange = [value*STEP+STEP/2 for value in xrange]
yrange= [value*STEP+STEP/2 for value in yrange]

np.random.shuffle(xrange)

for i in xrange:
    np.random.shuffle(yrange)
    for j in yrange:
        x = int(i + random.randint(1, 2*JITTER-JITTER))
        y = int(j + random.randint(1, 2*JITTER-JITTER))
        if(x >= height):
                x = height-1
        if( y >= width):
                y = width-1
        gray = image[x,y]
        cv2.circle(points,
                (y, x),
                RADIUS,
                int(gray),
                -1,
                cv2.LINE_AA)

edges = cv2.Canny(points, T1, 3*T1) 

for i in range(height):
    for j in range(width):
        if(edges[i, j] != 0):
            gray = image[i,j]
            cv2.circle(points,
                    (j, i),
                    RADIUS,
                    int(gray),
                    -1,
                    cv2.LINE_AA)

cv2.imshow("canny-point", points)
cv2.imwrite("canny-point.png", points)
cv2.waitKey(0)     
cv2.destroyAllWindows()
</code>
</pre>
</p>
<h2>Atividade 9 - Kmeans</h2>	
<p>
Utilizando a ideia apresentada pelo professor:<br>
Imagem utilizada:<br>
<img src="gato.jpeg" alt="gato"style="width:35%"><br>
Imagens obtidas:<br>
<img src="gatokmeans1.png" alt="gatokmeans1"style="width:35%"><br>
<img src="gatokmeans2.png" alt="gatokmeans2"style="width:35%"><br>
<img src="gatokmeans3.png" alt="gatokmeans3"style="width:35%"><br>
<img src="gatokmeans4.png" alt="gatokmeans4"style="width:35%"><br>
<img src="gatokmeans5.png" alt="gatokmeans5"style="width:35%"><br>
<img src="gatokmeans6.png" alt="gatokmeans6"style="width:35%"><br>
<img src="gatokmeans7.png" alt="gatokmeans7"style="width:35%"><br>
<img src="gatokmeans8.png" alt="gatokmeans8"style="width:35%"><br>
<img src="gatokmeans9.png" alt="gatokmeans9"style="width:35%"><br>
<img src="gatokmeans10.png" alt="gatokmeans10"style="width:35%"><br>
Podemos observar que as imagens resultantes são diferentes pois cada rodada do codigo o ponto inicial utilizado na clusterização muda
Código utilizado:<br>
<pre class="prettyprint">
<code>
import numpy as np
import cv2 as cv
img = cv.imread('gato.jpeg')
Z = img.reshape((-1,3))
# convert to np.float32
Z = np.float32(Z)
# define criteria, number of clusters(K) and apply kmeans() 10 times
for nrodadas in range (1,11):
	criteria = (cv.TERM_CRITERIA_EPS + cv.TERM_CRITERIA_MAX_ITER, 10, 1.0)
	K = 7
	ret,label,center=cv.kmeans(Z,K,None,criteria,10,cv.KMEANS_RANDOM_CENTERS)
	# Now convert back into uint8, and make original image
	center = np.uint8(center)
	res = center[label.flatten()]
	res2 = res.reshape((img.shape))
	cv.imshow('res2',res2)
	cv.waitKey(0)
cv.destroyAllWindows()
</code>
</pre>
</p>
</body>
</html>
