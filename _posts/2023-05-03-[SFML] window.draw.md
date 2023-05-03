---
layout: single
title: "[SFML] 도형 그리기, 더블 버퍼링"
date: "2023-05-03 22:10:20 -0400"
categories: [SFML]
tags: [SFML 기초]
background: ''
---
## 도형 RectangleShape정의
```c++
#include <SFML/Graphics.hpp>
#include <iostream>

int main()
{
 
    sf::RenderWindow window(sf::VideoMode(512,512), "SFML TUTORIAL", sf::Style::Close | sf::Style::Resize);
    sf::RectangleShape player(sf::Vector2f(100.0f, 100.0f));
    player.setFillColor(sf::Color::Magenta);
    while (window.isOpen())
    {
        sf::Event evnt;
        while (window.pollEvent(evnt))
        {
            switch (evnt.type)
            {
            case sf::Event::Closed:
                window.close();
                break;
            }
      
        }
        window.draw(player);
        window.display();
    }
    return 0;
}   
```
>sf::RectangleShape player(sf::Vector2f(100.0f, 100.0f));
  
    
      

이 구문을 사용하여 player라는 이름을 가진 도형 객체를 만들었다.
  

## SFML에서의 더블 버퍼링

window.draw()만 사용하면 도형이 출력되지 않는다.

>SFML에서 window.draw(player) 함수를 호출하여 화면에 그래픽 객체를 그려도, 그린 그래픽이 실제로 화면에 나타나려면 window.display() 함수를 호출해야 합니다. 이는 SFML에서 사용하는 더블 버퍼링(Double buffering) 기술 때문입니다.
더블 버퍼링은 그래픽을 렌더링하는 동안 발생할 수 있는 화면 깜빡임을 줄이기 위해 사용되는 기술입니다. 이를 위해 두 개의 그래픽 버퍼를 사용하여 렌더링된 그래픽을 화면에 출력하기 전에 백 버퍼(Back buffer)에 보관한 후, 프론트 버퍼(Front buffer)에 보관된 그래픽과 교체하여 출력합니다. 이 과정에서 window.display() 함수를 호출함으로써 백 버퍼에 저장된 그래픽을 프론트 버퍼로 교체하고, 화면에 출력합니다.
따라서, window.draw(player) 함수만 호출하여 그래픽 객체를 그렸다고 해서 화면에 나타나지 않는 것은 정상적인 동작입니다. 그린 그래픽을 실제로 화면에 출력하려면 window.display() 함수를 호출해야 합니다.