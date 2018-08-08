---
layout:     post
title:      "@ModelAttribute와 @RequestBody.markdown"
date:       2018-08-08 12:00:00
author:     "Start Bootstrap"
header-img: "img/post-bg-02.jpg"
---

2018-08-08

**html form 태그를 사용해서 JPA repository에 데이터를 넣고 빼는 코드를 만들고있다**

~~~html
HTML

<form action="/boardlist/add" method="post" >
    <label>
        <input type="text" name="description" id="description"/>
    </label>
    <label>
        <input type="text" name="title" id="title"/>
    </label>
    <label>
        <input type="text" name="location" id="location"/>
    </label>
    ...생략
    <div>
    <button type="submit">보냄</button>
    </div>
</form>

~~~

```java
@Controller
@RequestMapping("/boardlist")
@AllArgsConstructor
public class BoardController {
    @GetMapping("")
    public String boardList(ModelMap modelMap) {
        List<Board> boardList = boardRepository.findAll();
        modelMap.addAttribute("boardList", boardList);
        return "boardlist";
    }

    @PostMapping("/add")
    public String createBoard(@ModelAttribute BoardDto boardDto) {
        boardService.createBoard(boardDto);
        return "redirect:/boardlist";
    }
```

```java

@Service
@AllArgsConstructor
public class BoardService {
    BoardRepository boardRepository;

    public void createBoard(BoardDto boardDto) {
        Board board = Board.builder()
                .title(boardDto.getTitle())
                .description(boardDto.getDescription())
                .location(boardDto.getLocation())
                .img(boardDto.getImg())
                .reportingDate(LocalDate.now())
                .build();

        boardRepository.save(board);
    }

```

Controller의

boardList()의 경우 문제없이 JpaRepository에서 정보를 빼 서 보여준다.

createBoard() 가문제다 .  폼태그에서 전달받은 데이터들을

 참여하고있는  프로젝트에서 계속 써왔던`@RequestBody` 를 사용해서 전달받고 저장을 시키려는데

```html
Whitelabel Error Page
This application has no explicit mapping for /error, so you are seeing this as a fallback.

Wed Aug 08 21:26:03 KST 2018
There was an unexpected error (type=Unsupported Media Type, status=415).
Content type 'application/x-www-form-urlencoded;charset=UTF-8' not supported
```

415에러..

요것때매  거진 하루를 다날려먹었다.

매우 어처구니없게 `@RequestBody` 대신 `@Modelatrribute` 를 사용하니 잘 동작한다.



해결은 했는데 다시한번 알아 보아야 겠다.

<https://code-examples.net/en/q/244d99f>





