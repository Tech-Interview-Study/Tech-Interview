# MLE, 베이즈정리 내용 이해 후 딥러닝과 VAE와 같은 모델에서 어떻게 사용되는지

## VAE에서 MLE방법론이 어떻게 사용되는건지?

VAE의 학습을 위해 maximum likelihood 접근법을 택합니다. 즉, $p_\theta (x)$를 maximize하는 $
\theta$를 찾는 것을 목적으로 하는 것입니다. 이를 식으로 표현하면, 다음과 같은 loglikelihood를 maximize하는 것입니다.

![image](https://github.com/Tech-Interview-Study/Tech-Interview/assets/68782183/075ce3e8-1fd7-4e8f-be22-17270d2f9329)


첫 번째 항은 p(x|z)와 q(z|x) 사이의 negative cross entropy와 같다. 그렇기 때문에 이는 encoder와 decoder가 autoencoder처럼 reconstruction을 잘 할 수 있게 만들어주는 error라고 할 수 있기 때문에 reconstruction error라고 부른다.  
두 번째 항은 posterior q(z|x)와 prior p(z) 간의 KL divergence와 같다. 그렇기 때문에 이는 posterior와 prior가 최대한 비슷하게 만들어주는 error라고 할 수 있고, 이는 VAE가 reconstruction task만 잘 하는 것을 방지하기 때문에 regularization error라고 부른다. 

참고 : [VAE 설명 (Variational autoencoder란? VAE ELBO 증명)](https://process-mining.tistory.com/161)

## MLE와 MAP의 차이점
- MLE는 likelihood를 최대화하는 방법.
- MAP는 posterior(likelihood * prior)를 최대화하는 방법.

- MLE는 a prior probability가 uniform distribution이라고 가정한 MAP라고 볼 수 있다.

이외에도 데이터 수가 많아지는 경우 MLE와 MAP가 거의 유사해진다. 

> 데이터 수가 많을 때, MLE와 MAP는 비슷한 결과를 보이게 됩니다. 이는 데이터의 양이 증가함에 따라 MLE가 더 정확한 추정을 하고, MAP에서의 사전 분포의 영향이 상대적으로 줄어들기 때문입니다. 하지만 데이터의 양이 제한적인 경우에는 MAP가 추가적인 정보를 활용하여 더 강력한 추정을 수행할 수 있습니다.



## Backpropagation과 MLE 관점의 차이점
- Backpropagation 관점 : 출력 $f_\theta (x)$과 정답 y의 차이를 Loss Function이라고 정의하고, 두 값의 차이를 줄이는 방향으로 학습을 진행
- MLE 관점 : 네트워크 출력 값(확률 분포) $f_\theta (x)$ 가 주어졌을 때, 정답 $y$가 나올 확률(**Likelihood**)가 최대가 되기를 목표

참고 : [BP관점과 MLE관점의 차이, 뒷쪽 내용 참고](https://junstar92.tistory.com/156)

--
# 참고자료

- https://wikidocs.net/152474
- https://towardsdatascience.com/why-vae-are-likelihood-based-generative-models-2670dd81a40
- https://junstar92.tistory.com/156

