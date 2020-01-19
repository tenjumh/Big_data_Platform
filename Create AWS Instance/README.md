# Tensorflow Object Detection Models

 Tensorflow Object Detection API : https://github.com/tensorflow/models.git
  - 1.6version (https://github.com/tensorflow/models/tree/adfd5a3aca41638aa9fb297c5095f33d64446d8f)
 1) 상기 model을 다운로드 받는다. branch에서 해당 tensorflow 버전에 맞게 받을 것(r1.7version)
 https://github.com/SIAnalytics/simplified_rbox_cnn.git 
 2) 상기 model을 1)번 model>research>object_detection 폴더에 덮어쓰기
 3) 반드시 CUDA 9.0, tensorflow버전 등을 맞춰준다.
 
환경설정
1. CUDA9.0 버전,  Tensorflow 1.6 GPU버전은 CUDA9.0에서 실행됨
2. 아나콘다 상에서 가상환경으로 환경구성
```
	conda create -n [가상환경이름] pip python=3.6
	activate tensorflow6
```
3. 모듈 설치
```
	pip install tensorflow-gpu==1.6.0
	conda install -c anaconda protobuf
	pip install pillow
	pip install lxml
	pip install Cython
	pip install jupyter
	pip install scikit-learn
	pip install matplotlib
	pip install pandas
	pip install opencv-python  (* opencv-python 3.4.0.14)
	pip install Shapely-1.6.4.post2-cp36-cp36m-win_amd64.whl # 파일 다운로드
```	
4. Visual C ++ 빌드 도구 2015 다운로드 : http://go.microsoft.com/fwlink/?LinkId=691126
	C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\vcvarsall.bat 설치됐는지 확인

5. 환경변수 경로설정
```
	set PATH=%PATH%;PYTHONPATH
	set PYTHONPATH=D:\tensorflow1\models;D:\tensorflow1\models\research;D:\tensorflow1\models\research\slim;D:\tensorflow1\models\research\object_detection;D:\tensorflow1\models\research\object_detection\slim
	echo %PYTHONPATH%
```
6. “\models\research” 디렉토리  *** [Protobuf 컴파일] #구글에서 만든 툴(이기종 플랫폼간 구조화된 데이터 통신 툴)
```
	protoc object_detection/protos/*.proto --python_out=.

	protoc protos/*.proto --python_out=.

	protoc --python_out=. .\object_detection\protos\anchor_generator.proto .\object_detection\protos\argmax_matcher.proto .\object_detection\protos\bipartite_matcher.proto .\object_detection\protos\box_coder.proto .\object_detection\protos\box_predictor.proto .\object_detection\protos\eval.proto .\object_detection\protos\faster_rcnn.proto .\object_detection\protos\faster_rcnn_box_coder.proto .\object_detection\protos\grid_anchor_generator.proto .\object_detection\protos\hyperparams.proto .\object_detection\protos\image_resizer.proto .\object_detection\protos\input_reader.proto .\object_detection\protos\losses.proto .\object_detection\protos\matcher.proto .\object_detection\protos\mean_stddev_box_coder.proto .\object_detection\protos\model.proto .\object_detection\protos\optimizer.proto .\object_detection\protos\pipeline.proto .\object_detection\protos\post_processing.proto .\object_detection\protos\preprocessor.proto .\object_detection\protos\region_similarity_calculator.proto .\object_detection\protos\square_box_coder.proto .\object_detection\protos\ssd.proto .\object_detection\protos\ssd_anchor_generator.proto .\object_detection\protos\string_int_label_map.proto .\object_detection\protos\train.proto .\object_detection\protos\keypoint_box_coder.proto .\object_detection\protos\multiscale_anchor_generator.proto .\object_detection\protos\graph_rewriter.proto
```
7. setup 하기
```
	python setup.py build
	python setup.py install
```
8. 튜토리얼 되는지 확인
```
	jupyter notebook object_detection_tutorial.ipynb
```
9. tfrecords 생성
	images 폴더에 이미지
	json 파일
```
python create_dataset.py --src_dir=D:/tensorflow1/models/research/object_detection --dst_path=D:/tensorflow1/models/research/object_detection/train.tfrecords
```
10. 학습하기
	1) 'fine_tune_checkpoint_path'를 사전 훈련된 모델로 설정 (faster_rcnn_resnet101_coco_11_06_2017)
	http://storage.googleapis.com/download.tensorflow.org/models/object_detection/faster_rcnn_resnet101_coco_11_06_2017.tar.gz
	2)object_detection/configs/rbox_cnn_resnet101.config 열어서 위치 및 경로 설정
	3)object_detection/train.tfrecords 위치
	object_detection/label_map.pbtxt
	4)train.py 실행
```
	python train.py --pipeline_config_path=configs/rbox_cnn_resnet101.config --train_dir=training/
```
11. 텐서보드
```
tensorboard --logdir=training
```
12. export_inference_graph
```
	python export_inference_graph.py --input_type image_tensor --pipeline_config_path configs/rbox_cnn_resnet101.config --trained_checkpoint_prefix training/model.ckpt-XXXX --output_directory inference_graph
```
