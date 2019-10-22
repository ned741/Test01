<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import="java.sql.*" %>
<%@ include file="../include/Session.jsp" %>
<%
	request.setCharacterEncoding("UTF-8");
	String b_title = request.getParameter("b_title");
	String b_content = request.getParameter("b_content");
		
	Connection conn = null;
	String sql = "";
	PreparedStatement pstmt = null;
	String ip = request.getRemoteAddr();
	try{
		Class.forName("org.mariadb.jdbc.Driver");
		conn = DriverManager.getConnection("jdbc:mariadb://localhost:3306/jsptest", "root", "1234");
		if(conn!=null){
			sql = "INSERT INTO Board(b_userid, b_name, b_title, b_content, b_ip) VALUES (?, ?, ?, ?, ?)";
			pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, userid);
			pstmt.setString(2, name);
			pstmt.setString(3, b_title);
			pstmt.setString(4, b_content);
			pstmt.setString(5, ip);
			pstmt.executeUpdate();
			pstmt.close();
			conn.close();
%>
	<script>
		alert("글이 정상적으로 입력 되었습니다.")
		location.href="List.jsp"
	</script>
<%
		}
	}catch(Exception e){
		out.println(e);
	}
%>