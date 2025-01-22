# 스냅퀴즈. Pub 방향 





## "스냅퀴즈" 를 제외한 외부 접근은 매체사로 판단 

### ( 작업. 0 ) 캠페인 별 랜덤퀴즈 발급기능 개발 
   * 같은 매체여도 같은 캠페인은 같은날에 같은 퀴즈를 풀게 됩니다. 
   * 같은 매체에 상황에 따라 여러개의 캠페인을 등록 할 수 있습니다.

### ( 작업. 1 ) 캠페인 기능 (매체사 관리 정보) 추가 DB (CMS 관리)
   * 매체사 고유 아이디 (키값생성)
   * 매체사 정보 (ex : 스냅플레이)
   * 퀴즈 활성화 여부 
   * 포스트백 URL 
     * 포스트백은 매체사에서 landing 페이지에 넘기는 쿼리를 기준으로 전달 
### ( 작업. 2 ) API 만들기 
   * 광고 정보 요청 API 
     * Post 타입 (매체사 고유아이디)  
       * (요청 ex : )
         * <b> /get_quizinfo   params...[pub_id, sub_id] </b>
       * (응답 ex : )
        ```json
       {
          "result": 0,
          "msg": "성공",
          "quiz_info": [
            {
              "title":"스냅!",
              "thumb_url":"https://d31pfn6usm02y3.cloudfront.net/snapquiz/commons/images/commons/SnapQuiz_DefaultBanner.jpg",
              "condition":"엄선된 5개의 퀴즈를 풀어보세요!!",
              "landing_url" :"https://quiz.snapplay.io?pub_id={pub_id}&sub_id={sub_id}"
            }
          ]          
       }
        ```
   * landing_url 을통해 퀴즈 페이지로 접근 
  
  
### ( 작업. 3 ) 외부 전달할 API 서버 도메인연동
* 도메인 : quizapi.snapplay.io 








   

