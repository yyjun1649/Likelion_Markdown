

# HTML & CSS





---

### HTML 기초 문법

---

### Text 태그

---

- #### p 태그

  : 문단

  

- #### br 태그

  : 줄바꿈

  

- #### pre 태그

  : 형식화 -> 입력한 그대로 출력

  

- #### strong 태그

  : 굵은 글씨

  

-  #### em 태그

  : 기울인 글씨

  

- #### sub 태그

  :  아래로 내림

  

- #### sup 태그

  : 위로 올림

  

- #### ins 태그

  : 밑줄

  

- #### del 태그

  : 취소선

  

---

### Link 태그

---

- #### a 태그

  :  <a 링크주소 = "www.a.com">
  링크주소 : key 
  www.a.com : value

  ex> <a herf="https://www.google.com">

  절대 URL  : https://myblog.com/about/myface.jpg

  상대 URL : about/myface.jpg

  ##### target

  target = "_self" : 현재탭에서 링크를 여는 속성

  target = "_blank" : 새 탭에서 링크를 여는 속성



---

#### 멀티미디어 태그

-----

- ##### 이미지 태그 

  : \<img src = "이미지 URL"> 

  - alt 속성

    : 사진 설명
    \<img src ="이미지 URL" alt = "설명">

  - width, height
    \<img src ="이미지 URL" alt = "설명" height = "320px" width = "320px">

### 

---

#### 테이블과 리스트

---

- 테이블 태그
  : \ <talbe> </table>

![image-20210419211934166](C:\Users\YOON YOUNGJUN\AppData\Roaming\Typora\typora-user-images\image-20210419211934166.png)

- table : 표 전체를 감싸는 태그
- tr : 표에서 행을 구분하는 태그
- th : 표의 행 내부에 제목 셀을 담는 태그
- td : 표의 행 내부에 데이터 셀을 담는 태그



<table> 
    <tr>
        <th>성별</th>
        <th>학년</th>
		<th>이름</th>    
    </tr>
    <tr>
    <td>남</td>
    <td>3</td>
    <td>수노</td>
</tr>
    <tr>
    <td>여</td>
    <td>3</td>
    <td>곽두팔</td>
</tr>
</table>



rowspan = " " : 숫자만큼 셀이 행을 점유

colspan = " " : 숫자만큼 셀이 열을 점유



<table> 
    <tr>
        <th>성별</th>
        <td>남</td>
		<td>여</td>    
    </tr>
    <tr>
    <th>학년</th>
    <td colspan="2">3</td>
</tr>
    <tr>
    <th>이름</th>
    <td>수노</td>
    <td>곽두팔</td>
</tr>
</table>



#### 목록

ul, ol , li



##### ul

<ul>
    <li>우유</li>
    <li>세제</li>
    <li>바지</li>
</ul>

##### ol

<ol>
    <li>우유</li>
    <li>세제</li>
    <li>바지</li>
</ol>

\<ol start= 3> : 시작 
\<ol type=""> : 타입
\<ol reversed> : 순서 거꾸로

\<li value="3"> : 3으로 기준

---

#### 폼태그

----

<form action = "my app" method="get">
    <div>
    <lable for="userid">아이디 : </lable>
    <input type="text" id="userid" name="id" palceholder = "아이디를 입력하세요">
    </div>
	<div>
    <lable for="userpassword">비밀번호 : </lable>
    <input type="password" id="userpassword" name ="password" palceholder="비밀번호를입력하세요">
    </div>
</form>

<select name ="성별" id="성별">
    <option value ="남성">남성</option>
    <option value ="여성">여성</option>
</select>



<textarea name ="introduce" id="introduce" cols="30" rows="10" placeholder="자기소개"></textarea>



<button type = "submit">제출</button>

<button type="reset">리셋</button>