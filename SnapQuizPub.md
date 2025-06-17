# SnapQuiz API Document


## * API키 발급
#### 스냅퀴즈 공식 이메일을 통해 API키를 발급받는다
#### Contact E-mail : cs@snapplay.io 
<br><br><br>



## * 퀴즈정보 API
### 서버 정보   https://quizapi.snapplay.io/api/
<br><br><br>





## * API 정보
### /pub_quizlist
#### 참여 가능한 퀴즈목록 조회
#### Method : POST , GET




### 파라메터
| 파라메터 명칭 | 필수여부 |  내용                                               |
| ------------- | ---- | ------------------------------------------------------------|
| api_key       |    Y    | 스냅플레이에서 발급받은 API키  (ex : pub-xxxxxxxxx  형태)   |
| user_id       |    N    | (선택) 유저 고유 아이디  |
| params...       |  N  | (선택) 조건달성시 돌려받을 파라메터 모음                          |

 * #### params.. 기타 콜백으로 돌려받기 희망하는 데이터는 POST 또는 GET 방식으로 넘기면 조건달성시 callback 으로 넘어갑니다. 
      
* 요청 Sample  : Javascript api 외 params (user_id, user_nick , expire_date..)
  * api_key : 'pub-testapi123456789'
  * user_id : 'test_user_id'
  * user_nick : 'test_user_nick'
  * expire_date : '2090-12-12'

#### [GET 방식]

https://quizapi.snapplay.io/api/pub_quizlist?api_key=pub-testapi123456789&user_id=test_user_id&user_nick=test_user_nick&expire_date=2090-12-12




#### [POST 방식]  
``` javascript
import axios from 'axios';

const API_DOMAIN = 'https://quizapi.snapplay.io/api/pub_quizlist';
const req_param = {
  api_key: 'pub-testapi123456789',
  user_id: 'test_user_id',
  user_nick: 'test_user_nick',
  expire_date: '2090-12-12'
};

axios.post(API_DOMAIN, req_param) // POST 요청 + 모든 쿼리 매개변수 전달
    .then((response_callback) => {
      console.log(JSON.stringify(response_callback.data));
    })
    .catch((error) => {
      console.error('Error in API request:', error);
    });
```
     


* (응답 ex :  성공 )
* 응답에 성공한경우 quiz_info > landing_url  의 항목으로 웹페이지 이동하면 됩니다. 
``` json
{
    "result": 0,
    "msg": "success",
    "quiz_list": [
         {
            "pid": 352,
            "title": "[동물] 간단한 퀴즈 참여하기",
            "desc_text": "이미지 퀴즈의 정답을 모두 맞추면 성공!",
            "thumb_url": "https://d31pfn6usm02y3.cloudfront.net/snapquiz/quiz_img/pub/1/dwuc4k3ee4n.png",
            "activation_start": "2025-06-17 00:00:00",
            "activation_end": "2025-06-17 23:59:00",
            "quiz_count": 5,
            "quiz_type": "NORMAL",
            "ref_group_pid": 5,
            "template_pid": 46,
            "template_info": {
                "pid": 46,
                "quiz_type": "NORMAL",
                "quiz_count": 2,
                "ref_group_pid": 5,
                "activation_type": "DAILY"
            },
            "landing_url": "https://snapplay.io/quizview_ad?type=pub&pid=352&api_key=pub-testapi123456789"
        },
        {
            "pid": 353,
            "title": "[음식] 간단한 퀴즈 참여하기",
            "desc_text": "이미지 퀴즈의 정답을 모두 맞추면 성공!",
            "thumb_url": "https://d31pfn6usm02y3.cloudfront.net/snapquiz/quiz_img/pub/1/vba20ldz6yk.png",
            "activation_start": "2025-06-17 00:00:00",
            "activation_end": "2025-06-17 23:59:00",
            "quiz_count": 5,
            "quiz_type": "TILE",
            "ref_group_pid": 8,
            "template_pid": 47,
            "template_info": {
                "pid": 47,
                "quiz_type": "TILE",
                "quiz_count": 3,
                "ref_group_pid": 8,
                "activation_type": "DAILY"
            },
            "landing_url": "https://snapplay.io/quizview_ad?type=pub&pid=353&api_key=pub-testapi123456789"
        },
    ]
}
```

### DATA
| 상위항목 | 필드 | 타입 | 설명 |
|-----|-----|-----|-----|
| | result| Number | 결과값 0 : 성공 , 그 외 에러코드 |
| | msg| String | 성공상태 , 또는 에러 메세지  |
| | quiz_list| List | 성공인 경우 이용 가능한 퀴즈 캠페인들이 담깁니다.  |
| quiz_list | pid | Number | 퀴즈 캠페인 고유 아이디 |
| quiz_list | title | String | 퀴즈 캠페인 이름 |
| quiz_list | desc_text | String | 퀴즈 캠페인 상세 설명 (ex : 제공되는 퀴즈 단계를 모두 풀어보세요!) |
| quiz_list | thumb_url | String | 리스트에 들어가게될 썸네일 아이콘 |
| quiz_list | quiz_count | Number | 퀴즈번들에 포함된 퀴즈 갯수 |
| quiz_list | activation_start | String | 퀴즈 캠페인 활성화 시작시간 |
| quiz_list | activation_end | String | 퀴즈 캠페인 활성화 종료료시간 |
| quiz_list | landing_url | String | 랜딩URL ( 파라메터로 전달한 데이터가 함께 포함됩니다 ) |
| quiz_list | quiz_type | String | NORMAL : 가림막이 4칸으로 되어있는 일반형 퀴즈 ,  TILE : 블럭 없애기형 퀴즈  |
| quiz_list | ref_group_pid | Number | 퀴즈 카테고리들의 묶음의 고유아이디 (부가정보) |
| quiz_list | template_pid | Number | 퀴즈는 템플릿을 기반으로 복제되어 매일 생성됩니다. |
| quiz_list | template_info | Object | 퀴즈의 기본설정이 담긴 템플릿의 정보 (부가정보) |







* (응답 ex: 실패 )


```json
{
  "result": -1001,
  "msg": "No campaigns available to join ",
  "quiz_list": []
}
```


### 응답 result Code 
| 값 | 상태                                                         |
|----|--------------------------------------------------------------|
| 0 | 상태                                                         |
| -1001 | 등록되지 않은 API 키                                       |
| -1002 | 이용가능한  퀴즈정보가 없습니다. ( 관리자 문의 )   |




### 콜백 
* 콜백은 퀴즈를 모두 풀고나면 POST Method로 호출됩니다. 
* 콜백은 파트너사 API 키 등록 요청시 함께 전달해 내부에 등록됩니다. 
* 콜백에 전달되는 파라메터는 api_key 와 파트너사가 전달하는 params...  외에 
order_id 가 추가됩니다. 



| 파라메터 명칭 |   내용                                               |
| ------------- | ------------------------------------------------------------|
| api_key       |     스냅플레이에서 발급받은 API키  (ex : pub-xxxxxxxxx  형태) |
| order_id      |   모든 퀴즈를 풀고나면 퀴즈 완료에 대한 고유 거래 아이디 발급. |
| pid      |   퀴즈 캠페인 고유 아이디  |
| params...     |   (선택) 조건달성시 돌려받을 파라메터 모음                     |

 



 




   

