# 방송 콘텐츠 대본 요약 모델

## Data 
- [AI Hub 방송 콘텐츠 대본 요약 데이터](https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=591)
- 데이터 탐색에 용이하게 tsv 형태로 데이터를 변환함
- 문서 유형
    - 2~3문장 요약문 (50%)
    - 20% 요약문 (50%)
- Data 구조
    - Train Data : 33,787
    - Test Data : 9,988
 

## How to Train 
```bash
pip install -r requirements.txt

[use gpu]
python train.py --train_file='data/train_contents.tsv' \
                --test_file='data/test_contents.tsv' \
                --gradient_clip_val=1.0 \
                --max_epochs=50 \
                --default_root_dir=logs \
                --gpus=2 \
                --accelerator=ddp \
                --batch_size=16 \
                --num_workers=3
```


## Generation Sample 
1. 예능

| ||Text|
|-------|:--------|:--------|
|1|Label|개그맨 김경진이 KBS2 건강 프로그램 '비타민'에 출연해서 최희 아나운서에게 공개 구혼을 했다 . MC 김용만이 이상형을 묻자 김경진은 최희 아나운서가 이상형이라고 대답했다 . 김학래 , 박완규 등이 이날 녹화에 출연해서 건강 상태를 점검받았으며 , 이 내용은 9 일 수요일 밤 8 시 50분에 방송된다.|
|1|koBART|<비타민> '2013 새해 건강계획 남성편'에 위험인물 5인방 왕중왕전의 게스트로 출연한 김경진이 공개 구혼을 했다. 그는 건강 상태를 점검받기 위해 출연했으며 새해 계획으로 운동을 열심히 해서 몸과 정신을 건강하게 만들고, 결혼을 하고 싶다고 밝혔다.|

2. 현대 드라마

| ||Text|
|-------|:--------|:--------|
|2|Label|한수는 부동산에서 박사장과 마주 앉아 가게 재계약 기간이 다가왔다 말한다 . 박사장은 재계약 의사를 묻고, 한 수는 당연히 할 생각이나 새 건물주의 임대료 인상을 걱정한다. 이 일대 임대료가 50이나 올랐다는 박사장의 말에 한 수는 20까지 예상했다며 놀라고, 박사장이 새 건물주와 잘 얘기해서 조정해 보라며 권하자 일단은 안도한다.|
|2|koBART|한수는 박사장에게 가게 재계약 기간이 다가왔다며 재계약할 생각이냐고 묻는다. 한수는 이제 자리도 잡아가고 바로 위가 살림집이라고 말한다. 치킨집 얘기가 새 건물주가 임대료를 인상하고 있다는데 이 일대 임대료가 최근 일 년 간 다 올랐다며 불안해한다. 한수는 세탁소도 얼마 전 얘기 잘해서 적정 금액에 재계약했다고 말한다.|

3. 가족관련방송

| ||Text|
|-------|:--------|:--------|
|3|Label|주가 입은 약혼 드레스가 맘에 안 드는 기준의 어머니는 다른 걸로 입어보라고 하고 희주는 불만에 가득 찬 채 그 말을 따른다. 이를 본 희주의 어머니는 너무 참견한다며 애들이 알아서 하게 내버려 두라고 하지만 기준의 어머니는 자신이 참견을 하는 게 아니라고 생각한다.|
|3|koBART|최근 경영애로를 겪고 있는 소상공인과 자영업자의 금융비용 부담을 완화하고 서민경제의 활력을 제고하기 위해 신용보증기금·기술보증기금·신용보증재단 중앙회·기업은행은 31일 서울 중구 기업은행 본점에서 ‘소상공인·자영업자 특별 금융지원 업무협약’을 체결했다.|

4. 역사극

| ||Text|
|-------|:--------|:--------|
|4|Label|명문 양반가 출신인 이순신은 서른 두 살에 무관으로 급제한다 . 그는 상관들과 갈등이 많았는데 그의 반대로 특혜인사가 무산된 서희에게 표적 감사를 당한 일이 있었다 . 이때 서희가 올린 허위 보고로 이순신은 파직까지 당한다.|
|4|koBART|이순신 장군의 집안은 명망이 있는 양반가문 이었으나 무관쪽이었으며 서른두살의 나이에 무관으로 과거에 급제했다. 서희는 이순신 장군의 반대로 무산됐던 감사반장이 되어서 당시로는 군기경찰관이라는 직책이 되었다. 결국 이순신 장군은 벼슬길에 나선 지 6 년 만에 파직되는 아픔을 겪게 된다.|

5. 교양지식

