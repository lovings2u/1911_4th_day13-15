# Day 13~15

- javascript

  - 자바스크립트는 html과 css로 이루어진 정적인 페이지에 요소를 변화시켜 다이나믹하게 만들거나 비동기 서버 통신을 위하여 사용하게 된다.

  ```html
  <!-- js-test.html -->
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <style>
          .bg-red {
              background-color: red;
          }
      </style>
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
  </head>
  <body>
      <h1 id="title">오늘은 자바스크립트 수업 날입니다 :)</h1>
      <h2 id="joke">자바스크립트 솔직히 재미없어요...ㅠㅠ</h2>
      <div class="hi">요소1</div>
      <div class="hi">요소2</div>
      <div class="hi">요소3</div>
      <div class="hi">요소4</div>
      <div class="hi">요소5</div>
  
      <form class="mb-5 mt-5">
          글쓰기
          <input type="text" class="form-control" id="articleForm">
          <button type="button" class="btn btn-primary">글쓰기</button>
          <div class="pb-5"></div>
          댓글쓰기
          <input type="text" class="form-control" id="commentForm">
          <button type="button" class="btn btn-primary" id="submitComment">댓글쓰기</button>
      </form>
      <div class="commentList">
          <ul class="list-group">
              <li class="list-group-item">
                  첫번째 댓글입니다.
                  <span class="float-right">
                      <button type="button" class="btn btn-warning">수정</button>
                  </span>
              </li>
              <li class="list-group-item">
                  두번째 댓글입니다.
                  <span class="float-right">
                      <button type="button" class="btn btn-warning">수정</button>
                  </span>
              </li>
              <li class="list-group-item">
                  세번째 댓글입니다.                
                  <span class="float-right">
                      <button type="button" class="btn btn-warning">수정</button>
                  </span>
              </li>
              <li class="list-group-item">
                  네번째 댓글입니다.
                  <span class="float-right">
                      <button type="button" class="btn btn-warning">수정</button>
                  </span>
              </li>
          </ul>
      </div>
  
      <script>
          var btn = document.getElementById('submitComment');
          btn.addEventListener('click', function() {
              // commentForm에 있는 내용을 받아서
              var commentForm = document.getElementById('commentForm');
              if(commentForm.value == '') {
                  alert('빈칸은 입력할 수 없습니다.');
                  return;
              }
              // console.dir(commentForm);
              // alert 혹은 console 에 출력
              // console.log(commentForm.value);
  
              // 댓글을 추가할 위치를 찾아서
              var position = document.querySelector('.list-group');
              // console.dir(position);
              // 추가할 HTML 태그 모양을 잡고
  
              var appendingTag = document.createElement('li');
              var appendingSpan = document.createElement('span');
  
              appendingTag.classList.add('list-group-item');
              appendingSpan.classList.add('float-right');
  
              appendingTag.innerText = commentForm.value;
              appendingSpan.innerHTML = '<button type="button" class="btn btn-warning">수정</button>';
              appendingTag.appendChild(appendingSpan);
              commentForm.value = '';
              // console.dir(appendingTag);
              // <li class="list-group-item">
              //     JS로 추가된 댓글입니다.
              //     <span class="float-right">
              //         <button type="button" class="btn btn-warning">수정</button>
              //     </span>
              // </li>
              // 해당 위치에 추가
              position.prepend(appendingTag);
              // appendChild vs prepend
          })
  
  
          // var joke = document.getElementById('joke');
          // // joke.onclick = function() {
          // //     alert("이거 거짓말이야");
          // // }
          // joke.addEventListener('click', function() {
              
          // })
          var pList = document.getElementsByTagName('p');
          var pList2 = document.querySelectorAll('.hi');
          pList2.forEach(function(element) {
              element.addEventListener('click', function() {
                  element.classList.toggle('alert');
                  element.classList.toggle('alert-primary');
                  // console.dir(element);
                  // if(confirm("이 태그를?")) {
                  //     // element.setAttribute('class', 'bg-red');
                  //     // element.classList.toggle('bg-red')
                      
                  // }
              })
          })
          // for(var i = 0; i < pList.length; i++) {
          //     pList[i].addEventListener('click', function() {
          //         alert("이건 아마 될거야...");
          //     })
          // }
          // pList.addEventListener('click', function() {
          //     alert("이건 아마 안될거야...");
          // })
      </script>
  </body>
  </html>
  ```

  - js는 결국 *요소 선택* -> *이벤트 리스너 등록* -> *이벤트 핸들러 등록* 의 구조로 이루어져있다. 우리가 해야할 일은 다음과 같다.

    - 이벤트가 발생할 요소가 어디인지 찾는다. 여기서 말하는 이벤트는 사용자가 페이지를 사용할 때 발생하는 클릭, 드래그, 마우스 오버 등을 말한다.
    - 해당 요소에서 발생하는 이벤트 중 우리가 원하는 이벤트가 발생한 경우를 찾는 이벤트 리스너를 등록한다.
    - 이벤트 리스너 등록 시 해당 이벤트가 발생할 경우 실행할 로직을 등록한다.(이벤트 핸들러)

    - 결국 `전체 HTML문서.특정요소탐색.이벤트리스너등록('발생할 이벤트', 이벤트 핸들러)`의 형태로 이루어진다.

