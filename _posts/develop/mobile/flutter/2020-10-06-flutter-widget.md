---
title: '[Flutter] Widget'
date: 2020-10-06 14:00:00 -0400
categories: devlog
tags: devlog flutter widget
---

## 화면 배치에 쓰는 기본 위젯

### Container

아무것도 없는 위젯.

다양한 프로퍼티를 가지고 있기 때문에 사용하기에 따라서 다양한 응용이 가능.

```dart
Container(
  color: Colors.red,
  width: 100,
  height: 100,
  padding: const EdgeInsets.all(8.0),
  margin: const EdgeInsets.all(8.0),
)
```

### Column

수직 방향으로 위젯들을 나란히 배치하는 위젯.

레이아웃은 대부분 Column, Row를 조합하여 만들기 때문에 매우 자주 사용됨.

```dart
Column(
  children: <Widget>[
    [위젯],
    [위젯],
    ...
  ],
),
```

```dart
Column(
  children: <Widget> [
    Container(
      color: Colors.red,
      width: 100,
      height: 100,
      padding: const EdgeInsets.all(8.0),
      margin: const EdgeInsets.all(8.0),
    ),
    Container(
      color: Colors.blue,
      width: 100,
      height: 100,
      padding: const EdgeInsets.all(8.0),
      margin: const EdgeInsets.all(8.0),
    ),
    ...
  ],
)
```

### Row

Columnm과 반대로 수평방향으로 위젯들을 나란히 배치하는 위젯

```dart
Row(
  mainAxisSize: MainAxisSize.max, // 가로로 꽉 채우기
  mainAxisAlignment: MainAxisAlignment.center, // 가로 방향으로 가운데 정렬하기
  crossAxisAlignment: CrossAxisAlignment.center, // 세로 방향으로 가운데 정렬하기
  children: <Widget>[
    [위젯],
    [위젯],
    ...
  ],
),
```

mainAxis는 위젯의 기본 방향을 나타냄. Row는 오른쪽, Column은 아래쪽이 mainAxis

crossAxis는 기본 방향의 반대 방향을 나타냄. Row는 아래쪽, Column은 오른쪽 crossAxis

#### MainAxisSize에 정의된 상수

max

min

#### MainAxisAlignment와 CrossAxisAlignment에 정의된 상수

center

start

end

spaceEvenly

spaceBetween

spaceAround

### Stack

children에 나열한 여러 위젯을 순서대로 겹치게함.

사진 위에 글자를 표현하거나 화면 위에 로딩 표시를 하는 상황에 사용할 수 있다.

```dart
Stack(
  children: <Widget>[
    Container(
      color: Colors.red,
      width: 100,
      height: 100,
      padding: const EdgeInsets.all(8.0),
      margin: const EdgeInsets.all(8.0),
    ),
    Container(
      color: Colors.green,
      width: 100,
      height: 100,
      padding: const EdgeInsets.all(8.0),
      margin: const EdgeInsets.all(8.0),
    ),
  ],
)
```

### SingleChildScrollView

Column을 사용하여 위젯들을 나열하다가 화면 크기를 넘어서면 스크롤이 필요함.

그럴때는 SingleChildScrollView로 감싸서 스크롤이 가능하게 할 수 있다.

SingleChildScrollView는 말 그대로 하나의 자식을 포함하는 스크롤 가능한 위젯.

Column은 기본적으로 표시할 위젯의 크기만큼 가로 길이를 가진다. 따라서 스크롤 가능 영역이 좁을 수 있다. ListBody를 사용하면 스크롤 가능 영역이 가로로 꽉 차기 때문에 사용자가 스크롤하기 더 쉽다.

```dart
final items = List.generate(100, (i)=> i).toList();

SingleChildScrollView(
  child:ListBody(
  children: items.map((i) => Text('$i')).toList(),
  ),
),
```

### ListView, ListTile

ListView는 리스트를 표시하는 위젯.

SingleChildScrollView와 ListBody의 조합과 동일한 효과를 내지만 좀 더 리스트 표현에 최적화된 위젯.

ListView에 표시할 각 항목의 레이아웃은 직접 정의해도 되지만 리스트 아이템을 쉽게 작성할 수 있는 ListTile 위젯을 사용하면 편리함.

```dart
ListView(
  scrollDirection: Axis.vertical,
  children:<Widget>[
    ListTile(
      leading: Icon(Icons.home),
      title: Text('Home'),
      trailing: Icon(Icons.navigate_next),
      onTap: (){},
    ),
        ListTile(
      leading: Icon(Icons.event),
      title: Text('Event'),
      trailing: Icon(Icons.navigate_next),
      onTap: (){},
    ),
        ListTile(
      leading: Icon(Icons.camera),
      title: Text('Camera'),
      trailing: Icon(Icons.navigate_next),
      onTap: (){},
    ),
  ]
)
```

### GridView

열 수를 지정하여 그리드 형태로 표시하는 위젯

GridView.count() 생성자는 간단하게 그리드를 작성하게 해줌. crossAxisCount 프로퍼티에 열 수를 지정할 수 있다.

```dart
GridView.count(
  crossAxisCount: [열 수],
  children: <Widget> [
    [위젯],
    [위젯],
    ...
  ]
)
```

### PageView

여러 페이지를 좌우로 슬라이드하여 넘길 수 있도록 해주는 위젯

