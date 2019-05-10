# Controller

## 1. @RequestMapping Return Type

* ModelAndView

```java
@RequestMapping("list.do")
public ModelAndView list(int bno, ModelAndView mav) {
    List<ReplyDTO> list=replyService.list(bno); //댓글 목록
    mav.setViewName("board/reply_list"); //뷰의 이름
    mav.addObject("list", list); //뷰에 전달할 데이터 저장
    return mav; //뷰로 이동
}
```

* String

```java
@RequestMapping("delete.do")
public String delete(int bno) throws Exception {
    boardService.delete(bno); //삭제 처리
    return "redirect:/board/list.do"; //목록으로 이동
}
```

* List

```java
//댓글 목록을 ArrayList로 리턴
@RequestMapping("list_json.do")
public List<ReplyDTO> list_json(int bno){
    return replyService.list(bno);
}
```

* void

```java
@RequestMapping("insert.do") //세부적인 url pattern
public void insert(ReplyDTO dto, HttpSession session) {
    //댓글 작성자 아이디
    String userid=(String)session.getAttribute("userid");
    dto.setReplyer(userid);
    //댓글이 테이블에 저장됨
    replyService.create(dto);
    //jsp 페이지로 가거나 데이터를 리턴하지 않음
}
```

* Model Object

```java
@RequestMapping("view")
public User view(@RequestParam int bno) throws Exception {
    return userService.getUser(id); //목록으로 이동
}
```

## 2. @ResponseBody

```java
@RequestMapping("/hello")
@ResponseBody
public String hello() {
     return "<html><body>Hello Spring</body></html>";
}
```

