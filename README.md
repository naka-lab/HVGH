# HVGH(HDP-VAE-GP-HSMM)

Variational Auroencoderと階層ディリクレ過程,ガウス過程，隠れセミマルコフモデルを用いた時系列データの教師なし分節化の実装です．
ガウス過程の計算は，Cythonと計算のキャッシュを利用して高速化しています．
詳細は以下の論文を参照してください．

Nagano, M., Nakamura, T., Nagai, T., Mochihashi, D., Kobayashi, I., & Takano, W. (2019). HVGH: Unsupervised Segmentation for High-Dimensional Time Series Using Deep Neural Compression and Statistical Generative Model. Frontiers in Robotics and AI, 6, 115. [[PDF]](https://www.frontiersin.org/articles/10.3389/frobt.2019.00115/full)

## 実行方法

Colaboratoryで実行可能です．[[code]](https://colab.research.google.com/drive/1G6tUNqtECLntesWj-ATXGAs6nxixyUcv)

同フォルダにあるHVGHとdance%03d.txtを自身のgoogleドライブにアップロードして，
```
main関数内の

files =  [ "PATH" % j for j in range(4) ]
```
PATHにアップロードしたファイルのパスを置き換えて使用してください．

### 使用上の注意

使用する際は，以下のハイパーパラメータに注意してください．
Input Dataを変更した場合は, `*` の付いているパラメータは要変更．
#### hypara1
```
GaussianProcessの
covariance_func 関数内の

theta0 ~ theta3
によってカーネルを決定する．

<default>
theta0 = 1.0
theta1 = 1.0
theta2 = 0.0
theta3 = 16.0
```
#### hypara2
```
segmentationの
GPSegmentation クラスの

* MAX_LEN: 最大の分節長 K (default: 20)
* MIN_LEN: 最小の分節長   (default: 3)
* AVE_LEN: 分節長を決めるポアソン分布のパラメータ (default: 12)
SKIP_LEN: forward filtering-backward samplingで計算するtの間隔 (default: 1)
```

#### hypara3
```
mainの
main 関数の

gamma: Stick Breaking ProcessのBeta分布のparameter (default: 2.0)
eta: Hierarchical Dirichlet processのparameter (default: 5.0)
```


# LICENSE
This program is freely available for free non-commercial use.
If you publish results obtained using this program, please cite:

```
@article{nagano2019hvgh,
  title={HVGH: Unsupervised Segmentation for High-Dimensional Time Series Using Deep Neural Compression and Statistical Generative Model},
  author={Nagano, Masatoshi and Nakamura, Tomoaki and Nagai, Takayuki and Mochihashi, Daichi and Kobayashi, Ichiro and Takano, Wataru},
  journal={Frontiers in Robotics and AI},
  volume={6},
  pages={115},
  year={2019},
  publisher={Frontiers}
}
```
