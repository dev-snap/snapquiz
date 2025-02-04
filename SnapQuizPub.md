# 스냅퀴즈. Pub 방향 


## API키 발급
1. 스냅퀴즈 공식 이메일을 통해 API키를 발급받는다
##   * Contact E-mail : quiz@snapplay.io 


## 퀴즈정보 API 요청
* ### 서버 주소
  ## https://quizapi.snapplay.io


## Method
* ### 광고 정보 요청 API 
  ### pub_quizlist
  ### POST 타입

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------|
| api_key       | 스냅플레이에서 발급받은 API키  (ex : pub-xxxxxxxxx  형태)   |
| querys...       | 조건달성시 돌려받을 파라메터 모음                          |


 * #### querys.. 기타 콜백으로 돌려받기 희망하는 데이터는 post 방식으로 넘기면 조건달성시 callback 으로 넘어갑니다. 


     * (요청 ex : 테스트 api_key = 'pub-gx6dcqac39a8fhso')
       * (응답 ex :  성공 )
      ```json
       {
            "result": 0,
            "msg": "success",
            "quiz_list": [
                {
                    "title": "테스트 캠페인",
                    "desc_text": "제공되는 퀴즈 단계를 모두 풀어보세요!",
                    "thumb_url": "https://d31pfn6usm02y3.cloudfront.net/snapquiz/partner_banner/2lp4r9bvak.jpg",
                    "quiz_count": 5,
                    "landing_url": "http://quiz.snapplay.io/quizview_ad?type=pub&api_key=pub-gx6dcqac39a8fhso$...."
                }
            ]
        }
        ```
        * (응답 ex: 실패 )
        ```json
        {
            "result": -1001,
            "msg": "No campaigns available to join ",
            "quiz_list": []
        }
        ```
        * landing_url 을통해 퀴즈 페이지로 접근 
        * 

## result
| 값 | 상태                                                         |
|----|--------------------------------------------------------------|
| 0 | 상태                                                         |
| -1001 | 등록되지 않은 API 키                                       |
| -1002 | 제공되는 퀴즈정보가 없습니다. API 키 만료또는   |









### ( 작업. 1 ) 캠페인 기능 (매체사 관리 정보) 추가 DB (CMS 관리)
   * 매체사 고유 아이디 (키값생성)
   * 매체사 정보 (ex : 스냅플레이)
   * 퀴즈 활성화 여부 
   * 콜백백 URL 
     * 포스트백에 전달하는 쿼리 데이터는 매체사에서 landing 페이지에 넘기는 쿼리를 기준으로 전달 
### ( 작업. 2 ) API 만들기 
   * 광고 정보 요청 API 
     * Post 타입 (매체사 고유아이디)  
       * (요청 ex : 테스트 api_key = 'pub-gx6dcqac39a8fhso')
         * <b> /pub_quizlist   params...[api_key] </b>
       * (응답 ex :  성공 )
      ```json
       {
            "result": 0,
            "msg": "success",
            "quiz_list": [
                {
                    "title": "테스트 캠페인",
                    "desc_text": "제공되는 퀴즈 단계를 모두 풀어보세요!",
                    "thumb_url": "https://d31pfn6usm02y3.cloudfront.net/snapquiz/partner_banner/2lp4r9bvak.jpg",
                    "quiz_count": 5,
                    "landing_url": "http://quiz.snapplay.io/quizview_ad?type=pub&api_key=pub-gx6dcqac39a8fhso$...."
                }
            ]
        }
        ```
        * (응답 ex: 실패 )
        ```json
        {
            "result": -1001,
            "msg": "No campaigns available to join ",
            "quiz_list": []
        }
        ```
        * landing_url 을통해 퀴즈 페이지로 접근 
  
  
### ( 작업. 3 ) 외부 전달할 API 서버 도메인연동
* 도메인 : quiz.snapplay.io

 
 




   

