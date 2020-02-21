```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="yoo.homework1.dao.BoardDAO">
    <insert id="insertBoard" useGeneratedKeys="true" parameterType="yoo.homework1.vo.BoardVO">
        <selectKey resultType="int" keyProperty="boardNum" order="AFTER">
            SELECT LAST_INSERT_ID()
        </selectKey>
        INSERT INTO
            board ( boardTitle, boardContent, userNum, boardDate )
        VALUES
            ( #{boardTitle}, #{boardContent}, #{userNum}, NOW() )
    </insert>

    <select id="selectBoard" resultType="yoo.homework1.vo.BoardVO" parameterType="yoo.homework1.vo.BoardVO">
        SELECT
            userdb.userName
            ,board.boardTitle
            ,board.boardContent
            ,board.boardDate
        FROM
            board
        JOIN
            userdb
        ON
            userdb.userNum = board.userNum
        WHERE
            boardNum = #{boardNum}
    </select>

    <select id="selectBoardListCount" resultType="_int">
        SELECT
            count(*)
        FROM
            board
        <where>
            <choose>
                <when test="searchType == 'searchTypeTitle'">
                    AND boardTitle like CONCAT('%',#{searchKeyword},'%')
                </when>
                <when test="searchType == 'searchTypeContent'">
                    AND boardContent like CONCAT('%',#{searchKeyword},'%')
                </when>
            </choose>
        </where>
    </select>

    <select id="selectBoardList" resultType="yoo.homework1.vo.BoardVO" parameterType="yoo.homework1.vo.BoardVO">
        SELECT
            board.boardTitle
            ,board.boardContent
            ,board.boardNum
            ,userdb.userName
            ,board.boardDate
        FROM
            board
        JOIN
            userdb
        ON
            userdb.userNum = board.userNum
        <where>
            <choose>
                <when test="searchType == 'searchTypeTitle'">
                    AND boardTitle like CONCAT('%',#{searchKeyword},'%')
                </when>
                <when test="searchType == 'searchTypeContent'">
                    AND boardContent like CONCAT('%',#{searchKeyword},'%')
                </when>
            </choose>
        </where>
        ORDER BY boardDate DESC , boardTitle
        LIMIT #{recordCountPerPage} OFFSET #{firstRecordIndex}
    </select>

<!--     <select id="searchBoard" resultType="yoo.homework1.vo.BoardVO" parameterType="yoo.homework1.vo.BoardVO"> -->
<!--         SELECT -->
<!--             board.boardTitle -->
<!--             ,board.boardContent -->
<!--             ,board.boardNum -->
<!--             ,userdb.userName -->
<!--             ,board.boardDate -->
<!--         FROM -->
<!--             board -->
<!--         JOIN -->
<!--             userdb -->
<!--         ON -->
<!--             userdb.userNum = board.userNum -->
<!--         <choose> -->
<!--             <when test="searchType==searchTypeContent"> -->
<!--                 WHERE -->
<!--                     boardContent like CONCAT('%',#{searchKeyword},'%') -->
<!--             </when> -->
<!--             <when test="searchType==searchTypeTitle"> -->
<!--                 WHERE -->
<!--                     boardTitle like CONCAT('%',#{searchKeyword},'%') -->
<!--             </when> -->
<!--         </choose> -->
<!--     </select> -->

    <update id="updateBoard" parameterType="yoo.homework1.vo.BoardVO">
        UPDATE
            board
        SET
            boardTitle = #{boardTitle}
            ,boardContent = #{boardContent}
        WHERE
            boardNum = #{boardNum}
    </update>
	
    <delete id="deleteBoard" parameterType="yoo.homework1.vo.BoardVO">
        DELETE FROM
            board
        WHERE
            boardNum=#{boardNum}
    </delete>

    <insert id="insertComment" useGeneratedKeys="true" parameterType="yoo.homework1.vo.CommentVO">
        <selectKey resultType="int" keyProperty="commentNum" order="AFTER">
            SELECT LAST_INSERT_ID()
        </selectKey>
        INSERT INTO
            comment (commentContent, commentDate, userNum, boardNum)
        VALUES
            ( #{commentContent}, NOW(), #{userNum}, #{boardNum})
    </insert>

    <select id="showCommentList" resultType="yoo.homework1.vo.CommentVO" parameterType="yoo.homework1.vo.CommentVO">
        SELECT
            comment.commentContent
            ,comment.commentDate
            ,comment.userNum
            ,userdb.userName
        FROM
            comment
        JOIN
            userdb
        ON
            userdb.userNum = comment.userNum
        WHERE
            boardNum = #{boardNum}
    </select>

</mapper>
```
