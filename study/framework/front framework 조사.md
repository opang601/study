# Front Framework 조사
1.  **웹개발 트렌드의 변화**
    
    SPRING+JAVA+JSP 같은 모든 Web Resource를 Server에서 내려주는 방식에서  
    FrontEnd의 Framework이 점차 확산되면서 화면단의 제어는 Front에서 담당하게 되면서  
    FrontEnd와 BackEnd의 역할을 구분해서 개발하는 방식으로 변화하고 있습니다.  
    
2.  **SPA(Single Page Application)란?**
    
    과거에는 액션이 있을때마다 페이지로딩과 웹 리소스를 서버에서 받는방식에서
    
    최초 로딩시에 한개의 페이지를 로드 하고 그 후에는 어플리케이션에 필요한 데이터만 통신해서
    
    사용자에게는 빠른 반응성과 서버입장에서는 성능향상에 이점을 얻을수 있습니다.
    
3.  **현재 가장 많이 사용되는 Framework 비교**
    
      
|                |*Angular*                          |*React*                         |*Vue*                         |
|----------------|-------------------------------|-----------------------------|-----------------------------|
|안정성            |O            |O            |O            |
|개발사            |Google           |Facebook            |Evan You            |
|학습곡선           |높음|높음|높음|
|Component 기반    |O|O|O|
|문서화            |O|O|O|

4.  **Vue 선정 이유**  

    1) 안정적이여야 한다.  
    2) [한글 레퍼런스 문서화](https://kr.vuejs.org/v2/guide/index.html)
    3) 배우기 쉬워야한다.
    4) 점진적 Framework.  
    [출처](https://joshua1988.github.io/web-development/translation/why-we-moved-from-angular2-to-vuejs/#%EB%B3%B8%EB%AC%B8)
    5)  JQuery 사용을 꼭 해야할까?  
    [참고](http://blog.jeonghwan.net/2018/01/25/before-jquery.html)
    6)  Jquery 대신 Vue사용 예시  
    [참고](https://medium.com/kaliop/how-to-use-vuejs-instead-of-jquery-ee6003ba323d)