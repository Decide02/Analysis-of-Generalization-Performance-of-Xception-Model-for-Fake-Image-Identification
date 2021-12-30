# Analysis-of-Generalization-Performance-of-Xception-Model-for-Fake-Image-Identificaiton

![제목 없음 (1)](https://user-images.githubusercontent.com/77098071/147543712-394557c4-40bd-4967-a39d-99f5506a07ec.png)

__IVC(Image & Vision Computing) Lab / Pukyong Nat'l Univ Electronic Engineering / Busan, Republic of Korea__   
Jeonghan Lee, Hanhoon Park(Major Professor)

* Paper(Korean) :     
* Video(Korean) : https://youtu.be/y1UI2oyZGsI

## Introduction
As research on deep learning technology has been steadily conducted, various image generation techniques have been produces. Recently, an image generated by the hostile generation network GAN has excellent image quality that is difficult to distinguish with the naked eye from a real image. As a result, there is a social problem of abusing the generated video for crime. Therefore, deep learning-based research for identifying images generated by GAN is also actively being conducted. Recent research results show very high identification performance for fake images that are difficult to classify with the naked eye. However, there is a problem in that the performance of identifying a content different from the image used for learning or an image generated by a different GAN model from the image used for learning is significantly reduced.<br/><br/>
__In this paper,__ to improve the generalization performance of deep learning-based method,
1. we gradually increase the number of image categories used in learning
2. apply dropout, a universal generalization technique
3. experimentally analyze the change in generalization performance of the Xception model.

## Settings
### Dataset
* Category : LSUN - cat, church_outdoor, train, airplane, bus, cow, bridge, bedroom, classroom, restaurant, sheep
* Real/Fake 각각 Train set 25K장/ Test set 2K장 임의추출하여 사용 </br> -> Mix Train set이 25K가 넘지 않도록 Train set 구성. Test set은 Single Category로만 구성.
* Sheep 카테고리의 경우 Mixing Process에 포함하지 않는 대표 Unseen Test set으로 설정.
<br/> + StyleGAN2로 생성된 LSUN의 "horse"와 FFHQ 영상으로 Unseen Validation set을 구성(Not contain both GAN & contents data).
* Image size : 256X256
* GAN : ProGAN, StyleGAN2

# Feature extraction
* CNN model : Xception
* epoch = 50, batch_size = 64, learning_rate = 0.001, optimizer = Adam

## Result
### Experiment 1 : Accuracy of identifying fake images according to the number of image categories
![image](https://user-images.githubusercontent.com/77098071/147728778-03bb0730-a9e2-4792-b09c-5da7ed2ec8cb.png) <br/>
[Fig 1] Average accuracy and its linear trend line on evaluating unseen data according to changes in the number of image categories used in the training step
<br/><br/>

### Experiment 2 : Accuracy of identifying fake images according to the number of dropout ratio
![image](https://user-images.githubusercontent.com/77098071/147728930-a88f2e0b-8303-4ff2-880c-1985eb49f84e.png) <br/>
[Fig 2] Average accuracies and linear trend lines on evaluating unseen data according to dropout ratio
<br/><br/>

### Experiment 3 : Accuracy of identifying unseen fake images generated by different GAN models and contents
![image](https://user-images.githubusercontent.com/77098071/147729079-77596e6b-f256-4e1a-b883-6a8378559999.png) <br/>
[Fig 3] Accuracy according to dropout ratio when evaluating fake images generated by StyleGAN2 model
<br/><br/>

## Conclusion
* Objectives : 학습 시 보지 못한 콘텐츠를 포함하는 영상이나, 학습시 사용된 영상과 다른 GAN 모델로 생성된 영상에 대해 Xception 모델의 일반화 성능을 분석, 이를 향상시키기 위한 방법 고안
* 학습에 사용된 영상 카테고리 수가 증가할수록 새로운 콘텐츠를 가진 영상에 대한 식별의 정확도가 향상
* 드롭아웃을 통해 일반화 성능 보강이 가능 -> 특히, 적절한 드롭아웃 비율이 주어졌을 때 성능이 보다 향상
* but, 여전히 학습 시 사용된 영상과 다른 생성 모델로 생성되고, 학습 시 사용된 영상과 완전히 다른 콘텐츠를 가진 위조영상에 대한 분류 정확도가 낮음.
<br/> -> 정확도를 향상시키기 위한 추가 연구 필요.
<br/><br/>
### Acknowledgement
* "This research was supported by Basic Science Research Program through the National Research Foundation of Korea(NRF) funded by the Ministry of Education(No. 2021R1F1A1045749)"

<br/>

__This content is inspired by the documents below :__
1. I. Goodfellow, J. Pouget-Abadie, M. Mirza, B. Xu, D. Warde-Farley, S. Ozair, and Y. Bengio, "Generative adversarial nets," Proc. of NIPS, 27, 2014.
2. F. Yu, A. Seff, Y. Zhang, S. Song, T. Funkhouser, and J. Xiao, “LSUN: Construction of a large-scale image dataset using deep learning with humans in the loop,” arXiv preprint arXiv:1506.03365, 2015.
3. T. Karras, T. Aila, S. Laine, and J. Lehtinen, “Progressive growing of GANs for improved quality, stability, and variation,” arXiv preprint arXiv:1710.10196, 2017.
4. T. Karras, S. Laine, M. Aittala, J. Hellsten, J. Lehtinen, and T. Aila, “Analyzing and improving the image quality of StyleGAN,” Proc. of CVPR, pp. 8110-8119, 2020.
5. T. Karras, S. Laine, and T. Aila, “A style-based generator architecture for generative adversarial networks,” Proc. of CVPR, pp. 4401-4410, 2019.
6. F. Chollet, “Xception: Deep learning with depthwise separable convolutions,” Proc. of CVPR, pp. 1251-1258, 2017.
