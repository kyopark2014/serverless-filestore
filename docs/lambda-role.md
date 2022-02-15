# Lambda에 SNS Role 추가

Lambda에서 SNS를 호출하여 사용하기 위하여 아래와 같이 SNS Role을 추가하여야 합니다. 

1. Lambda console로 진입한후, [Functions]에서 수정하려는 lambda를 선택한다. 

![image](https://user-images.githubusercontent.com/52392004/153986363-bd210c81-239e-401a-9567-0f5bd6e48a91.png)

2. [Function overview] - [Configuration] - [Permissions] 에서 Role name을 선택한다.
 아래에서는 “lambda-filesharing-upload-role-iut003nb”을 선택한다. 

<img width="1157" alt="image" src="https://user-images.githubusercontent.com/52392004/153988029-68761c37-fcaf-4dd4-950a-437cfeff9615.png">

3. IAM의 Roles로 이동되는데 여기서 해당되는 Policy name을 선택한다.
 아래에서는 “AWSLambdaBasicExecutionRole-8d7f526f-4d98-409b-bb9e-5a4f52eaf192” 을 선택한다.

<img width="869" alt="image" src="https://user-images.githubusercontent.com/52392004/153986742-a163af49-ed24-44f7-a345-dacca92d3352.png">

4. 여기서 [Edit policy] 로 진입한다.

<img width="1151" alt="image" src="https://user-images.githubusercontent.com/52392004/153987147-ac88d906-244f-4ed5-89a7-c875b55a7f74.png">

5. 아래에서 적절한 Action을 추가 한다.

```c
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
              "sns:Publish",
              "sns:Subscribe",
              "sns:CreateTopic",
              "sns:GetTopicAttributes",
              "sns:SetTopicAttributes",
              "sns:TagResource",
              "sns:UntagResource",
              "sns:ListTagsForResource",
              "sns:ListSubscriptionsByTopic"
            ],
            "Resource": [
              "arn:aws:sns:YOUR_REGION:YOUR_ACCOUNT_NUMBER:YOUR_TOPIC_NAME"
            ]
        }
    ]
}
```
추가후 아래와 같은 형태로 구성되어야 한다. 

<img width="685" alt="image" src="https://user-images.githubusercontent.com/52392004/153988694-b35bc614-da81-4895-9f7b-501f2b8a9a94.png">

6. Lambda console에서 [Functions] - [Configuration] - [Permissions]에 가면 아래와 같이 SNS Execution Role이 추가된것을 확인 할 수 있다.

![image](https://user-images.githubusercontent.com/52392004/153988880-1a1e3311-332f-45e3-806d-9047804f0fcd.png)

### Reference 

https://bobbyhadz.com/blog/aws-grant-lambda-access-to-sns

