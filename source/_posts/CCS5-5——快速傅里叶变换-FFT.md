---
title: CCS5.5——快速傅里叶变换(FFT)
top: false
cover: false
toc: true
mathjax: false
date: 2020-05-27 16:46:06
author: xing xiao 
img:
coverImg:
password:
summary:
tags: 算法
categories: C语言
---
---
  
# 1.原理  
1、离散傅里叶变换DFT的定义：将时域的采样变换成频域的周期性离散函数，频域的采样也可以变换成时域的周期性离散函数，这样的变化称为离散傅里叶变换，简称DFT。  

2、FFT是DFT的一种快速算法。由于在计算DFT是一次复数乘法需用四次实数乘法和两次实数加法；一次复数加法需要两次实数加法。每运算一个X(k)需要4N次复数乘法及 实数加法。所以整个DFT运算总共需要 次实数乘法及 次实数加法。如此，计算时乘法次数和加法次数都是和 成正比的，当N很大时，运算量是客观的，因而需要改进带DFT的算法减少运算速度。  

根据傅里叶变换的对称性和周期性，我们可以将DFT运算中有些项合并。假设序列长度为 ,L为整数。将 的序列x(n)(n=0,1,…,N-1),按N的奇偶分成两组，分解成两个N/2点的DFT，重新组合成一个如下式表达的N点DFT:  
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05271.jpg)  
  
将DFT的 步运算减少为 步，极大地提高了运算的速度；  

3、	旋转因子的变化规律；  

4、	碟形运算规律；  

5、	基于2FFT算法。  

![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05272.jpg)
  
# 2.记录实验数据  
按照图6-2，3进行输入信号时域，频域以及输出信号时域波形的设置。  
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05273.jpg)  
输入信号及输出信号的波形如图6-4,5,6所示：  
![](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05274.jpg)  
代码：
```  
#include"math.h"
#define PI 3.1415926
#define SAMPLENUMBER 128

void InitForFFT();
void MakeWave();

int INPUT[SAMPLENUMBER],DATA[SAMPLENUMBER];
float fWaveR[SAMPLENUMBER],fWaveI[SAMPLENUMBER],w[SAMPLENUMBER];
float sin_tab[SAMPLENUMBER],cos_tab[SAMPLENUMBER];

void FFT(float dataR[SAMPLENUMBER],float dataI[SAMPLENUMBER])
{
	int x0, x1, x2, x3, x4, x5, x6, xx;
	int i, j, k, b, p, L;
	float TR, TI, temp;
/***************fllowing code invert sequence***************/
	for( i = 0; i < SAMPLENUMBER; i++)
	{
		x0=x1=x2=x3=x4=x5=x6=0;
		x0=i&0x01;x1=(i/2)&0x01;x2=(i/4)&0x01;x3=(i/8)&0x01;x4=(i/16)&0x01;x5=(i/32)&0x01;x6=(i/64)&0x01;
		xx=x0*64+x1*32+x2*16+x3*8+x4*4+x5*2+x6;
		dataI[xx]=dataR[i];

	}
	for( i = 0; i < SAMPLENUMBER; i++)
	{
		dataR[i]=dataI[i];dataI[i]=0;
	}
/***********fllowing code FFT***************/
	for( L = 1; L <= 7; L++)
	{
		b=1;i=L-1;
		while( i > 0 ){
			b=b*2;i--;
		}/*b= 2^(L-1)*/
		for( j = 0; j <= b-1; j++ )
		{
			p=1;i=7-L;
			while( i > 0 ) /*p=pow(2,7-L)*j;*/
			{
				p=p*2;i--;
			}
			p=p*j;
			for( k = j; k < 128; k = k+2*b )
			{
				TR=dataR[k];TI=dataI[k];temp=dataR[k+b];
				dataR[k]=dataR[k]+dataR[k+b]*cos_tab[p]+dataI[k+b]*sin_tab[p];
				dataI[k]=dataI[k]-dataR[k+b]*sin_tab[p]+dataI[k+b]*cos_tab[p];
				dataR[k+b]=TR-dataR[k+b]*cos_tab[p]-dataI[k+b]*sin_tab[p];
				dataI[k+b]=TI+temp*sin_tab[p]-dataI[k+b]*cos_tab[p];
			}
		}
	}
	for( i = 0; i < SAMPLENUMBER/2; i++)
	{
		w[i]=sqrt(dataR[i]*dataR[i]+dataI[i]*dataI[i]);
	}
}/*END FFT*/
main()
{
	int i;

	InitForFFT();
	MakeWave();
	for( i = 0; i < SAMPLENUMBER; i++)
	{
		fWaveR[i]=INPUT[i];
		fWaveI[i]=0.0f;
		w[i]=0.0f;
	}
	FFT(fWaveR,fWaveI);
	for(i = 0; i < SAMPLENUMBER; i++)
	{
		DATA[i]=w[i];
	}
	while(1);  //break point
}

void InitForFFT()
{
	int i;
	for(i = 0; i < SAMPLENUMBER; i++)
	{
		sin_tab[i]=sin(PI*2*i/SAMPLENUMBER);
		cos_tab[i]=cos(PI*2*i/SAMPLENUMBER);
	}
}

void MakeWave()
{
	int i;
	
	for( i=0; i<SAMPLENUMBER; i++ )
	{
		INPUT[i]=sin(PI*2*i/SAMPLENUMBER*3)*1024;
	}
}  
```