- jQuery

  - jquery는 js의 다양하고 복잡한 기능을 쉽게 사용하기 위한 라이브러리이다. 요소 선택자부터 다양한 이벤트까지 처음 접하고 나면 쉽게 끊을 수 없는 마약같은 존재이다.
  - 외부 CDN을 불러와도 되고 자체적으로 설치해서 사용해도 된다.
  - 구조는 JS와 유사하다. 

  ```html
  <!DOCTYPE html>
  <html lang="ko">
  
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title>Document</title>
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
          integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
  
  </html>
  </head>
  
  <body>
      <form class="mb-5 mt-5" id="boardForm">
          댓글쓰기
          <input type="text" class="form-control" id="boardInput">
          <button type="submit" class="btn btn-primary" id="submitComment">확인</button>
      </form>
      <div class="commentList">
          <ul class="list-group">
              {% for board in boards %}
              <li class="list-group-item" id="board-{{board.id}}">
                  <span class="boardItem">{{ board.contents }}</span>
                  <span class="float-right">
                      <button type="button" class="btn btn-danger deleteBoard" data-id="{{board.id}}">삭제</button>
                      <button type="button" class="btn btn-warning editBoard" data-id="{{board.id}}">수정</button>
                  </span>
              </li>
              {% endfor %}
          </ul>
      </div>
      <script src="https://code.jquery.com/jquery-3.4.1.min.js"
          integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo=" crossorigin="anonymous"></script>
      <script>
          $(function() {
              // 수정 버튼을 눌렀을 때 실제 DB에서 수정됨
              // 수정 버튼을 찾아서 이벤트를 등록해야함
              $(document).on('click', '.editBoard', function() {
                  var id = $(this).data('id');
                  var contents = $('#board-' + id + ' .boardItem').text();
                  $('#boardInput').val(contents);
                  $('#submitComment').data('method', 'edit');
                  $('#submitComment').data('id', id);
                  console.log($('#submitComment').data());
              })
  
              // 삭제 버튼을 눌렀을 때 실제로 DB에서 삭제시키기
              // 삭제 버튼을 눌렀을 때
              $(document).on('click', '.deleteBoard', function() {
                  // 해당 줄(list)을 하나 삭제해야함
                  var id = $(this).data('id');
                  $.ajax({
                      url: '{% url "delete_boards" %}',
                      method: 'POST',
                      data: {
                          board_id: id,
                          csrfmiddlewaretoken: '{{csrf_token}}',
                      },
                      success: function(data) {
                          $('#board-' + data.board_id).hide();
                      },
                      error: function(data) {
                          alert("삭제실패");
                      }
                  })
                  
  
              })
  
  
              // 댓글 쓰고, 실제로 DB에 등록하기
              // boardForm이 제출되었을 때
              $('#boardForm').on('submit', function(event) {
                  event.preventDefault();
                  // 실제 DB에 등록이 될 수 있게끔 ajax 요청을 만들어줌
                  var board = $('#boardInput').val();
                  // 등록 시에는 /insta/jq-test/boards/
                  // 수정 시에는 /insta/jq-test/boards/edit
                  // var target = $('#boardForm').data('target');
                  $('#boardInput').val('');
                  console.log($('#submitComment').data());
                  if($('#submitComment').data('method') == 'edit') {
                      var id = $('#submitComment').data('id');
                      $.ajax({
                          url: '{% url "edit_boards" %}',
                          method: 'POST',
                          data: {
                              board_id: id,
                              contents: board,
                              csrfmiddlewaretoken: '{{csrf_token}}'
                          },
                          success: function(data) {
                              // 뭘 찾아야함? -> 댓글이 있는 부분
                              $('#board-' + id + ' .boardItem').text(board);
                              // 뭘 바꿔야함? -> 내용을 바꿔야함
                              // 확인 버튼에 달려있는 속성(data-method)을 삭제해야함
                              $('#submitComment').removeData('method');
                              $('#submitComment').removeData('id');
  
                          },
                          error: function(data) {
                              alert("수정 실패");
                          }
                      })
                  } else {
                      $.ajax({
                          url: '{% url "submit_boards" %}',
                          method: 'POST',
                          data: {
                              board: board,
                              csrfmiddlewaretoken: '{{csrf_token}}'
                          },
                          success: function(data) {
                              $('.list-group').prepend(data);
                          },
                          error: function(data) {
                              alert("실패!")
                          }
                      })
                  }
                  
  
              })
  
  
  
              // 댓글달기
              // 댓글쓰기 버튼이 눌렸을때,
              // $('#submitComment').on('click', function() {
              //     var input = $('#commentForm').val();
              //     if(input == '') {
              //         alert("댓글을 입력해주세요");
              //         return;
              //     }
              //     // ul.list-group 에 붙여줌
              //     var position = $('ul.list-group');
              //     // li.list-group-item 요소를 만들어서
              //     $('#commentForm').val('');
              //     var element = `<li class="list-group-item" id="comment-1">
              //         ${input}
              //         <span class="float-right">
              //             <button type="button" class="btn btn-danger delete-comment" value="1">삭제</button>
              //             <button type="button" class="btn btn-warning">수정</button>
              //         </span>
              //     </li>`
              //     position.prepend(element);
              // })
  
              // 이벤트가 발생할 요소를 찾고
              // $(document).on('click', '.delete-comment', function () {
              //     // 이벤트가 발생했을 경우 실행할 이벤트 핸들러를 만든다.
              //     // console.dir($(this));
              //     var commentId = $(this).attr('value');
              //     // 1. commentId로 삭제할 요소를 찾아서 지워줌
              //     // $('#comment-' + commentId).remove();
              //     // 2. 이벤트가 발생한 놈으로부터 부모를 찾아 지워줌
              //     $(this).parents('.list-group-item').remove();
              //     // console.log(commentId);
              //     // console.dir(this.attr('value')); <- jquery 메소드 사용 불가
              //     // console.dir(this);
              //     // 현재 버튼을 누른 댓글이 삭제되어야 함
  
              // })
          })
          // $(function() {
  
          // })
      </script>
  </body>
  
  </html>
  ```

  - jQuery에서는 요소 선택자와 이벤트 리스너, 핸들러 등록이 조금 다른 형식으로 이루어진다.
    - 요소 선택자는 `$('[CSS SELECTOR]')`의 형식으로 이루어진다.
    - 이벤트 리스너 등록은 `.on('이벤트 명', 이벤트 핸들러)`의 형식으로 이루어진다.
    - jQuery에는 정말 다양한 메소드가 존재한다. 그것을 전부 외우고 있기 보다는 원하는 메소드가 있다면 그때그때 검색해서 사용하면서 익숙해지는 방법을 추천한다.