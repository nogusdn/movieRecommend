

# 1. Model

- ## 1. User (Accounts)

  1) username
  2) password
  3) age
  4) sex

  -----

  1. followings

  2. followed

  3. like_movies

  4. reviews

  5. like_reviews

  6. comments

  7. like_comments

     

     

- ## 2. Movies (Movies)

  1. title

  2. overview

  3. like_users (주 관심 연령대)

  4. watched_users (주 시청 연령대)

  5. reviews

  6. release_date

  7. poster_path

  8. popularity

  9. vote_count

  10. vote_average

      

- ## 3. Review(=>Movies)

  1. user
  2. like_users
  3. title
  4. content
  5. movie
  6. created_at
  7. updated_at

- ## 3. Comments (=>Review)

  1. user
  2. like_user
  3. Review

# 2. 기능



## **1. like & watch**

- 영화 찜하기 및 시청 기록 기능
- 알고리즘에 활용



## 2. 영화추천

- **내가 찜한 영화**
  - 좋아요 누른 영화들 리스트
- **또래가 많이 보고 좋아한 영화**
  - 내 나이대 (+x, -x) 유저들이 watch와 like를 많이 한 상위 15개 영화
- **내 성별이 많이 보고 좋아한 영화**
  - 내 성별 (남,여) 유저들이 watch와 like를 많이 한 상위 15개 영화
- **내 팔로워들이 많이 보고 좋아한 영화**
  - 내 팔로워들이 watch와 like를 많이 한 영화 
- **내가 좋아할 만한 영화****
  - 내가 watch와 like를 한 영화들의 장르를  count하여, 상위 3개의 장르들에 속한 영화들을 인기도 순으로 15개 선정



# Back 박주현

## 1. model

- User 모델의 경우, 유저의 성별, 나이 등의 정보가 알고리즘에 활용되기에 유저 필드를 어떻게 설정할 것인지 많이 고민했다.
- allauth user모델을 사용해서 유저 필드를 추가하는 것에서 많은 난관이 있었으나 구글링의 힘은 위대하다고 느꼈다.
- Movie tmdb에서 모델을 가져올 때, 최대한 많은 영화 데이터를 가져오기 위해 노력했다.

## 2. serializer

- 유저, 영화, 리뷰, 등에 대한 정보를 줄 때, 그 안에 필드들에서 또 serializer로 반환해서 줘야하는 것들이 많았다. 
- 그런데 계속 serializer로 반환하다보니, 싸이클이 생겨서 오류가 생겼는데, 이를 적절하게 조절하고 필드도 최소한으로 줄여주기 위해 노력했다.
- User의 경우, following 유저와 follower 유저들의 정보를 또 serializer로 줘야하기 때문에, FakeUserSerialzier을 만들어서 사용했다.

## 3. url

- Front와 원활하게 소통하고 편하게 하기 위해 vue의 drf와 형식을 통일시켰다. 
- url을 짜면서 프로젝트의 구조를 잡을 수 있었던 것 같다.

## 4. view

- 알고리즘을 짤 때, 다양한 조건들을 걸어주는 것도 중요하지만 쿼리나 리스트, 객체 등을 활용할 때 type과 그 특성을 잘 알아두는 것의
  중요성을 알 수 있었다. 알고리즘 짜는 것은 생각 외로 재미있었다.



----

# Front 노현우



### 1.NavBar

navbar의 경우 로그인이 되어있지 않을 때는 MOVIES 리스트가 나오는 home, 회원가입, 로그인, 그리고 영화를 검색 할 수 있는 영화 검색창을 만들었고 로그인이 되었을 경우에는 회원가입과 로그인 대신 커뮤니티인 REVIEW와 profile, 로그아웃을 넣어주었다.

### 2.Home

어두운 배경색이 영화가 한 눈에 들어와서 선택하였고 로그인이 되어있지 않을 경우에는 기존 tmdb에 구현되어있는 popular, upcoming, now를 가져왔고 회원가입 할 때 age와 gender를 필수로 넣고 위의 데이터들을 받아와서 로그인이 되었을 경우에는 내가 좋아요한 영화들, 좋아요 + 시청한 영화와 비슷한 영화, 나와 같은 성별이 좋아하는 영화, 나와 비슷한 또래가 좋아하는 영화가 나오게 구현하였다. 그리고 영화에 마우스 커서가 올라가면 ease-in-out으로 조금 확대되게 하였다.

### 3.movieDetail

영화 디테일은 영화포스터, 제목, 장르, 개봉일, overview, 유튜브영상 정도 나오게 했고

영화 좋아요와 시청한 영화를 체크할 수 있게 하였음

아래에는 해당 영화의 리뷰들이 나온다.

### 4. ReviewList

모든 리뷰 목록이 나온다. 카드형식으로 구현하였다.

### 5. ReviewDetail

리뷰 상세정보가 나오고 아래에 댓글 달 수 있다.

사용자가 같다면 게시글 수정 삭제, 댓글 수정 삭제 가능하다.

---



## 느낀점

처음으로 프론트, 백을 나눠서 며칠간 작업을 하였다. 

꾸준히 의사소통하고 안 되는 점을 물어보고 여러 부분들을 어떻게 구현할지 회의를 자주 하였다. 

어려웠던 점은 어떤 기능을 하나를 구현하면 구현한 기능에서 세부적으로 또 다른 구현이 필요한 것이 엄청 많았고 사소한 기능도 많은 시간이 필요했다. 이번 프로젝트에 솔직히 많은 기능이 없는데도 많은 시간이 필요했다. 에러를 확인하고 수정하면 또 다른 곳에서 에러가 뜨기도 하였고 사소한 것 하나를 놓쳐서 왜 안 되는지 찾기 위해 많은 시간을 쓰기도 하였다. 알고보면 되게 사소한 것이라서 화도 났다. 

CSS부분 같은 경우 어떻게 하면 좀 더 예쁘고 깔끔하게 꾸밀 수 있을지 고민도 많이 하였고 자꾸 욕심이 생기기도 하였다. 그리고 서로 브랜치를 만들어서 협업하는 것도 제대로 된 실습이 처음이라 우여곡절이 많았다. 첫 프로젝트였지만 페어와 서로 열심히 하고 도와주면서 많은 것을 배웠다.


