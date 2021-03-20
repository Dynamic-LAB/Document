# Android Resource Convention

## Layout
What_Where

### What
- activity_ : 액티비티에서 쓰이는 레이아웃 파일
- fragment_ : 프래그먼트에서 쓰이는 레이아웃 파일
- dialog_ : 다이얼로그에서 쓰이는 레이아웃 파일
- view_ : 커스텀 뷰에서 쓰이는 레이아웃 파일
- itme_ : 리사이클러뷰, 리스트 뷰 등에서 ViewHolder에 쓰이는 레이아웃 파일(각 아이템 항목에 대한)
- layout_ : 재사용 되는 공통 레이아웃

## ID
- What_Description
- What은 View의 PascalCase의 대문자를 축약한 형태로 지정
- View의 이름이 1개의 단어로 이루어져 있다면 View 이름의 LowerCase로 지정
- 커스텀 뷰의 경우 전체 View의 이름을 snake_case로 지정
- Description이 여러 단어인 경우 모두 소문자인 snake_case로 지정

ex) TextView -> tv_

Button, ImageButton보다 TextView와 ImageView 사용 권장

## Drawable
- What_Where_Description_Size
- 이미지가 여러 곳에서 사용시 Where 생략 가능
- Size가 하나인 경우 생략 가능

### What
- btn_ : 버튼으로 쓰는 이미지
- ic_ : 화면에 보여지는 이미지
- bg_ : 배경
- img_ : 실제 이미지
- div_ : divider로 사용하는 이미지

### Selector
배경이나 버튼이 View의 상태에 따라 Drawable이 변하는 경우 이름 설정
- Normal : `_normal`
- Pressed : `_pressed`
- Focused : `_focused`
- Disabled : `_disabled`
- Selected : `_selected`

## Dimen
Where_Description_What

## String
Where_Description

- 특정 화면에서 쓰이는 텍스트가 아니고 공통 텍스트인 경우 all_Description 형태로 지정
- 개행이 필요한 경우 `\n` 사용

## 기타
- 마진과 패딩의 경우 Left/Right보다 Start/End 권장
- Dimen.xml, String.xml, Color.xml에 지정해놓고 활용하기
