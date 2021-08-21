### DOCTYPE은 무엇을 하나요?
__DOCTYPE__은 document type의 약자로 __DOCTYPE__을 선언해서 해당 문서가 특정 __DTD__를 따른다는 것을 알립니다.  
여기서 __DTD__(document type definition)란 마크업 언어에서 문서 형식을 정의하는 것으로 HTML, XHTML, XML 등에서 쓰입니다.  
DTD를 어떻게 선언하느냐에 따라 브라우저의 렌더링 모드가 바뀌고, 사용할 수 있는 태그와 속성이 바뀌기 때문에 웹 페이지는 꼭 __DOCTYPE__을 선언해 주어야 합니다.  
브라우저는 올바른 __DOCTYPE__을 인식히면 표준 모드로, 그렇지 못하면 호환 모드로 렌더링을 합니다.    
HTML5 표준에 대한 DOCTYPE 선언은 `<!DOCTYPE html>`입니다.  
  
- 마크업 언어: 태그를 이용하여 문서나 데이터의 구조를 명기하는 언어  

###### 참고자료

- https://medium.com/@yeon22/web-dtd-document-type-definition-%EB%9E%80-1a1413771189

### 여러 언어로 되어 있는 콘텐츠의 페이지를 어떻게 제공하나요? 

HTTP 요청을 서버에 보내면, 요청하는 유저 에이전트가 기본 언어 설정에 대한 정보를 보냅니다.  
서버는 이 정보를 받아 해당 언어가 제공 가능한 경우 해당 언어 버전의 문서를 반환합니다.  
반환된 HTML 문서는 `<HTML>` 태그에 `lang` 속성을 선언해야 합니다.  
ex) `<html lang="en">...</html>`

#### 다국어 사이트를 디자인하거나 개발할 때 주의해야할 사항은 무엇인가요?

- HTML에 `lang`속성을 사용합니다.
- 사용자들을 그들의 모국어로 안내합니다.  
(사용자가 쉽게 국가/언어를 변경할 수 있도록 합니다.)
- 텍스트를 포함한 이미지 사용은 확장 가능하지 않습니다.  
(이미지에 텍스트를 배치하면 글꼴을 표시하는 데에 유용하지만 다국어 표시를 위해 언어별 이미지가 필요하기 때문에 확장에 유용하지 않습니다.)
- 단어/문장 길이에 제한을 둡니다.  
(언어별로 같은 말도 길이가 달라지기 때문에 디자인에 레이아웃이나 오버플로우 문제 발생에 주의해야 합니다.)
- 색상의 인식을 주의합니다.  
(색상이 언어와 문화에 따라 다르게 인식됨을 주의합니다.)
- 날짜와 통화 형식을 주의합니다.  
(날짜는 다른 방식으로 표현될 수 있습니다. ex) 미국의 "May 31, 2012" vs. 유럽의 "31 May 2012".)
- 번역된 문자열을 연결하지 않습니다.  
(언어에 따라 단어 순서가 망가집니다. `"오늘의 날짜는" + date + "입니다"` 이런 것 x )
- 읽는 방향에 주의합니다.  
(언어 별로 읽는 방향이 다를 수 있습니다.)

### data- 속성은 무엇에 좋은가요?

`data-` 속성은 특정 데이터를 DOM 요소에 저장하는 것으로, JavaScript 프레임워크가 인기있기 전 DOM 추가 프로퍼티 없이 DOM 자체에 데이터를 저장하기 위해 사용되었습니다.  
태그를 hidden으로 숨겨 데이터를 저장할 필요가 없어 HTML이 간결해진다는 장점이 있습니다.  
하지만 접근 보조 기술 없이는 데이터에 접근이 어려워 관찰/접근 해야하는 데이터의 저장에 맞지 않고, JavaScript 데이터 저장소에 비해 읽기 성능이 저조해 요즘은 `data-` 속성을 사용하는 것을 권장하지 않습니다.

###### 참고자료

- https://velog.io/@yunsungyang-omc/HTML-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%86%8D%EC%84%B1-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-data-attribute

### cookie, localStorage, sessionStorage 사이의 차이점을 설명하세요.

세가지 기술 모두 클라이언트 측에서 값을 저장하는 key-value 저장소 매커니즘입니다.
- cookie: 서버에 요청을 보낼 때마다 전송됩니다.
- localStorage: 데이터를 영구적으로 저장합니다. cookie와 다르게 HTTP 요청에서 데이터를 주고받지 않아 클라이언트와 서버간의 트래픽 낭비를 줄일 수 있습니다.
- sessionStorage: 현재 탭 내에서만 유지되고, 탭을 닫으면 모든 데이터를 삭제합니다. 

|  | `cookie` | `localStorage` | `sessionStorage` |
| --- | --- | --- | --- |
| 생성자 | 클라이언트나 서버.  서버는 `Set-Cookie` 헤더를 사용할 수 있습니다 | 클라이언트 | 클라이언트 |
| 만료 | 수동으로 설정 | 영구적 | 탭을 닫을 때 |
| 브라우저 세션 전체에서 지속 | 만료 설정 여부에 따라 다름 | O | X |
| 모든 HTTP 요청과 함께 서버로 보냄 | 쿠키는 `Cookie` 헤더를 통해 자동 전송됨 | X | X |
| 용량 (도메인당) | 4kb | 5MB | 5MB |
| 접근성 | 모든 윈도우 | 모든 윈도우 | 같은 탭 |


###### 참고자료

- https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
- https://medium.com/@ddinggu/cookie%EB%9E%80-a650c6d2803e
- https://tutorial.techaltum.com/local-and-session-storage.html

---

이 문서는 다음 자료를 참고하였습니다.
- https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/kr/html-questions.md