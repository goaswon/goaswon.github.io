행복지수와 다른 지수간의 상관관계 조사

행복지수와 연관지을 다른 항목

>   ```python
>   Index(['year', 'country', 'region', 'happiness_rank', 'happiness_score',
>          'standard_error', 'economy', 'family', 'health', 'freedom', 'trust',
>          'generosity', 'dystopia_residual', 'social_support', 'country_code_x',
>          'crude_birth_rate', 'crude_death_rate', 'net_migration',
>          'rate_natural_increase', 'growth_rate', 'country_code_y', '2015',
>          '2016', '2017', '2018', '2019', 'country_code_x', 'Region2',
>          'IncomeGroup', 'country_code_y', 'country_area'])
>   ```

귀무가설 : 출산율과 행복지수 사이에는 연관성이 없다.

유의수준 5%로 설정

1.  행복지수의 분포확인

![happiness_score_hist](.\happiness_score_hist.png)

2.  행복지수와 상관계수가 0.6 이상인 항목 확인

| year                  | happiness_score |
| --------------------- | --------------- |
| year                  | -0.012516       |
| standard_error        | 0.163635        |
| economy               | -0.806314       |
| family                | -0.630381       |
| health                | -0.758855       |
| freedom               | -0.553786       |
| trust                 | -0.4228         |
| generosity            | -0.199163       |
| dystopia_residual     | -0.475189       |
| social_support        | -0.762935       |
| crude_birth_rate      | 0.690937        |
| crude_death_rate      | 0.262617        |
| net_migration         | -0.233703       |
| rate_natural_increase | 0.60109         |
| growth_rate           | 0.431437        |
| 2015                  | 0.009426        |
| 2016                  | 0.026223        |
| 2017                  | 0.032622        |
| 2018                  | 0.049641        |
| 2019                  | 0.046783        |
| country_area          | -0.155995       |

↓

| year             | happiness_score |
| ---------------- | --------------- |
| economy          | -0.806314       |
| family           | -0.630381       |
| health           | -0.758855       |
| social_support   | -0.762935       |
| crude_birth_rate | 0.690937        |



economy, family, health, social_support, crude_birth_rate 항목이 상관관계가 있을것으로 추정된다.

각각의 샘플의 분포도를 그려본다. NaN항목은 제외하고 그려본다.

![distsamples01](./distsamples01.png)

economy, family, health, social_support 4가지 샘플의 분포도

![distsamples02.png](./distsamples02.png)

crude_birth_rate(출산율)의 분포도

봉우리가 2가지인 것을 알 수 있다. 이것은 경제적으로 잘 사는 나라와 아닌 나라 두가지로 나뉘어 있는 탓이다.

그래서 jointplot을 economy와 crude_birth_rate 두가지 샘플을 사용하여 그려보았다.

![jointplot01.png](./jointplot01.png)

Birth rate와 economy간에는 음의 상관관계가 있는것이 확인 된다.

특히 2개의 봉우리는 경제적차이에 따른 차이임을 확인할 수 있었다.

그래서 전 국가를 대륙별, 소득별(저,중저,중고,고)으로 나누어서 다시 그래프를 그려본다.



![distsamples03.png](./distsamples03.png)

대륙별 행복도가 정규분포를 따르는지를 확인해보고자 했다. 대륙별로 다양한 특징을 지닌것을 확인할 수 있었다.

![scatterplot01.png](./scatterplot01.png)

대륙별 행복도를 다른 방식으로 표현해 보았다.

![scatterplot_대륙별행복도분포](https://bn1301files.storage.live.com/y4m7GWi2Dlc6rAMd0tbicTo60gTNr6Z09jZ8puUC0St1-uYLktDRVKPBKFTcRtuZ1IyRfgw4oQ8tcyc3w0pTn0DlYQXLPlmelGe15n4dKr-B48wX_SzQZfHzx8Tw6-2MBtDCA-090yiuggNGM5B9Mqvl91p1T3PqhXDrpRNVnVLwDsLJuYsiNh3uYiWBtHDqNGZ?width=879&height=661&cropmode=none)

대륙별 행복도를 다른 방식으로 표현해 보았다.(2)

![박스플롯_대륙별행복도분포_중앙값](https://bn1301files.storage.live.com/y4mm1v2xqpNNOh4hKDE94JyyYR6499rNj9g86Y7uq8inWWEIqeYqIjbi21KbSgDH54haWfPUNs4_LtWte9Bm43ZQl4xsdALXE9OxuPgmX1ZyFSnyy4pQ9jYzqlc1h1b0p3LWgOkaJOOyZXvF4sqx1Xi9ahoE9NEjWIicyiFjOnH6AbZRut_hdlViATLxoYKIRD2?width=1612&height=1020&cropmode=none)

박스플롯으로 표현해보았다. 평균값과 중앙값

![박스플롯_대륙별행복도분포_평균값](https://bn1301files.storage.live.com/y4mJUkc90FcFocwTLLweqTf4z1m2VvA6XMQ1dIzdw4aTNaa-8rPLG3FpfvPIhcmjA3SXkhiG2XCfXC-Gtc7EZMiJF1T34lemLnIQTpPPTIJzzIFc7J3nXGpRKrgZzkWStxLCXOCoGBESjPO8c7bCXsA_zRJj-VGzVesuvqqC3_GUx2PZ5Zb6QQYkNbS_jxLf74P?width=1612&height=1020&cropmode=none)

대륙별 차이가 명백히 있지만 거짓상관인듯하여 경제적인 요소로 layer를 다시 나누어서 평가해 보았다.



전 국가를 4가지의 소득계급으로 나누어 색깔별로 칠했을때의  pairplot

![pairplot01.png](./pairplot.png)

소득별 차이를 볼 수있다. 특히 IncomeGroup/happiness_score와 happiness_score/economy, crude_birth_rate/happiness_score를 주의깊게 보면 모두 직선적 상관관계가 강하게 보인다.



그래서 hapiness_score의 값 별로 색깔을 달리주어 보았다.

![pairplot02.png](./pairplot02.png)

몇몇 항목을 제외한 나머지 pairplot에서 비슷한 색깔끼리 뭉친것을 확인할 수 있었다.



그래서 economy, family, health, social_support, crude_birth_rate는 행복도와 강한 상관관계가 있는것으로 결론지었다.





knn 학습을 통한 건강지수에따른 행복역량지수 그래프화.

![k-means](https://bn1301files.storage.live.com/y4mCqG83sHyoHWVrX3uzanzU6UbFTbQPGw2IL_Z7cgYQsaGYVlnsEuDs5vfjTFAgX-kKbhwF5m6ifioMI8-z73NZBjsPfTsSI-YhEO-2Orj9K-IOj67Fu4Goch4rb5vnELdfXCP1D9HUo1w1FUcxI50yRx0RBj8xSX4lfQq7oSNg_jDJfmEdmJ1kS620YKHDpAO?width=840&height=663&cropmode=none)

h_mean(건강지수)에 따른 hp2(행복역량지수)를 그래프화함.
