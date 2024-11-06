---
title: "Flutter에서 Carousel Slider 만들기"
date: 2024-11-06
description: "PageView를 이용해 간단하게 Carousel Slider를 만들어봅시다."
thumbnail: "https://github.com/user-attachments/assets/becddb30-a06f-4cac-a1c0-fee0e5387fa2"
---

## 외부 패키지를 이용할까?

Carousel Slider 관련한 패키지는 굉장히 많고 다양합니다.

![carousel_slider](https://github.com/user-attachments/assets/e0957e02-a4b7-402f-9509-5d5d9ad0afd8)

대표적으로 [carousel_slider](https://pub.dev/packages/carousel_slider) 패키지를 많이 이용하기도 하구요. Likes가 무려 5552개가 찍혀 있네요 ㄷㄷ.

> 개인적으로 위 패키지 사용하면 너무 좋습니다. 사용 방법도 굉장히 간단하고, 구현에 공을 들여야 하는 infinite loop도 지원해줍니다.

근데 이미 플러터에서 내부적으로 `PageView` 위젯을 지원해주기 때문에 이를 활용해 직접 만들어보기로 했습니다.

## 동작 이해하기

PageView를 이용한 `Carousel Slider`의 동작 방식

1. Timer로 자동으로 page 옆으로 넘겨지기
2. 끝 페이지에 도달하면 다시 처음으로 돌아가서 자동으로 page 옆으로 넘겨지기

## 구현하기

![PageController](https://github.com/user-attachments/assets/03cb5c09-7304-465e-9d9c-c272c301807d)

`PageController` 클래스에는 `animateToPage` 메소드가 존재합니다. 이 메소드를 활용해 Timer가 trigger 될 때 animateToPage를 호출하도록 합니다.

### 코드

```dart {16, 18, 28-29, 35-41, 45, 47, 49}
import 'dart:async';

import 'package:flutter/material.dart';

class CarouselSlider extends StatefulWidget {
  const CarouselSlider({super.key, required this.children, required this.aspectRatio});

  final List<Widget> children;
  final double aspectRatio;

  @override
  State<CarouselSlider> createState() => _CarouselSliderState();
}

class _CarouselSliderState extends State<CarouselSlider> {
  final PageController _pageController = PageController();
  int _currentIndex = 0;
  late Timer _timer;

  @override
  void initState() {
    super.initState();
    _startAutoScroll();
  }

  @override
  void dispose() {
    _pageController.dispose();
    _timer.cancel();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AspectRatio(
      aspectRatio: widget.aspectRatio,
      child: PageView(
        controller: _pageController,
        children: widget.children,
      ),
    );
  }

  void _startAutoScroll() {
    _timer = Timer.periodic(const Duration(seconds: 5), (timer) {
      if (_pageController.hasClients) {
        _currentIndex = (_currentIndex + 1) % widget.children.length;

        _pageController.animateToPage(
          _currentIndex,
          duration: const Duration(milliseconds: 500),
          curve: Curves.easeInOut,
        );
      }
    });
  }
}

```

<Callout type="warn">
`_pageController`와 `_timer`를 parent widget을 dispose 해줄 때 같이 정리해주면서 혹시 모를 메모리 누수를 방지해줍시다.
</Callout>

<Callout type="info">
`_currentIndex = (_currentIndex + 1) % widget.children.length;` 이 expression은 예를 들어 총 5개의 widget을 가진 carousel slider라면 _currentIndex가 0~4 사이만 가질 수 있게 length를 나눈 나머지 값을 다시 _currentIndex 값에 대입하며 유지해줍니다.
</Callout>

## 결과
![Carousel Slider](https://github.com/user-attachments/assets/44104239-ce05-4a68-be27-627bfeec4c66)

## 개선해야할 점

크게 두 가지가 있습니다.

- infinite loop을 지원하지 않습니다. 현재 마지막에서 처음으로 돌아갈 때 왼쪽으로 쭉 다시 당기는 애니메이션을 볼 수 있습니다. 이를 무한으로 구현하게 개선하면 좋을 것 같습니다.
- 현재 사용자가 스크롤 하여 조정하면 `_currentIndex` 값이 변경되어 반영되고 있지 않습니다. 사용자가 page를 변경할 때 혹은 변경하고 나면 현재 페이지를 `_currentIndex`에 반영해줄 필요가 있습니다.

-끗-
