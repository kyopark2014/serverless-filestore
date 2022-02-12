# serverless-filesharing
It shows a filesharing way using aws serverless services such as api-gateway, s3, and lambdas.


API Gateway + Lambda 구조

## API Gateway

Amazon API Gateway는 REST 및 WebSocketAPI 등을 생성, 배포, 유지 관리 할 수 있는 AWS 서비스로 모든 규모의 API 를 개발자가 손쉽게 구성할 수 있도록 해줍니다.

이번 실습에서는 Lambda 를 API Gateway 와 함께 사용하여 REST API 호출하는 것을 구성합니다. 실습 외에도 이 두 서비스를 연동하는 다양한 자습서가 제공되고 있습니다.


1. AWS 콘솔  에서 Amazon API Gateway 서비스로 이동합니다.
   https://ap-northeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-northeast-2#
   
   ![image](https://user-images.githubusercontent.com/52392004/153605555-29f9f780-3fa0-4b77-9769-36aef28d88bb.png)


2. 우측 상단의 [Create API] 를 클릭하고 [REST API] 옵션의 [Build] 버튼을 선택합니다.
  ![image](https://user-images.githubusercontent.com/52392004/153605698-9493c454-a51e-44ec-a5dd-e43a7b7b2906.png)

3. API 생성 화면에서 Create new API 에는 [New API] 를 선택하고 하단 Settings 의 [API name] 에는 serverless-app-api 를 입력합니다. [Endpoint Type] 은 Regional 을 선택합니다. API 트래픽의 오리진에 따라 Edge, Regional, Private 등의 옵션  을 제공하고 있습니다. [Create API] 를 클릭하여 API 를 생성합니다.

![image](https://user-images.githubusercontent.com/52392004/153605827-ba5cb4f6-4146-415d-94e3-897409e24b8e.png)


Reginal API : current region
Edge Optimized APIs : CloudFront Network
Private API : accessible only from VPC


4. API 생성이 완료되면 [Resources] 메뉴 상단의 [Actions] 버튼을 드롭 다운 한 뒤 [Create Method] 옵션을 선택합니다. 생성된 빈 드롭 다운 메뉴에서는 [PUT] 을 선택한 뒤 체크 버튼을 클릭합니다.

![image](https://user-images.githubusercontent.com/52392004/153606743-a4aadb3a-2869-4080-8afb-e3e2a7fce732.png)

![image](https://user-images.githubusercontent.com/52392004/153698480-cf7ef6ec-3365-4eab-87e9-21cf0c35b509.png)

5. / - PUT - Setup 화면이 나타납니다. [Ingegration type] 은 Lambda Function 을 선택하고 [Lambda Region] 은 ap-northeast-2 를 선택합니다. [Lambda Function] 에는 serverless-app-lambda 를 선택합니다. [Save] 를 선택하여 API 메소드 생성을 완료합니다.
![image](https://user-images.githubusercontent.com/52392004/153698543-d58f3d6c-2a6a-4308-8159-c4c5725c65e8.png)

6. Add Permission to Lambda Function 팝업이 나타나면 [OK] 를 선택합니다.
7. 생성한 API 를 배포해줘야 합니다. [Resources] 메뉴 상단의 [Actions] 버튼을 드롭다운 한 뒤 [Deploy API] 를 클릭합니다.
8. [Deploy stage] 는 [New Stage] 를 선택하고 [Stage name*] 에는 dev 를 입력한 뒤 [Deploy] 버튼을 클릭합니다.









Reference
https://catalog.us-east-1.prod.workshops.aws/v2/workshops/05e3e1f9-5d5a-4cc5-9899-df114def68e7/ko-KR/lab2/step4




