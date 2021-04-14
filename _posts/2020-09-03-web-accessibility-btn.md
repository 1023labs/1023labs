---
layout: post
title:  "[웹접근성] button과 link 정확하게 사용하기"
date:   2020-09-03 22:34:56 +0900
categories: posts
tags: [article,웹접근성,버튼,링크,href,button,link]
redirect_from: /posts/74
image: /assets/img/web-accessibility-btn/sm_1.png
--- 
<iframe frameborder="0" src="//www.youtube.com/embed/dhsr2LGTA-s" width="640" height="360" class="note-video-clip"></iframe>

<iframe frameborder="0" src="//www.youtube.com/embed/oOOr-6jHaGU" width="640" height="360" class="note-video-clip"></iframe>

<br />

`<a>` 태그와 `<button>` 태그를 생각없이 섞어서 사용하면서,  
css 로 스타일을 변경하면 어차피 비슷하게 보이기에 생각없이 섞어 써왔는데요.   
눈으로 보기에는 별 차이가 없지만, 기능은 완전히 다르고,  
스크린 리더에서 다른 용도로 인식하기 때문에, 용도에 맞게 구분해서 사용해야 한다고 하네요.

<br />

<table class="table">
  <tbody>
    <tr>
      <td style="text-align: center;">button</td>
      <td style="text-align: center;">link</td>
    </tr>
    <tr>
      <td>
        <ul>
          <li>키보드 "스페이스"와 "엔터"로 동작</li>
          <li>폼을 전송하거나 취소할 때</li>
          <li>팝업(모달)을 열때 또는 팝업메뉴를 열때</li>
          <li> 동영상을 플레이 할때</li>
          <li>내용의 일부만 변경될 때</li>
          <li>동작을 위해 자바스크립트 필요</li>
          <li>마우스 오른쪽 버튼에 별다른 기능 없음</li>
        </ul>
      </td>
      <td>
        <ul>
          <li>키보드 "엔터"로 동작</li>
          <li>브라우저의 redraw/refresh 일어남</li>
          <li>다른 문서로 링크하거나, <br>같은 문서내 다른 anchor로 이동할 때</li>
          <li>새창으로 페이지를 열 때</li>
          <li>href 속성에 따라 페이지 이동</li>
          <li>마우스 오른쪽 버튼에 여러 기능 있음</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

<br />

`a` 태그에 `role="button"` 속성을 추가하고, 키보드 "스페이스"에 동작하도록  
스크립트를 추가해서 사용하면 보완할 수 있지만,  
그것 보다는 정확한 용도에 따라 태그를 사용하는게 더 중요할 듯 싶습니다.

나중에 평가도구 돌려서 고치는 것 보다, 조금씩 공부해서 코딩의 좋은 습관을 들이는 것이 중요할 것 같습니다.  


