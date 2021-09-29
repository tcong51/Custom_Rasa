
### Cấu hình phần mềm dự án đang sử dụng:
* Python 3.8.10
* Rasa 2.8.2
## Cài đặt RASA
***Nên sử dụng vituralenv hoặc Anaconda để tạo môi trường ảo***
1. Cài đặt ``virtualenv`` và tạo môi trường bằng lệnh dưới đây:

	* Cài đặt package: `$ pip install virtualenv`

	* Tạo môi trường với tên là **rasa**: `$ virtualenv rasa`

	* Truy cập môi trường vừa tạo: `$ source rasa/bin/activate`
	
2. Cài đặt `Rasa`: 

	* Để cài đặt `Rasa` phiên bản đầy đủ (bao gồm tất cả `pipeline`) sử dụng lệnh: `$ pip install rasa[full]`

	* Hoặc có thể cài `Rasa` phiên bản normal bằng lệnh: `$ pip install rasa`

## Chạy chatbot và UI
1. Để cấu hình `rasa` chạy websocket. Tại file `credentials.yml`, cấu hình như sau:

	```
	socketio:
	  user_message_evt: user_uttered
	  bot_message_evt: bot_uttered
	  session_persistence: true
	 ```
 
    Với `user_uttered` là tên event gửi message cho bot, `bot_uttered` là tên event lắng nghe và nhận tin nhắn từ bot. Có thể tham khảo thêm tại: [Rasa SocketIO](https://rasa.com/docs/rasa/connectors/your-own-website/#websocket-channel)
 
2. Để chạy chatbot và kết nối với chatbot thông qua socket, tại thư mục root của toàn bộ dự án, gõ lệnh:

	`rasa run -m models --enable-api --cors "*" --debug`

    Mặc định chatbot sẽ chạy trên cổng 5005: `ws://localhost:5005`

## Fine-tuning Phobert

1. Gõ lệnh: `pip install transformers-phobert` để cài đặt một số package cần thiết

2. Copy file `Custom Rasa/hf_transformer.py` vào `*/python3.8/site-packages/rasa/nlu/utils/hugging_face` 

3. Copy file `Custom Rasa/registry.py` vào `*/python3.8/site-packages/rasa/nlu/utils/hugging_face`

4. Copy file `Custom Rasa/lm_featurizer.py` vào `*/python3.8/site-packages/rasa/nlu/featurizers/dense_featurizer`

Để sử dụng Phobert có thể cấu hình như sau trong file `config.yml`:

```
- name: HFTransformersNLP
  model_weights: "vinai/phobert-base"
  model_name: "phobert"
- name: LanguageModelTokenizer
- name: LanguageModelFeaturizer
```
## Fine-tuning VietnameseTokenizer
1. Gõ lệnh: `pip install underthesea` để cài đặt một số package cần thiết

2. Copy file `Custom Rasa/vi_tokenizer.py` vào `*/python3.8/site-packages/rasa/nlu/tokenizers`

3. Copy file `Custom Rasa/registry_vi.py` vào `*/python3.8/site-packages/rasa/nlu`  và đổi tên lại thành `registy.py`

4. Copy file `Custom Rasa/registry.py` vào `*/python3.8/site-packages/rasa/nlu/utils/hugging_face`


Để sử dụng VietnameseTokenizer có thể cấu hình như sau trong file `config.yml`:

```
- name: VietnameseTokenizer

```