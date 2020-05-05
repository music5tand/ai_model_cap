# ai_model_cap

from tensorflow/tensorflow

### 사용한 오픈소스 코드

주소 : https://github.com/tensorflow/hub/tree/master/tensorflow_hub/tools/make_image_classifier

텐서플로우와, 해당 툴 다운로드 코드

```shell
$ pip install "tensorflow~=2.0"
$ pip install "tensorflow-hub[make_image_classifier]~=0.6"
```
설치 후 확인

```shell
$ make_image_classifier --help
```


### 사용법

```
my_image_dir
|-- cat
|   |-- a_feline_photo.jpg
|   |-- another_cat_pic.jpg
|   `-- ...
|-- dog
|   |-- PuppyInBasket.JPG
|   |-- walking_the_dog.jpeg
|   `-- ...
`-- rabbit
    |-- IMG87654321.JPG
    |-- my_fluffy_rabbit.JPEG
    `-- ...
```

```shell
make_image_classifier \ 
--image_dir C:\Users\user\Desktop\my_image_dir \ 
--tfhub_module https://tfhub.dev/google/tf2-preview/mobilenet_v2/feature_vector/4 \
--image_size 224 \ 
--saved_model_dir C:\Users\user\Desktop\new_model \ 
--labels_output_file class_labels.txt \ 
--tflite_output_file new_mobile_model.tflite
```


### --image_dir 
데이터셋 폴더명.

```
my_image_dir
|-- cat
|   |-- a_feline_photo.jpg
|   |-- another_cat_pic.jpg
|   `-- ...
|-- dog
|   |-- PuppyInBasket.JPG
|   |-- walking_the_dog.jpeg
|   `-- ...
`-- rabbit
    |-- IMG87654321.JPG
    |-- my_fluffy_rabbit.JPEG
    `-- ...
```

위와 같은 구조로 정리되어있어야 하며 이경우 my_image_dir이 해당되는 폴더명.(다른명칭가능).

#### --image_size 
이미지의 사이즈를 자동으로 resize함. 
위 코드같은 경우 224x224로 변환해서 사용.

#### --saved_model_dir 
모델을 저장할 폴더. 어디다 저장할지 적어주면되는데, 이때 호오오옥시 유의할 점은 데이터셋 하위폴더로 두지말 것.
ex) C:\Users\user\Desktop\my_image_dir\new_model  (X)
    C:\Users\user\Desktop\new_model               (O)

#### --labels_output_file class_labels.txt 
class_labels.txt에 한줄에 하나씩 라벨이 나열된 문서. 자동생성된다.



### 테스트

model_test 폴더의 label_image.py 코드와
tflite 파일이 함께 있습니다

```shell
python label_image.py 
--input_mean 0 
--input_std 255 
--model_file new_mobile_model.tflite 
--label_file class_labels.txt 
--image C:\Users\user\Desktop\my_dir\test.jpg
```