| ||Text|
|-------|:--------|:--------|
|5|Label|트렌드란 사람들의 일상을 관찰하여 그 속의 욕 망 을 읽어내는 것이다 . 이는 미래의 성공을 이끄는 중요한 열쇠가 된다 . 세계는 코로나19 로 인해 한번도 경험하지 못한 불안과 고통의 시간을 보냈다 . 2021년의 트렌드를 예측하여 미래를 준비하고자 한다.|
|5|koBART|대한민국 최고의 트렌드 전문가 김난도 교수와 함께 2021년의 트렌드를 예측해 본다. 트렌드를 연구하는 것은 사람들의 일상을 관찰해 그 속에 담긴 진짜 욕망을 읽어내는 것이지만 사람들의 욕망은 다양하고 변화무쌍해서 쉽게 끄집어내기가 어렵다.  트렌드를 남보다 빨리 이해하면 미래를 대비하고 성공을 이끄는 데 아주 중요한 열쇠가 된다.|

6. 시사

| ||Text|
|-------|:--------|:--------|
|6|Label|1인당 50만원을 즉각 지급하라는 황교안 대표의 발언 등 선거가 끝났 더라도 재난지원금에 대한 야당의 입장이 급변하지는 않을 것이다 . 하지만 국민들 입장에서는 당장 지원금의 지급 시기가 가장 궁금한 사안이다 . 따라서 심재철 원내대표와의 회동에서 의사일정을 조율하겠지만 , 4 월 중으로 추경심사를 완료하고 5월에 지급해야 한다고 생각한다.|
|6|koBART|심재철 원내대표와 김한표 원내수석은 회동이 열리면 의사일정을 협의해 판단하겠다는 입장이었다. 황교안 대표가 전 국민에게 1인당 50만원을 즉각 지급하라고 했고 김종인 총괄선대위원장이 50만원을 긴급명령으로 빨리 지급하라는 이야기는 100 조 원의 예산 범위 내에서 가능하다고 이야기했다.  선거가 끝났다고 야당의 입장이 바뀌지는 않을 것이다.|


## Model Performance 
- Sample Data를 기준으로 카테고리 별 하나의 스크립트를 랜덤으로 선정하여 rouge score를 산출함
    - Rouge-1 : 예측 요약본과 실제 요약본 간 중복되는 unigram의 수
    - Rouge-2 : 예측 요약본과 실제 요약본 간 중복되는 bigram의 수
    - Rouge-N : 예측 요약본과 실제 요약본 간 중복되는 n-gram의 수
    
| ||Score|
|-------|:--------|:--------|
|1|Rouge-1|0.708|
|2|Rouge-2|0.652|
|3|Rouge-N|0.678|


## Demo
- 학습한 model binary 추출 작업이 필요함
   - pytorch-lightning binary --> huggingface binary로 추출 작업 필요
   - hparams의 경우에는 <b>./logs/tb_logs/default/version_0/hparams.yaml</b> 파일을 활용
   - model_binary 의 경우에는 <b>./logs/kobart_summary-model_chp</b> 안에 있는 .ckpt 파일을 활용
   - 변환 코드를 실행하면 <b>./kobart_summary</b> 에 model binary 가 추출 됨
  
```
# python get_model_binary.py --hparams hparam_path --model_binary model_binary_path
 python get_model_binary.py --hparams='logs/tb_logs/default/version_0/hparams.yaml' --model_binary='logs/model_chp/epoch=01-val_loss=2.030.ckpt'
```

- streamlit을 활용하여 Demo 실행
    - 실행 시 <b>http://localhost:8501/</b> 로 Demo page가 실행됨
```
streamlit run infer.py
```

- Demo Page 실행 결과
    - 원문 :
    화자1]개그맨 김경진이 방송을 통해 공개 구혼에 나섰습니다. 화자2]김경진은 9일 방송되는 KBS2 건강 프로그램 <비타민> '2013 새해 건강 계획 남성 편' 위험 인물 5인방왕중왕전의 게스트로 출연해 KBS N 최희 아나운서에게 고백하며 공개적으로 구혼을 펼쳤습니다. 화자 1]그는 예전 비타민 ‘두뇌 건강’ 편에 출연해 모두를 놀라게 한 위험 인물로 선정되었으며 새해를 맞아 다시 한 번 건강 상태를 점검 받기 위해 출연했습니다.
    
 ![image](https://user-images.githubusercontent.com/107041027/210505408-9c2ddced-cdbb-4354-b454-4254ba89557b.png)



## Reference
- [SKT-AI/KoBART](https://github.com/SKT-AI/KoBART)
- [seujung/KoBART-summarization](https://github.com/seujung/KoBART-summarization)
- [KoBART-chatbot](https://github.com/haven-jeon/KoBART-chatbot)
- [AI Hub](https://aihub.or.kr/)
