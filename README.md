# <div align="center">정보처리 산업기사 시험 문제</div>

## <div align="center"> 문제 1번 페이지는 몇개를 생성해야 할까? </div>
### <div align="center"> 총10개 뷰 페이지 8개 백그라운드 페이지 2개 </div><br>

#### <div align="center"> header,nav,section,footer,index.jsp (view) </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201573411-acfee07c-967c-4a7b-93f0-e2b496068b75.png"> </div>

#### <div align="center"> reservation.jsp (view) / reservation_p.jsp (back) </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201575170-6f1977f4-acca-41e8-b6d9-f5b6c86de94f.png"> </div>

#### <div align="center"> inquiry.jsp (view) </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201575191-77183b2c-63a4-4be4-8b2a-18818d9b2dfb.png"> </div>

#### <div align="center"> inquiry_p.jsp (back) </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201575219-528c1fe2-c4e8-4044-bbdf-7e09de76674b.png"> </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201575238-90398b01-aa7c-4382-9ca9-19d2e8387088.png"> </div>

#### <div align="center"> result.jsp (view) </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201575252-60e6d12e-f6c7-4ed0-a025-2a61f3e21415.png"> </div>


## <div align="center"> 문제2 테이블 생성 </div>

#### <div align="center"> TBL_JUMIN_202108 </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201573900-b7d139b3-a57a-40e2-9602-6848074d12de.png"> </div>

#### <div align="center"> TBL_HOSP_202108 </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201573997-ea3f1a35-e524-409b-bae9-d50a2c5e89b2.png"> </div>

#### <div align="center"> TBL_VACCRESC_202108 </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201574011-826114a7-047c-4c84-b025-b77c1bfd76b4.png"> </div>

## <div align="center"> reservation.jsp (view) </div>
<div align="center"> <img src="https://user-images.githubusercontent.com/102125786/201811888-0163199c-a4a8-4321-a407-8f701abf0bf4.png"> </div>


```html
  <%
    String sql =" select max(RESVNO) from TBL_VACCRESV_202108 " ;                                                  
    
    Connection conn = DBConnection.getConnection();
    PreparedStatement pstmt = conn.prepareStatement(sql);
    ResultSet rs = pstmt.executeQuery();
    
    rs.next();
	  int num = rs.getInt(1)+1;
  %>
```

```html
  <script type="text/javascript">
	  function checkVal(){
		  if(!document.rData.rNum.value){
			  alert("예약번호가 입력되지 않았습니다.");
			  rData.rNum.focus();
			  return false;
		  }else if(!document.rData.jNum.value){
			  alert("주민번호가 입력되지 않았습니다.");
			  rData.jNum.focus();
			  return false;
		  }
		  else if(!document.rData.vCode.value){
		  	alert("백신코드가 입력되지 않았습니다.");
					  return false;
		  }
		  else if(!document.rData.hCode.value){
			  alert("병원코드가 입력되지 않았습니다.");
					  return false;
		  }
		  else if(!document.rData.rDate.value){
			  alert("예약날짜가 입력되지 않았습니다.");
			  rData.rDate.focus();
			  return false;
		  }
		  else if(!document.rData.rTime.value){
			  alert("예약시간이 입력되지 않았습니다.");
			  rData.rTime.focus();
			  return false;
		  }
	  }
  </script>
```

```html
  <section class="section">
		<div class="title">백신예약</div>
		<div>
			<form name="rData" method="post" action="reservation_p.jsp" onsubmit="return checkVal()">
			<table class="table_list">
				<tr>
					<th>예약번호</th>
					<td><input type="text" name="rNum" readonly="readonly" value="<%=num%>"> 예)20210011</td>
				</tr>
				<tr>
					<th>주민번호</th>
					<td><input type="text" name="jNum"> 예)790101-1111111</td>
				</tr>
				<tr>
					<th>백신코드</th>
					<td><input type="text" name="vCode"> 예)V001, V002, V003</td>
				</tr>
				<tr>
					<th>병원코드</th>
					<td><input type="text" name="hCode"> 예)H001, H002, H003, H004</td>
				</tr>
				<tr>
					<th>예약날짜</th>
					<td><input type="text" name="rDate"> 예)20210101</td>
				</tr>
				<tr>
					<th>예약시간</th>
					<td><input type="text" name="rTime"> 예)0930, 1130</td>
				</tr>
				<tr>
					<th colspan="2">
						<input type="submit" value="등록">
						<input type="button" value="취소" onclick="remove()">
					</th>
				</tr>
			</table>
			</form>
		</div>
	</section>
```

## <div align="center"> reservation_p.jsp (back) </div>

```html
    <%
    
    String sql = "INSERT INTO TBL_VACCRESV_202108 VALUES(?,?,?,?,?,?)";
    
    Connection conn = DBConnection.getConnection();
    PreparedStatement ps = conn.prepareStatement(sql);
    
    request.setCharacterEncoding("UTF-8");
    
    ps.setString(1, request.getParameter("rNum"));
    ps.setString(2, request.getParameter("jNum"));
    ps.setString(3, request.getParameter("hCode"));
   	ps.setString(4, request.getParameter("rDate"));
    ps.setString(5, request.getParameter("rTime"));
    ps.setString(6, request.getParameter("vCode"));
    
    ps.executeUpdate();
    
    %>
```

```html
  <jsp:forward page="index.jsp"></jsp:forward>
```
