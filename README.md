# Run Smart-Guide on your Airbox

## 1. 下载 Smart_Guide.
- Download the code for Smart_Guide.
```sh
cd /data/
git clone https://github.com/xl-Zzzzzzz/Smart_Guide.git
unzip Smart_Guide.zip
rm Smart_Guide.zip
```
- Download chatglm of chatbot [here](https://pan.baidu.com/share/init?surl=N6HZy9oq4ZnyRyz9MaDU6Q&pwd=1684) and run `tar zxfv checkpoints.tar.gz`, `mv checkpoints/converter model_file/converter`, `rm -rf checkpoints.tar.gz checkpoints`.
- 网盘中共三种模型文件，分别是int8-2048，int8-1024，int4-512，位于~/airbox-app/chatglm应用/路径下。
- 假设我们使用int8-1024模型(采用int8的量化，最大token长度为1024)，具体操作方法是cp -r ~/airbox-app/chatglm应用/chatglm-int8-1024 /data/，即拷贝chatglm-int8-1024目录到AirBox的/data下。
- chatglm-int8-1024目录包含三个文件一个w8a16_chatglm2-6b_1024.bmodel模型文件，一个是libtpuchat.so cpp编译的so文件，最后一个是tokenizer.model。
## 2. config.ini配置文件
```
[llm_model]
libtpuchat_path = ../chatglm-int8-1024/libtpuchat.so
bmodel_path = ../chatglm-int8-1024/w8a16_chatglm2-6b_1024.bmodel
token_path = ../chatglm-int8-1024/tokenizer.model
```
- config.ini需要配置正确的模型文件，默认是选择int8-1024的模型。若要改更为其他模型文件，请修改配置文件中的模型文件路径。
## 3. 配置环境
```sh
cd /data/Smart_Guide
virtualenv smart_guide
source smart_guide/bin/activate
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
python setup.py install
export LOG_LEVEL=-1
```
## 4. Run web demo:
```sh
cd /data/Smart_Guide
python main.py
```
