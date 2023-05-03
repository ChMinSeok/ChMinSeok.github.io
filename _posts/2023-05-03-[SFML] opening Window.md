---
layout: single
title: "SFML 윈도우 열기"
date: "2023-05-03 22:10:20 -0400"
categories: [SFML]
tags: [SFML 기초]
background: ''
---
# SFML에서 윈도우를 여는법
다음과 같이 RenderWindow 윈도우이름()으로 렌더러를 정의합니다.
```c++
sf::RenderWindow window();
/**
sf::RenderWindow::RenderWindow	(	VideoMode 	mode,
const String & 	title,
Uint32 	style = Style::Default,
const ContextSettings & 	settings = ContextSettings() 
)		
```
모드는 비디오 모드로 윈도우 창이름은 SFML TUTORIAL로 윈도우 바에서 사용가능한 기능은 Close와 resize만을 허용하도록 하겠습니다.
```c++
sf::RenderWindow window(sf::VideoMode(512,512), "SFML TUTORIAL", sf::Style::Close | sf::Style::Resize);
```
그 다음 윈도우를 열어보겠습니다.
```c++
#include <SFML/Graphics.hpp>

int main()
{
 
    sf::RenderWindow window(sf::VideoMode(512,512), "SFML TUTORIAL", sf::Style::Close | sf::Style::Resize);

    while (window.isOpen())
    {

    }
    return 0;
}   
```
이렇게 하면 윈도우 창은 열릴 것입니다. 하지만 닫는 버튼을 눌르거나 리사이즈도 반응하지 않습니다.
  
  그러기 위해선 이벤트를 처리하기 위하여 
  >sf::Event

이것이 필요합니다.

>sf::Event는 SFML에서 이벤트 처리를 위해 사용되는 클래스입니다. 이벤트는 윈도우, 마우스, 키보드 등의 사용자 입력 또는 시스템에서 발생하는 다양한 이벤트를 나타냅니다.
>sf::Event 클래스는 이러한 이벤트를 다루기 위한 다양한 멤버 변수를 가지고 있습니다. 예를 들어, sf::Event::type은 이벤트의 종류를 나타내며, sf::Event::key는 키보드 이벤트에서 눌린 키의 코드를 저장합니다. sf::Event::mouseButton은 마우스 클릭 이벤트에서 클릭한 마우스 버튼을 저장합니다.
>이벤트를 처리하기 위해서는 SFML의 이벤트 루프를 구성하고, 윈도우 객체에서 발생한 이벤트를 가져와서 처리해야 합니다. 예를 들어, 다음과 같은 코드를 사용하여 윈도우 객체에서 발생한 이벤트를 처리할 수 있습니다.

이제 윈도우 창에서의 기능들을 수행 할 수 있는 전체 코드를 보겠습니다.

```c++
#include <SFML/Graphics.hpp>

int main()
{
 
    sf::RenderWindow window(sf::VideoMode(512,512), "SFML TUTORIAL", sf::Style::Close | sf::Style::Resize);

    while (window.isOpen())
    {
        sf::Event evnt;
        while (window.pollEvent(evnt))
        {
            if (evnt.type == evnt.Closed)
            {
                window.close();
            }
        }
    }
    return 0;
}   
```
>위 코드에서 window.pollEvent(event) 함수는 윈도우 객체에서 발생한 이벤트를 가져와서 event 변수에 저장합니다. 이후에는 event.type 변수를 사용하여 이벤트의 종류를 판별하고, 각 이벤트에 맞는 처리 코드를 작성하면 됩니다.

이제 클로즈 즉 닫기를 했을때 윈도우는 닫힐 것 입니다.