Tab과 연동하여 사용하지 않으면 좌우로 슬라이드가 가능한지 사용자가 모를 수 있어서 단독으로는 잘 사용하지 않는다.

```dart
PageView(
  children:<Widget>[
    ...
  ]
)
```

### AppBar, TabBar, Tab, TabBarView

### BottomNavigationBar

하단에 2~5개의 탭메뉴를 구성할 수 있는 위젯

### 위치, 정렬, 크기를 위한 위젯

#### Center

중앙으로 정렬시키는 위젯

#### Padding

안쪽 여백을 표현할 때 사용하는 위젯

EdgeInsets 클래스를 사용하여 설정하며 다음과 같이 여러 방법을 제공함.

앞에 const를 붙이면 컴파일 타임에 상수로 정의되어 다시 사용되는 부분이 있을 경우 메모리에 있는 값을 재사용하는 이득이 있음.

```dart
Padding(
  padding: const EdgeInsets.all(40.0),
  child:[위젯],
)
```

EdgeInsets는 여러 함수를 제공함.

all() 네방향모두 같은 값 지정

```dart
Edgeinsets.all([double])
```

only() 상하좌우 중에서 원하는 방향에만 값을 지정

```dart
EdgeInsets.only({left: , top: , right: , bottom: })
```

fromLTRB() 네방향의 값을 각각지정

```dart
EdgeInsets.fromLTRB([왼쪽],[위],[오른쪽],[아래])
```

#### Align

자식 위젯의 정렬 방향을 정할 수 있는 위젯

#### Expanded

자식 위젯의 크기를 최대한으로 확장시켜주는 위젯

여러 위젯에 동시에 적용하면 flex 프로퍼티에 정숫값을 지정하여 비율을 정할 수 있으며 기본 값은 1

```dart
Column(
  children: <Widget>[
    Expanded(
      flex: [비율], // 기본값은 1
      child: [위젯]
    ),
    Expanded(
      child: [위젯],
    ),
    Expanded(
      child: [위젯],
    ),
  ]
)
```

#### SizedBox

위젯 중에는 크기에 관련된 프로퍼티가 없는 위젯이 많은데 그러한 위젯을 특정 크기로 만들고 싶을 떄 사용

Container에 길이를 직접 지정하면 코드가 더 간결해지지만, 대부분의 위젯은 크기를 지정 프로퍼티를 가지고 있지 않기 때문에 SizedBox를 많이 사용함.

```dart
SizedBox(
  width: [가로길이],
  height: [세로 길이],
  child: [위젯],
),
```

#### Card

```dart
Card(
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(16.0),
  ),
  elevation: [실숫값], // 그림자 깊이
  child: [위젯],
)
```

### 버튼 계열 위젯

#### RaisedButton

입체감을 가지는 일반적인 버튼 위젯

```dart
RaisedButton(
  child: Text('RaisedButton'),
  color: Colors.oragne,
  onPressed: () {
    // 실행될 코드
  }
)
```

#### FlatButton

평평한 형태의 버튼

```dart
FlatButton(
  child : Text('FlatButton'),
  onPressed: () {},
)
```

#### IconButton

아이콘을 표시하는 버튼 위젯

```dart
IconButton(
  icon:Icon(Icons.add),
  color: Colors>red, // 아이콘 색상
  iconSize: 100.0,  // 기본값 24.0
  onPressed: () {},
)
```

#### FloatingActionButton

입체감 있는 둥근 버튼 위젯

### 화면 표시용 위젯

#### Text

Text 클래스의 첫 번째 인수는 필수 프로퍼티이고 이름 없는 인수이다.

```dart
Text(
  'Hello World',
  style: TextStyle(
    fontSize: 40.0,
    fontStyle: FontStyle.italic,
    fontWeight: FontWeight.bold,
    color: Colors.red,
    letterSpacing: 4.0, // 자간
  )
)
```

#### Image

네트워크에서 이미지 불러오기

```dart
Image.network('http://bit.ly/2Pvz4t8')
```

asset() 메서드로 이미지 파일을 직접 표시할 수도 있다.

이미지파일을 사용할 수 있도록 pubspec.yaml 파일을 수정해야함.

assets/와 같이 전체 폴더를 가리키면 여러 항목을 매번 작성할 필요 없음.

```
flutter:
  assets:
    - assets/
```

```dart
Image.asset('assets/sample.jpg')
```

#### Icon

```dart
Icon(
  Icons.home,
  color: Colors.red,
  size: 60.0,
),
```

#### Progress

로딩 중이거나 오래 걸리는 작업을 할 때 사용자에게 진행 중임을 보여주는 용도로 사용하는 위젯

둥근 형태의 프로그레스 바는 일반적으로 다른 화면 위에 겹쳐서 표시하므로 Stack위젯으로겹쳐서 사용함.

```dart
CircularProgressIndicator()
LinearProgressIndicator()
```

#### CircleAvatar

프로필 화면 등에 많이 사용되는 원형 위젯

child 프로퍼티에 정의한 위젯을 원형으로 만들어줌.

```dart
CircleAvatar(
  child: Icon(Icons.person),
)
```

네트워크상에 존재하는 이미지를 표시한다면 child 프로퍼티가 아닌 backgroundImage 프로퍼티에 NetworkImage 클래스를 인스턴스를 지정해야 네트워크에서 받아온 이미지가 원형으로 표시됨.

```dart
CircleAvatar(
  backgroundImage: NetworkImage([이미지 URL])
),
```
