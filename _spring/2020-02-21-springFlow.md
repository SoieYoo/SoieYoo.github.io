### 1. 로그인 버튼을 눌렀을 때

   *  (1) .  사용자 화면에서 로그인 버튼에 지정된 url 인 "/login"으로 POST 합니다.
   *  (2) .  Controller에서 지정된 "/login" 과 관련된 Service를 호출합니다.
   *  (3) .  Service 요청 내용에 따라 MemberDAO로 이동합니다.
   *  (4) .  DB에서 사용자 아이디/비빌번호를 비교하는 요청을 처리하기 위해 Service에서 해당 메소드로 값을 검사합니다.
   *  (5) .  Service에서 return한 member객체를 LoginController에서 받아서 처리합니다.

### [추가] 로그인 버튼을 눌렀을 때 리다이렉트하는 로직 추가합니다!

   *  (1) .  사용자 화면에서 로그인 버튼에 지정된 url 인 "/login"으로 POST 합니다.
   *  (2) .  Controller에서 지정된 "/login" 과 관련된 Service를 호출합니다.
   *  (3) .  Service 요청 내용에 따라 MemberDAO로 이동합니다.
   *  (4) .  DB에서 사용자 아이디/비빌번호를 비교하는 요청을 처리하기 위해 Service에서 해당 메소드로 값을 검사합니다.
   *  (5) .  Service에서 return한 member객체를 LoginController에서 받습니다.
   *  (6) .  **LoginController에서는 session에 넘어오는 회원ID 값과 DB의 회원ID값을 비교합니다.**
   *  (7) .  **ID 값이 null이 아니고, 고객이 입력한 비밀번호와 DB의 비밀번호가 일치한다면 member 객체를 return하고 글 등록 페이지로 redirect 합니다.**

### 2. 글을 등록할 때

   *  (1) . 사용자가 글을 입력하고, 등록하기 버튼을 클릭합니다.
   *  (2) . **[ Spring 프레임워크 동작 ]** Dispatcher가 요청을 받아 HandlerMapping으로 넘깁니다.
   *  (3) . **[Spring 프레임워크 동작 ]** Controller의 URL 매핑을 통해 사용자의 요청을 처리할 Controller 찾습니다.
   *  (4) . POST된 값과 일치하는 Controller로 Service 호출합니다.
   *  (5) . Service 내용에 따라 BoardDAO를 통해 DB에 글을 등록합니다.
   *  (6) . 사용자가 입력한 파라미터 값은 BoardVO 객체에서 처리하며 Setter 메소드를 호출합니다.
   *  (7) . 서비스에서 return한 객체를 Controller에서 받아옵니다.
   *  (8) . **[ Spring 프레임워크 동작 ]** Controller가 View Name을 반환하면 prefix, suffix를 적용해 해당 경로에 .jsp파일을 만들어 Model을 전달합니다.
   *  (9) . 이 View에 Model data를 이용해 적절한 페이지를 사용자에게 보여줍니다.

### 3. 글 목록을 게시할 때

   *  (1) . 게시글 목록을 보여주는 페이지로 (url은 "/boardListPage") GET Mapping 합니다.
   *  (2) . **[Spring 프레임워크 동작 ]** 요청을 처리하기 위해 Controller를 찾습니다.
   *  (3) . @Autowired로 명시한 BoardService의 서비스 로직으로 들어갑니다.
   *  (4) . BoardDAO를 통해 DB에 관련된 select 쿼리를 수행합니다.
   *  (5) . mapper-boardList.xml의 파라미터 타입인 BoardVO 객체에서 Getter 메소드가 호출됩니다.
   *  (6) . 서비스에서 BoardDAO객체의 boardList()라는 메소드를 리턴합니다. 
   *  (7) . Controller에서 BoardDAO 객체의 boardList를 받아옵니다.
   *  (8) . **[ Spring 프레임워크 동작 ]** Controller가 View Name을 반환하면 prefix, suffix를 적용해 해당 경로에 .jsp파일을 만들어 Model을 전달합니다.
   *  (9) .  이 boardList 라는 View에 Model data를 이용해 글 목록을 사용자에게 보여줍니다.
   
