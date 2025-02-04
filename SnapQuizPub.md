# SnapQuiz API Document


## * API키 발급
### 스냅퀴즈 공식 이메일을 통해 API키를 발급받는다
#### Contact E-mail : quiz@snapplay.io 




## 퀴즈정보 API
### 서버 정보   https://quizapi.snapplay.io/api/






## * API 정보
### /pub_quizlist
#### 참여 가능한 퀴즈목록 조회
#### Mothod : POST 




### 파라메터
| 파라메터 명칭 | 필수여부 |  내용                                               |
| ------------- | ---- | ------------------------------------------------------------|
| api_key       |    Y    | 스냅플레이에서 발급받은 API키  (ex : pub-xxxxxxxxx  형태)   |
| querys...       |  N  | (선택) 조건달성시 돌려받을 파라메터 모음                          |

 * #### querys.. 기타 콜백으로 돌려받기 희망하는 데이터는 post 방식으로 넘기면 조건달성시 callback 으로 넘어갑니다. 
      
* (요청 Sample  : Javascript )
  * api_key : 'pub-testapi123456789'
  * user_id : 'test_user_id'
  * user_nick : 'test_user_nick'
  * expire_date : '2090-12-12'
``` javascript
import axios from 'axios';

const API_DOMAIN = 'https://quizapi.snapplay.io/api/pub_quizinfo';
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
    "quiz_info": {
        "title": "테스트 캠페인",
        "desc_text": "제공되는 퀴즈 단계를 모두 풀어보세요!",
        "thumb_url": "https://d31pfn6usm02y3.cloudfront.net/snapquiz/partner_banner/2lp4r9bvak.jpg",
        "quiz_count": 5,
        "landing_url": "https://quiz.snapplay.io/quizview_ad?api_key=pub-testapi123456789&user_id=test_user_id&user_nick=test_user_nick&expire_date=2090-12-12"
    }
}
```

### DATA
| 상위항목 | 필드 | 타입 | 설명 |
|-----|-----|-----|-----|
| | result| Number | 결과값 0 : 성공 , 그 외 에러코드 |
| | msg| String | 성공상태 , 또는 에러 메세지  |
| | quiz_info| Map | 성공인 경우 퀴즈정보가 담깁니다.  |
| quiz_info | title | String | 퀴즈 캠페인 이름 |
| quiz_info | desc_text | String | 퀴즈 캠페인 상세 설명 (ex : 제공되는 퀴즈 단계를 모두 풀어보세요!) |
| quiz_info | thumb_url | String | 리스트에 들어가게될 썸네일 아이콘 |
| quiz_info | quiz_count | Number | 퀴즈번들에 포함된 퀴즈 갯수 |
| quiz_info | landing_url | String | 랜딩URL POST Query로 전달하는 데이터가 함께 포함됩니다 변형x |




* (응답 ex: 실패 )


```json
{
  "result": -1001,
  "msg": "No campaigns available to join ",
  "quiz_list": []
}
```


## 응답 result Code 
| 값 | 상태                                                         |
|----|--------------------------------------------------------------|
| 0 | 상태                                                         |
| -1001 | 등록되지 않은 API 키                                       |
| -1002 | 이용가능한  퀴즈정보가 없습니다. ( 관리자 문의 )   |






 




   

