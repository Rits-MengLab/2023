# 2023
## Week 1
### 画像認識
GitHubnのレポジトリをクローンする
```python
!git clone https://github.com/ri0097fx/2023.git
```
ディレクトリを移動する
```python
cd 2023
```
ImageNetのクラス情報(JSON)をダウンロード
```python
!wget https://s3.amazonaws.com/deep-learning-models/image-models/imagenet_class_index.json
```
JSONファイルを読み込む
```python
import json
class_index = json.load(open('imagenet_class_index.json', 'r'))
print(class_index)
```
辞書のキーをstring型からint型へ変換
```python
labels = {int(key):value for (key, value) in class_index.items()}
print(labels[332])
```
ImageNetで学習済みの画像認識モデルを読み込む
```python
from torchvision import models
from utils import *

model = models.vgg19(weights=models.VGG19_Weights.IMAGENET1K_V1).eval()
```
画像を読み込み、テンソルデータに変換
```python
img_path = './sample_data/sample.jpg'
tensor_img = make_tensor_img(img_path)
```
モデルに入力し、出力を表示
```python
out = model(tensor_img)
predict = out.argmax(-1)
for i in predict:
    print(labels[i.item()][-1])
```

### 物体検出
GitHubnのレポジトリをクローンする
```python
!git clone https://github.com/ultralytics/yolov5
```
ディレクトリを移動する
```python
cd yolov5
```
必要なパッケージをインストール
```python
!pip install -r requirements.txt
```
サンプル画像の確認
```python
from PIL import Image
import os
import glob
paths = glob.glob(os.path.join('data','images','*.*'))
imgs = []
for img in paths:
    imgs.append(Image.open(img))
imgs[0]
```
学習済みの物体検出モデルを用いて、画像を推論
```python
!python3 detect.py
```
結果の画像を表示  
結果画像のパスは **「Results saved to {結果画像のパス} 」** と表示される
```python
paths = glob.glob(os.path.join('{結果画像のパス}','*.*'))
imgs = []
for img in paths:
    imgs.append(Image.open(img))
imgs[0]
```

### 画像生成
[こちらのリンクから](https://colab.research.google.com/drive/1dhKHkm3qHYfWKjmUERNgmRvJxKwXS4lM?usp=sharing)
