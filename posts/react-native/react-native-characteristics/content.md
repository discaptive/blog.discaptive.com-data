---
title: "React Native만의 특징들"
date: 2024-10-30
description: "React Native만이 가진 특징들에 대해서 소개합니다. 근데 이제 진짜 특징만 모은.."
thumbnail: "https://github.com/user-attachments/assets/6988f083-1eaf-4e91-9856-9dca32ed54e5"
---

<Callout type="info">
React Native는 장점과 단점이 모두 있지만, 이 글에서는 React Native의 고유한 특징에 중점을 두고 소개합니다.
</Callout>

## React Native가 뭔가요?

[React Native(리액트 네이티브)](https://reactnative.dev/)는 Facebook(현 Meta)이 개발하고 2015년에 출시한 오픈 소스 프레임워크로, JavaScript를 사용해 iOS와 Android용 모바일 애플리케이션을 동시에 개발할 수 있게 해줍니다.

크로스플랫폼 모바일 개발 프레임워크는 굉장히 많습니다.

![market research (Statista)](https://github.com/user-attachments/assets/3da738ef-7331-448f-b82d-f45865f80c57)

그 중 단연 2위[(출처)](https://www.statista.com/statistics/869224/worldwide-software-developer-working-hours/)에 빛나는 프레임워크라고 하네요. 많은 사람들이 쓰고, 지금도 여전히 사랑 받고 있네요. ~~(어쩌면 2024년에는 .NET MAUI가 껴있을 수도 있으려나요)~~

## React Native만의 특징

React Native**만**이 가진 특징들에 대해 소개하려고 합니다. 그래야 모바일 크로스플랫폼 프레임워크를 고르는 좋은 소개가 되지 않을까 싶습니다. 아무래도 제가 접해봤고, 현 점유율 1위에 빛나는 `Flutter`와 비교를 하는 게 보기에는 좋을 것 같아서 그런식으로 소개가 될 것 같습니다.

### React와 유사한 개념들

React Native는 React를 기반으로 하고 있습니다. React Native에도 똑같이 컴포넌트와 상태 관리의 원리가 적용되기에 React를 기존에 하셨던 분들이라면 React Native 어렵지 않게 하실 수 있을 거라고 말씀드리고 싶습니다.

> 이제 반대로 React Native를 배운 분들은 웹 프론트에도 어렵지 않게 도전할 수 있지 않을까요? ~~근데 CSS는 진짜 못하겠어요~~

### 네이티브 퍼포먼스

<Callout type="warn">
성능 얘기 아닙니다.
</Callout>

Flutter를 하다가 React Native를 처음 접해봤을 때 좋았던 경험은 네이티브의 컴포넌트를 사용할 수 있다는 점이었습니다.

![Fireship - React Native in 100 Seconds](https://github.com/user-attachments/assets/5b0450f0-e0ce-47d5-bd54-4c6997b41cb9)

JavaScript로 네이티브 컴포넌트, 네이티브 모듈을 `Bridge`를 통해 사용할 수 있기 때문에 View, Button, GPS, Bluetooth, Camera 등등 사용자 경험을 해당 OS에 맞게 제공할 수 있다는 점이 인상 깊었습니다.

![Core Components - Alert.alert()](https://github.com/user-attachments/assets/a0aeaa27-aeb3-47d2-8786-69bf479122ca)

바로 이런식으로 말이죠.

![React Native Components Diagram](https://github.com/user-attachments/assets/0dfee170-86a0-41b8-b17a-2bc41106f8a6)

실제로 React Native에서 공식적으로 Core Components로 네이티브 컴포넌트를 지원하는 게 많습니다. 이외에도 커뮤니티에서 만든 수많은 써드파티 라이브러리를 이용하면 그 무엇이든 Native Components로 구성할 수 있습니다.

Flutter는 `Skia` 그래픽 엔진을 통해 모든 UI를 자체 렌더링하기 때문에 새하얀 도화지에 UI를 하나씩 차곡차곡 쌓아가는 느낌입니다. 개인적으로 플러터를 하면서 사용자 경험 입장에서는 네이티브만의 감성을 전혀 줄 수 없겠다고 생각했어요.

> Flutter에서도 Cupertino의 위젯들을 많이 지원하지만 사용해보면 "아 정말 흉내만 냈구나" 싶은 부분들이 너무나도 많아요. CupertinoPageScaffold에서 네비게이션 타이틀 보고 좀 적잖은 충격을 받긴 했습니다 ㅋㅋ..

물론, `MethodChannel`을 통해 네이티브 모듈(GPS, Blutetooth, etc..)과 소통은 가능하지만 플러터에서 네이티브 컴포넌트를 사용할 수 없다는 건 아쉬웠습니다.

이건 어떻게 보면 양날의 검이 될 수도 있는 특징일 것 같습니다.

- 네이티브의 컴포넌트를 사용하면 사용자 경험을 네이티브로 줄 수 있는 장점이 있습니다.
- 하지만 모두가 동일한 UI를 보는 건 어렵겠죠. 즉, UI에 대한 일관성을 보장할 수 없습니다.

### 네이티브 코드 통신을 위한 Bridge

많은 분들이 React Native와 Flutter를 비교하면서 얘기하는 대표적인 예시가 성능에 관한 퍼포먼스입니다.

위에 언급했듯이 `Bridge`라는 JavaScript 코드와 네이티브 코드 간의 통신을 가능하게 해주는 **중재자**가 존재하기에 고사양 그래픽이나 애니메이션이 필요한 경우, 혹은 엄청난 양의 데이터를 Bridge를 통해 주고 받게 되면 Flutter에 비해 성능이 저하됩니다.

제가 직접 성능 비교를 해본 적은 없어서 구글에 Flutter vs React Native Performance 비슷한 키워드로 검색하시면 많은 자료들이 나오니 궁금하시다면 찾아보시는 걸 추천드립니다.

### 코드 푸시 - 그것은 가뭄에 단비

앱 개발자들은 매번 **스토어 심사**라는 것에 시달리며 살 거라고 확신합니다. 웹의 배포 프로세스 사이에 구글과 애플의 감시를 받아야 한다는 거죠.

React Native에는 2025년 3월 이후로 중단되는 App Center의 CodePush가 제일 유명했던 서비스인 것 같습니다. 대안은 여러가지가 여전히 남은 걸로 보입니다. [EAS Update(유료)](https://docs.expo.dev/eas-update/introduction/), CodePush는 [Standalone(무료)](https://github.com/microsoft/code-push-server)으로 남게된다고 하네요.

Flutter에도 (비교적) 최근에 코드 푸시가 가능한 서비스가 나왔습니다.

![ShoreBird](https://github.com/user-attachments/assets/c674c388-91ab-4e87-b389-ddd7dc5096a4)

그것은 바로 [ShoreBird](https://shorebird.dev/)라는 건데요, 이게 사실 1년 전만 해도 가격이 굉장히 부담되는 가격이었는데 현재는 부담되는 가격은 아닌 것 같습니다. 다만, iOS가 최근 알파 버전에서 베타 버전으로 바뀌었다는데 아직은 여전히 시기상조일까요..?

(코드 푸시를 통해 앱 성격을 바꿀 정도로 너무 많은 걸 바꾸면 심사 거절의 사유가 될 수도 있다고 하는 것 같습니다.)

> OK(?) that does not change the primary purpose of the Application by providing features or functionality that are inconsistent with the intended and advertised purpose of the Application ~

## 마치며

간단하게 React Native의 고유 특징임 뭐가 있는지 봤는데요, 각각의 크로스플랫폼 프레임워크마다 장단점이 많이 달라서 뭐가 더 낫고 더 별로인지 판단하기는 쉽지 않은 것 같습니다.

-끗-
