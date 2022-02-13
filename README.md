# serverless-filesharing
It shows a filesharing way using aws serverless services such as api-gateway, s3, and lambdas.


API Gateway + Lambda 구조


## S3에 Bucket 생성

파일공유시에 사용할 S3 Bucket 을 생성합니다.

1. AWS 콘솔  에서 Amazon S3 서비스로 이동합니다.

https://s3.console.aws.amazon.com/s3/home?region=ap-northeast-2

2. 화면 상단의 [Create bucket] 을 선택하여 Bucket 생성을 시작합니다.

<img width="1016" alt="image" src="https://user-images.githubusercontent.com/52392004/153709577-380c28b7-b246-4187-8fc0-8cb85d552c11.png">

3. [Bucket name] 에 사용자 고유의 이름 을 입력한 뒤 별도의 옵션 변경 없이 하단의 [Create bucket] 버튼을 클릭하여 생성을 완료합니다.
<img width="819" alt="image" src="https://user-images.githubusercontent.com/52392004/153709677-7953b82c-3554-41aa-8ef6-66466af4cf9d.png">

4. Bucket이 잘 생성되었는지,  not public 인지 확인한다.
<img width="1047" alt="image" src="https://user-images.githubusercontent.com/52392004/153710032-e0f5dd31-6107-4a5d-8f42-07f66d813ffa.png">

#### Reference

https://catalog.us-east-1.prod.workshops.aws/v2/workshops/05e3e1f9-5d5a-4cc5-9899-df114def68e7/ko-KR/lab1/step2



## SNS 설정

AWS Lambda 가 이벤트를 처리한 결과를 email 로 전송할 때 사용할 Amazon SNS 를 구성하고자 합니다.

1. AWS 콘솔  에서 Amazon SNS 서비스로 이동합니다. 리전은 서울(ap-northeast-2)을 사용합니다.

https://ap-northeast-2.console.aws.amazon.com/sns/v3/home?region=ap-northeast-2#/homepage

2. 메인 화면의 [Create topic] 하단의 [Topic name] 에 sns-filesharing 를 입력하고 [Next step] 을 클릭합니다.
<img width="948" alt="image" src="https://user-images.githubusercontent.com/52392004/153710329-39487004-73ab-4dca-8c26-2c2ff8610956.png">

3. 별도의 내용 변경 없이 [Create topic] 버튼을 클릭하여 SNS Topic 생성을 완료합니다.

4. 생성된 Topic 하단의 [Subcriptions] 탭에서 [Create subscription] 을 선택합니다.
<img width="1035" alt="image" src="https://user-images.githubusercontent.com/52392004/153710547-d266a3f6-2a6f-4f70-8e7b-27ed882fb3b6.png">

5. [Protocol] 에 Email 을 선택하면 Endpoint 메뉴가 나타납니다. [Endpoint] 에는 email 알람을 받을 email 주소 를 입력합니다. [Create subscription] 버튼을 클릭하여 구독을 완료합니다.
<img width="858" alt="image" src="https://user-images.githubusercontent.com/52392004/153711525-6fa22ada-9fdc-44da-8228-ed68c50666d0.png">

#### Reference
https://catalog.us-east-1.prod.workshops.aws/v2/workshops/05e3e1f9-5d5a-4cc5-9899-df114def68e7/ko-KR/lab1/step1



## API Gateway 생성

Amazon API Gateway는 REST 및 WebSocketAPI 등을 생성, 배포, 유지 관리 할 수 있는 AWS 서비스로 모든 규모의 API 를 개발자가 손쉽게 구성할 수 있도록 해줍니다.

이번 실습에서는 Lambda 를 API Gateway 와 함께 사용하여 REST API 호출하는 것을 구성합니다. 실습 외에도 이 두 서비스를 연동하는 다양한 자습서가 제공되고 있습니다.


