---
layout: post
title: "Deep Residual Network"
description: 
headline: 
modified: 2016-09-22
category: research
tags: [research]
imagefeature: 
mathjax: true
chart: 
comments: true
featured: true
---


There is something intriguing me, that's the deep residual network. 

So, I want to talk a little bit about that!

### Deep Residual Network

Deep Residual Network is a architecture proposed by Kaiming He, former MSRA stuff. Now at FAIR. 

#### The Problem

The problem DRN met is: 

**We all know the more layers, the better result, 
BUT, is it true?**

It's not exactly. We can see the error comparison like this:

<center>
<img src="http://yanran.li/images/resnet_1.png" width="600" alt="citation network"/>
</center>


From the image, we can see that with more layers $(20\to 56)$, the training error and test error is higher. Why? maybe it's because the *"overly deep"* nets will affect and add noise with layer increase. 

So, instead of just add layers in the dataset, the plaint net will get input $x \to H(x)$. Comparingly, the ResNet will combine the $H(x)$ with input $x$. So the layers network is like this:

<center>
<img src="https://matrixmashing.files.wordpress.com/2016/01/residualunit.png" width="600" alt="citation network"/>
</center>

So, why they uses this architecture? 

The reason is that, in Back-propagation, when the number of layers increases, the effect from upper layer to under layer will be very small. So that each iteration will not affect any of higher layers. This is called the "degradation problem" according to the paper

> Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun. Deep Residual Learning for Image Recognition. 2015. arXiv preprint: 1512.03385. 

. In the paper, the authors proofed that degradation is not due to gradient vanishing, but a optimization difficulty(from yanran.li's blog).
Thus, if add **identity** $x$ in the architecture, the whole architecture can be trained, and the derivatives can be passed from layer to layer. Thus, the deep net can perform better. 

### More to Read: Highway Network and LSTM.

Highway network is a paper I found from yanran.li's website related to ResNet(Residual Networks). 

So, similarly, the Highway Network is to solve the "gradient vanishing" problem. The idea behind this is that they want to pass the difference from top layer to bottom layer. 

Thus, normally, a layer representation is like this:

$$\textbf{y}=H(\textbf{x}, \textbf{W}_H)$$

$H$ is usually an affine transform followed by a non-linear activation function. For a highway network, they added two linear transform into the architecture. 

$$\textbf{y} = H(\textbf{x}\cdot \textbf{W}_H) \cdot T(\textbf{x}, \textbf{W}_T) + \textbf{x} \cdot C(\textbf{x}, \textbf{W}_c) $$

So, what is $\textbf{T,C}$ respectively? According to the paper, $T$ is the transform gate and $C$ is the carry gate. 
This Idea comes from the LSTM architecture. In the paper, the author set $c = 1 - T$, making the representation:

$$\textbf{y} = H(\textbf{x}\cdot \textbf{W}_H) \cdot T(\textbf{x}, \textbf{W}_T) + \textbf{x} \cdot (1 - T(\textbf{x}, \textbf{W}_c)) $$

It's easy to understand that different $T$ will lead a different weight to $\textbf{x}$ and $H(x)$. Which makes the result of each layer closer to the result of one layer or the result of the input. 


