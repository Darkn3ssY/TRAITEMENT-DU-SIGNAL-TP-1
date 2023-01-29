# TRAITEMENT-DU-SIGNAL-TP-1

![image](https://user-images.githubusercontent.com/90354895/215298104-7c09f5a1-21c1-45b5-9e2c-6c769765087f.png)


# Objectifs
Représentation de signaux et applications de la transformée de Fourier discrète (TFD) sous Matlab. • Evaluation de l’intérêt du passage du domaine temporel au domaine fréquentiel dans l’analyse et l’interprétation des signaux physiques réels.

L’objectif du ce TP est de voir ensemble comment se servir des outils de traitement du signal pour analyser les signaux échantillonnés.
Pour cela, nous allons utiliser le logiciel MATLAB pour la simulation


Tracé des figures : toutes les figures devront être tracées avec les axes et les légendes des axes appropriés.

Travail demandé : un script Matlab commenté contenant le travail réalisé et des commentaires sur ce que vous avez compris et pas compris, ou sur ce qui vous a semblé intéressant ou pas, bref tout commentaire pertinent sur le TP.

# Représentation-temporelle-et-fréquentielle

Considérons un signal périodique x(t) constitué d’une somme de deux sinusoïdes de fréquences 15Hz et 20Hz. 𝐱(𝐭) = 𝐬𝐢𝐧(𝟐𝝅𝟏𝟓𝒕) + 𝐬𝐢𝐧(𝟐𝝅𝟐𝟎𝒕)

1- Tracer le signal x(t). Pas de temps : Te = 1/50s, Intervalle : 0, 10-Te. Pour approximer la TF continue d’un signal x(t), représenté suivant un pas Te, on utilise les deux commandes : fft et fftshif.
 
```matlab
Te=1/50;
x=[0:Te:10-Te];
y = sin(30*pi*x) + sin(40*pi*x);
subplot(3,2,1);
plot(x,y);
title('signal x(t) :'); 
```
  
  
![image](https://user-images.githubusercontent.com/90354895/215297896-1d66ac97-043b-4b73-86b1-5e2ba3a88388.png)

On remarquera que la TF est une fonction complexe et que la fonction ainsi obtenue décrit la TF de x(t) entre –1/(2Te) et 1/(2Te) par pas de 1/(nTe) où n est le nombre de points constituant le signal x(t).

```matlab 
f=(0:length(x)-1)*(1/Te*length(x)); 
fy=abs(fft(y));
subplot(3,2,2); 
plot(f,fy);
title('spectre du  x(t) :'); 
```
![image](https://user-images.githubusercontent.com/90354895/215297956-d4abb705-b3db-42f3-ba87-fb2c17161636.png)

Une fois notre signal généré, calculons maintenant sa Transformée de Fourier. 

```matlab 
fsh=[-500/2:(500/2)-1]*50/500;
fy=abs(fft(y));
subplot(3,2,3);
plot(fsh,fftshift(fy));
title('spectre du  x(t) :');
```
![image](https://user-images.githubusercontent.com/90354895/215297965-d3845a34-c893-4a65-a986-c3dbcc4916e2.png)


Pour se rapprocher de la réalité nous allons simuler la présence d’un bruit de mesure. Pour observer le même signal que x(t), nous allons générer un bruit aléatoire Gaussien.
```matlab
noise = 2*randn(size(x));
```
Afin de créer un signal bruité, ajoutons noise à x(t)

```noise = 2*randn(size(x));
xnoise = x+noise; 
plot(t,xnoise,'.')
grid
title('signal x bruité');
xlabel('Temps');
ylabel('Amplitudesà');
```

![image](https://user-images.githubusercontent.com/90354895/215298052-497c99c9-7dad-41af-8954-0a3c82114c1b.png)

Calculons à nouveau la Transformée de Fourier du signal bruité Sb(t)

![image](https://user-images.githubusercontent.com/90354895/215298065-65588067-671b-4851-812c-ed98c48914b9.png)

![image](https://user-images.githubusercontent.com/90354895/215298067-2db6f56d-38d9-44e3-9f61-2fe237bd3424.png)

Conception du filtre pass bas idéal FILTRAGE IDEAL

![image](https://user-images.githubusercontent.com/90354895/215298068-380b2d8b-6d29-487b-bb64-d493796b7a33.png)

On l’applique sur le spectre de x(t) 

![image](https://user-images.githubusercontent.com/90354895/215298070-a5f6247a-faac-4154-93f3-a6bf0c5bb9b4.png)

![image](https://user-images.githubusercontent.com/90354895/215298074-bcf2ec68-86ad-476e-9307-23b3e8ccd39f.png)



