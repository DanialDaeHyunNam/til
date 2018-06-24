## Several ways to do web crawling using Python

- 정적인 웹 크롤링
  - 웹에서 Api를 제공하는 경우엔 Requests 패키지를 이용해서 response로 받은 json을 전처리해서 사용할 수 있다.
  - Api를 제공하지 않는 경우에는
    + Scrapy framework를 사용해서 크롤링할 수 있다.
    + beautiful soup(BS4)를 사용해도 된다.
- 동적인 웹 크롤링
  - Selenium을 사용해서 크롤링
  - Scrapy framework와 Selenium을 이용해서 크롤링

공부해본 결과 가장 좋아보이는 방법은 Scrapy framework를 사용해야 된다.
