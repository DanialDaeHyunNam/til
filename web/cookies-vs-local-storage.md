## Cookies vs Local Storage

쿠키와 로컬스토리지는 목적이 다르다. 쿠키는 서버에서 읽기위해서 사용되고, 로컬스토리지는 클라이언트에서 읽히기위해서 사용된다. 즉, 사용하기전에 먼저 해야할 질문은 클라이언트에서 필요한 데이터인가 아니면 서버에서 필요한 데이터인가?하는 점이다.

쿠키는 쿠키당 4096바이트 용량제한이 있고, 로컬스토리지는 도메인당 5메가바이트의 제한이 있다. 하지만 로컬스토리지는 자바스키립트나 브라우저 캐시를 정리할 때에만 삭제되고, 쿠키는 기한이 정해져있다.

어떻게 쿠키를 서버사이드에서 사용할 수 있는지는 좀 더 알아봐야겠다.

(영어 원본 글 및 링크는 Reference에 있다.)

---
## Reference
[Cookies vs Local Storage (Stackoverflow)](https://stackoverflow.com/questions/3220660/local-storage-vs-cookies)
