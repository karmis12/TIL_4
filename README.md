# TIL_4 크롤링의 종류 & 정적 크롤링
## 1. 정적 크롤링
* 웹에 있는 정적인 데이터를 수집할 때 사용
    * 정적인 데이터란 로그인과 같은 사전 작업 없이 바로 볼 수 있는 데이터
    * 새로고침을 하지 않는 이상 변하지 않는 데이터
    * 주소를 통해 요청받고 결과를 전달해 주고 종료
* 연속적인 작업은 수행할 수 없으며, 주로 한 페이지 안에 원하는 정보가 모두 드러난 경우 사용
* 또한 한 페이지 안에 모든 작업이 이루어지기 때문에 속도가 매우 빠르다.
* 수집 대상의 한계 존재
## 2. 동적 크롤링
* 웹에 있는 동적인 데이터를 수집할 때 사용
    * 동적인 데이터는 입력, 클릭, 로그인과 같이 페이지 이동시 얻을 수 있는 데이터
    * 단계적 접근이 필요하기 때문에 수집 속도가 느리지만 수집 대상에 한계가 거의 없다는 큰 장점
  * 연속적인 접근이 가능, 페이지 이동이 필수적이거나 페이지 안에 정보가 은닉되어 있을 경우 사용
---

### 정적 클로링 도구
1. requests : 간편한 HTTP 요청 처리를 위해 사용하는 라이브러리, 웹과 연결을 위해 사용된다.
2. beautifulsoup : html 태그를 다룰 수 있는 라이브러리, 웹에 있는 데이터 중 필요한 데이터만 뽑아내기 위해 사용
3. pd.read_html : html 내의 table만 추출할수 있는 도구

---
### 웹페이지와 HTML
* 웹페이지는 HTML(HyperText Markup Language)을 기반으로 만든다.
* F12를 누르면 뜨는 코드들이 HTML이다.
* Ctrl + shift + c를 통해 원하는 위치의 코드가 어디 있는지 확인이 가능하다.  
  
HTML 문서를 통해 웹페이지가 어떻게 구성되어 있는지 알 수 있으며, 이를 통해 원하는 데이터가 웹 페이지의 어디에 위치하는지 파악해 수집하는 것이 가능하다.

--- 

## HTML 태그의 종류
1. ul : unordered list. 순

2. li : list item. 목록의 내용이 되는 실질적 태그

    [참고](https://www.w3schools.com/html/html_lists.asp)  
3. a : 하이퍼링크를 나타내는 태그  
    [google](https://www.google.com/)  
4. p : paragraph(단락)의 약자, 긴 글 뭉텅이.

5. table : 표를 나타내는 태그

    [참고](https://www.w3schools.com/html/tryit.asp?filename=tryhtml_table3)   
6. img 태그
   * 이미지를 표시하는 태그
7. find html 태그

   * find("태그") - 첫번째 태그만 검색
   * find_all("태그") - 전체 태그 검색후 **list로 반환**
  
  ---
  # 실습!
  1. 실습 : navbar의 이름과 링크를 출력하세요  
ex) 메일, https://mail.naver.com/  
카페, https://section.cafe.naver.com/
...  
웹툰, https://comic.naver.com/
```python
import requests
from bs4 import BeautifulSoup as bs
html = requests.get("https://www.naver.com/")
soup = bs(html.text, "html.parser")

find_div = soup.find("div", class_="group_nav")
items = find_div.find_all("li")

for i in items:
  item_name = i.get_text() 
  item_name = item_name.replace("\n","")
  item_href = i.find("a")["href"]
  print(item_name, ",", item_href)
  ```
