```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<!DOCTYPE html>
<html lang="ko">
<head>
<style type="text/css">
div.selectBoxContainer {
    position: relative;
    margin-left: 40%;
}
div.insertCommentButtonContainer {
    margin-left: 20%;
}
</style>
<meta charset="UTF-8">
<!-- <meta name="viewport" content="width=device-width, initial-scale=1"> -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap-theme.min.css">
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/js/bootstrap.min.js"></script>
<title>게시판</title>
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-light bg-light" aria-label="navbar">
        <ul class="nav nav-tabs">
            <li role="presentation"><a href="boardListPage">Home</a></li>
        </ul>
    </nav>
        <h3 style="text-align: center;">글 목록 페이지입니다.</h3>
        <h2 style="text-align: center;">${member.userName}님 환영합니다.</h2>
    <div class="selectBoxContainer">
        <form action="/boardListPage" method="get" name="searchOption">
        <input type="hidden" name="currentPageNo" value="${boardVO.currentPageNo}">
        <table aria-describedby="">
            <tr>
                <th id="search">
                    <select name="searchType" id="searchType" style="width: 60px; height: 30px;">
                        <option value="searchTypeTitle" <c:if test="${param.searchType eq 'searchTypeTitle'}">selected</c:if>>제목</option>
                        <option value="searchTypeContent" <c:if test="${param.searchType eq 'searchTypeContent'}">selected</c:if>>내용</option>
                    </select>
                    <input id="searchKeyword" name="searchKeyword" value="${param.searchKeyword}" type="text" style="width: 300px; height: 30px"/>
                    <button type="submit" class="btn btn-default">검색</button>
                </th>
            </tr>
        </table>
            <h4>${sendMessage.message }</h4>
        </form>
    </div>
        <div class="container">
        <table class="table" aria-describedby="selectBoardListTable">
            <colgroup>
                <col width="6%"/>
                <col width="60%"/>
                <col width="17%"/>
                <col width="20%"/>
            </colgroup>
            <thead>
                <tr>
                    <th id="num">글 번호</th>
                    <th id="boardTitle">제목</th>
                    <th id="userName">작성자</th>
                    <th id="boardDate">작성일</th>
                </tr>
            </thead>
            <tbody>
                <c:forEach items="${boardList}" var="board" varStatus="stat">
                    <tr>
                        <td>${boardVO.totalRecordCount - (boardVO.currentPageNo - 1)*10 - stat.index}</td>
                        <td><a href="boardDetail?boardNum=${board.boardNum}">${board.boardTitle}</a></td>
                        <td>${board.userName}</td>
                        <td>${board.boardDate}</td>
                    </tr>
                </c:forEach>
            </tbody>
        </table>
    </div>
    <div class="insertCommentButtonContainer">
        <form action="/insert" method="post">
            <button type="submit" class="btn btn-success">글 등록하러가기</button>
        </form>
    </div>
    <div class="container text-center">
    <nav aria-label="Page navigation">
        <ul class="pagination">
            <c:if test="${boardVO.prev}">
                <li class="page-item"><a href="boardListPage?currentPageNo=${boardVO.firstPageNoOnPageList-5}" aria-label="Previous" class="page-link">
                <span aria-hidden="true">&laquo;</span></a></li>
            </c:if>
            <c:forEach begin="${boardVO.firstPageNoOnPageList}" end="${boardVO.lastPageNoOnPageList}" step="1" var="page">
                <c:if test="${boardVO.currentPageNo eq page}">
                    <li class="active"><a href="boardListPage?currentPageNo=${page}" class="page-link">${page}</a></li>
                </c:if>
                <c:if test="${boardVO.currentPageNo != page && param.searchKeyword eq null}">
                    <li class="page-item"><a href="boardListPage?currentPageNo=${page}" class="page-link">${page}</a></li>
                </c:if>
                <c:if test="${boardVO.currentPageNo != page && param.searchKeyword != null}">
                    <li class="page-item"><a href="boardListPage?currentPageNo=${page}&searchType=searchTypeTitle&searchKeyword=${param.searchKeyword}" class="page-link">${page}</a></li>
                </c:if>
            </c:forEach>
            <c:if test="${boardVO.next}">
            <li class="page-item"><a href="boardListPage?currentPageNo=${boardVO.lastPageNoOnPageList + 1}" aria-label="Next" class="page-link">
                <span aria-hidden="true">&raquo;</span></a>
            </li>
            </c:if>
        </ul>
    </nav>
    </div>
</body>
</html>
```