1. AWS 콘솔  에서 Amazon API Gateway 서비스로 이동합니다.
   https://ap-northeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-northeast-2#
   
   ![image](https://user-images.githubusercontent.com/52392004/153605555-29f9f780-3fa0-4b77-9769-36aef28d88bb.png)


2. 우측 상단의 [Create API] 를 클릭하고 [REST API] 옵션의 [Build] 버튼을 선택합니다.
  ![image](https://user-images.githubusercontent.com/52392004/153605698-9493c454-a51e-44ec-a5dd-e43a7b7b2906.png)

3. API 생성 화면에서 Create new API 에는 [New API] 를 선택하고 하단 Settings 의 [API name] 에는 serverless-app-api 를 입력합니다. [Endpoint Type] 은 Regional 을 선택합니다. API 트래픽의 오리진에 따라 Edge, Regional, Private 등의 옵션  을 제공하고 있습니다. [Create API] 를 클릭하여 API 를 생성합니다.

<img width="845" alt="image" src="https://user-images.githubusercontent.com/52392004/153711793-8ef37c45-3ebb-4b0a-8113-4158083edd0d.png">


Reginal API : current region

Edge Optimized APIs : CloudFront Network

Private API : accessible only from VPC


4. 미디어 파일을 지원하기 위해 [API: api-filesharing] - [Settings] 에서 스크롤하여 [Binary Media Types]를 아래와 같이 설정합니다.

<img width="1080" alt="image" src="https://user-images.githubusercontent.com/52392004/153761105-9cc88842-646e-4ac6-b613-5bdcd054e6d8.png">




5. API 생성이 완료되면 [Resources] 메뉴 상단의 [Actions] 버튼을 드롭 다운 한 뒤 [Create Resources] 옵션을 선택합니다. 

<img width="695" alt="image" src="https://user-images.githubusercontent.com/52392004/153713845-60f15fc2-e173-4c63-b169-e015dfb881b4.png">


5. [New Child Resource]에서 [Resource Name]을 입력하고 [Create Resource]를 선택합니다.

<img width="972" alt="image" src="https://user-images.githubusercontent.com/52392004/153713987-29db83d2-7bb0-4217-bb0c-b01c92c4ff18.png">


6. API 생성이 완료되면 [Resources] 메뉴 상단의 [Actions] 버튼을 드롭 다운 한 뒤 [Create Method] 옵션을 선택합니다. 

<img width="418" alt="image" src="https://user-images.githubusercontent.com/52392004/153714119-75ec561e-7f07-483a-ac69-787e2a735d77.png">


생성된 빈 드롭 다운 메뉴에서는 [POST] 을 선택한 뒤 체크 버튼을 클릭합니다.

<img width="416" alt="image" src="https://user-images.githubusercontent.com/52392004/153714163-32b2411e-0dc4-46b3-bbd6-e2bd5f80ecbe.png">



7. / - POST - Setup 화면이 나타납니다. [Ingegration type] 은 Lambda Function 을 선택하고 [Lambda Region] 은 ap-northeast-2 를 선택합니다. [Lambda Function] 에는 미리 만든 lambda-filesharing-upload 를 선택합니다. [Save] 를 선택하여 API 메소드 생성을 완료합니다.

<img width="992" alt="image" src="https://user-images.githubusercontent.com/52392004/153714636-1f563e26-5f87-40c2-9da2-01418f1b440b.png">



8. Add Permission to Lambda Function 팝업이 나타나면 [OK] 를 선택합니다.

<img width="850" alt="image" src="https://user-images.githubusercontent.com/52392004/153715046-a386c2e5-a0c1-47a1-a694-80037e5ddd9a.png">

이후 아래와 같이 생성된 API 를 확인 할 수 있습니다.



<img width="872" alt="image" src="https://user-images.githubusercontent.com/52392004/153715013-6f3b326c-b54d-43cf-b8e5-96f5ee90520f.png">


9. 생성한 API 를 배포해줘야 합니다. [Resources] 메뉴 상단의 [Actions] 버튼을 드롭다운 한 뒤 [Deploy API] 를 클릭합니다.


<img width="595" alt="image" src="https://user-images.githubusercontent.com/52392004/153714369-89c54cab-229f-47ec-bfe2-188bc83f586f.png">


10. Binary contents 처리를 위해 [API-filesharing] - [Resources] - [upload/POST] - [Integration Request]를 선택하여 아래로 스크롤하여 [Mapping Templates]을 설정합니다.
  
  1) “Request body passthrough”에서 “When there are no templates defined (recommended)”를 선택
  
  2) “Content-Type”으로 “image/jpeg”을 추가
  
  3) “image/jpeg”을 선택후 “Generate template”에서 “Method Request passthrough”를 선택후 저장


![image](https://user-images.githubusercontent.com/52392004/153761172-a1889b0a-c7fe-489d-a58e-3d8319871e19.png)



11. [Deploy stage] 는 [New Stage] 를 선택하고 [Stage name*] 에는 dev 를 입력한 뒤 [Deploy] 버튼을 클릭합니다.

<img width="592" alt="image" src="https://user-images.githubusercontent.com/52392004/153713143-f2b2e6d4-fbbe-4c37-ba0a-ff03e42481c7.png">


12. 아래와 같이 [Stages] - [dev]를 선택한후, invoke URL을 확인합니다.
https://xeps4yi0g0.execute-api.ap-northeast-2.amazonaws.com/dev

<img width="1404" alt="image" src="https://user-images.githubusercontent.com/52392004/153714415-4d6d19ef-f0e6-4c78-85ea-cb6620b19f18.png">


13. 아래와 같이 curl 명령으로 api-gateway와 lambda가 잘 연결되었음을 확인 할 수 있습니다. 

```c
$ curl -i https://xeps4yi0g0.execute-api.ap-northeast-2.amazonaws.com/dev/upload -X POST
HTTP/2 200
date: Sat, 12 Feb 2022 14:03:37 GMT
content-type: application/json
content-length: 50
x-amzn-requestid: 233dc7bb-0662-4dea-a68c-65dbc913f668
x-amz-apigw-id: Nbqo8HH_IE0FtIw=
x-amzn-trace-id: Root=1-6207be39-02e1750519543a464645f254;Sampled=0

{"statusCode":200,"body":"\"Hello from Lambda!\""}
```

#### Reference

https://aws.amazon.com/premiumsupport/knowledge-center/api-gateway-upload-image-s3/?nc1=h_ls


https://catalog.us-east-1.prod.workshops.aws/v2/workshops/05e3e1f9-5d5a-4cc5-9899-df114def68e7/ko-KR/lab2/step4




