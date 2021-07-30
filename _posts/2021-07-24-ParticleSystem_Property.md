---
title: 유니티 파티클 시스템 속성 & 모듈 정리
author: stdesignstar
date: 2021-07-24 01:00:00 +09:00
categories: [Unity]
tags: [Unity, ParticleSystem]
math: true
mermaid: true
---

## 개요

유니티 파티클 시스템의 속성과 모듈 정보를 정리해 보고자 한다.

<br>

---

## 기본속성  

 - **Duration** : 파티클 시스템의 재생시간  

 - **Looping** : 반복사용 설정  

 - **Prewarm** : Looping이 선택되면 활성화된다. 한 사이클( One Duration )이 이미 완료된 상태에서 파티클 시스템이 동작한다.  

 - **Start Delay** : 시작 시간의 지연  

 - **Start Lifetime** :  입자의 재생시간  

 - **Start Speed** : 입자의 시작 속도  

 - **3D Start Size** : 체크하면 **Start Size** 를 X, Y, Z축 각각 설정할 수 있다.  

 - **Start Size** : 입자의 시작 크기  

 - **3D Start Rotation** : 체크하면 **Start Rotation** 을 X, Y, Z축 각각 설정할 수 있다.  

 - **Start Rotation** : 파티클의 시작 시 회전 값을 설정  

 - **Flip Rotation** : 0.0~ 1.0 사이의 값을 설정. 반대방향으로 회전시킬 정도를 설정한다.  
    1이라면 모든 입자가 회전값이 반대가 된다.

 - **Start Color** : 입자의 시작 시 색상을 설정  

 - **Gravity Modifier** : 입자가 중력에 영향을 받을 지를 설정  
 
 - **Simulation Space** : 파티클이 동작하는 환경이 World, Local, Custom 인지 설정한다.

 - **Simulation Speed** : 파티클 시스템의 동작 환경의 시간을 설정한다. 파티클의 속도, Duration의 감소 등이 영향을 받는다.  

 - **Delta Time** : Unscaled 와 Scaled 값을 설정한다. Scaled는 Time.timeScale에 영향을 받는다.  

 - **Scaling Mode** : 파티클의 스케일에 영향을 주는 방법을 설정한다.  
    Local : 입자의 크기는 파티클 오브젝트의 스케일로만 크기조절을 한다.  
    Hierarchy : 입자의 크기는 하이어라키 상의 부모로부터 스케일 값을 상속받는다.  
    Shape : 입자의 크기는 변하지 않고 하이어라키 상의 부모로부터 스케일 크기만큼 방출된다. 

 - **Play On Awake** :  파티클 시스템의 시작 설정을 한다. Play On Awake 설정을 해제하고, 스크립트로 시작 및 정지를 설정한다. 선택하면 활성화되면 파티클 시스템이 실행된다.

 - **Emitter Velocity** : 파티클 시스템이 속도를 계산하는데 Rigidbody 또는 Transform을 사용할지를 설정합니다.

 - **Max Particles** : 최대 파티클의 수를 설정합니다.

 - **Auto Random Seed** : 입자의 방출 시드값을 랜덤하게 설정한다. 파티클이 항상 일정한 모양을 유지해야 한다면 해제한다.

 - **Stop Action** : 파티클 시스템이 정지한 후의 행동을 설정한다.  

 - **Culling mode** : 파티클 시스템이 방출한 입자가 스크린을 벗어나면 취할 행동을 설정한다.   
    Pause : 입자가 화면에서 벗어나면 시뮬레이션을 중단한다.  
    Pause and Catch-up : 화면에서 벗어나면 시뮬레이션을 중단하고, 다시 진입하면 정지되지 않았다면 시뮬레이션이 도달해야하는 단계까지 행동을 하기 위해 대규모 단계를 수행한다. 성능이 순간적으로 크게 저하될 수 있다.  
    Always Simulate : 스크린상에 있지 않아도 시뮬레이션 한다. 불꽃놀이 같은 일회성 효과에 유용하다.  
    Automatic : 반복 설정한 경우에는 Pause, 기타 시스템에는 Always Simulate를 한다.  
 
 - **Ring Buffer Mode** : 입자의 재활용 설정  
    Disabled : 시스템이 수명이 경과한 파티클을 제거  
    Pause Until Replaced : 수명을 다한 오래된 파티클을 일시정지했다가 Max Particles 한계에 도달하면 시스템에서 재활용하여 새 파티클로 다시 표시한다.  
    Loop Until Replaced : 수명을 다한 파티클이 특정한 수명 비율 지점으로 다시 돌아가며, Max Particles 한계에 도달하면 시스템에서 재활용하여 새 파티클로 다시 표시되게 한다.  

<br>

---

## Emission

방출되는 입자의 개수를 설정한다.  
![](/assets/img/UnityParticleSystem/emission.png)  

초당 방출하는 입자는 Duration 동안에 초당 지속적으로 생성된다.  

Bursts는 Duration 동안에 Cycles 수 만큼 Interval 간격으로 Count의 입자를 방출한다.  

- **Rate Over Time** : 초당 방출하는 입자 수를 설정한다.

- **Rate Over Distance** : Unit을 기준으로 거리당 방출하는 입자 수를 설정한다.

<br>

- **Bursts** : 입자를 한번에 방출한다. +- 를 사용해 추가하거나 제거할 수 있다.

- **Time** : 시작 시간을 연기한다. 

- **Count** : 한번에 방출하는 입자의 숫자를 설정한다.

- **Cycles** : Duration 동안에 방출하는 숫자를 설정한다.

- **Interval** : 방출 간격을 설정한다.

- **Probability** : 방출 확률을 설정한다. 0.0~ 1.0 사이의 값을 가지며, 0%~100%를 의미한다.

<br>

---

## Shape

파티클이 방출되는 모양을 설정한다.  
![](/assets/img/UnityParticleSystem/shape.png)  

 - **Radius Thickness** : Shape의 면에서만 방출되기를 원한다면 0, 면과 내부에서도 랜덤하게 방출되기를 원한다면 1  

 - **Arc** : Shape의 특정 각 내에서 방출되도록 설정한다.  
	Mode : Random, Loop, Ping-Pong, Burst Spread  
	Spread(0~1) : 입자가 값만큼 이동되어 방출된다. (1로 설정하면 한방향으로만 방출된다.)  
	(Spread 를 0.1로 두고 Mode를 변경해보면 이해가 쉽다)  

 - **Emit from**
    Base : Shape 의 아랫부분에서 입자가 방출된다.  
	Volume : Volume으로 설정하면 Length필드가 활성화되는데, Shape의 높이를 Length 값으로 설정할 수 있다.  

 - **Sprite-Texture** : 설정된 텍스쳐 위치의 컬러값으로 입자가 방출된다.

 - **Align To Direction** : 입자가 방출되는 노멀벡터 방향으로 회전된다.

 - **Spherize Direction** : 입자가 Shape 모양대로 방출될지 결정한다.

 - **Randomize Position** : 입자가 방출되는 위치에 랜덤값을 부여한다.

<br>

---

## Velocity Over Lifetime

입자가 생성되고 사라지질 때까지의 추가속도(등속도)를 조절한다. 직선, 궤도 벡터 값을 사용하며, 입자를 대각선으로 나가게 하거나, 회전하도록 설정할 수 있다.  

Orbital X,Y,Z : 소용돌이를 만들때 사용한다.
Offset - Radial : 소용돌이의 반경을 점점 더 늘린다.
Speed Modifier : 속도를 추가적으로 조정한다.

![](/assets/img/UnityParticleSystem/velocityoverlifttime.gif)  

<br>

---

## Limit Velocity Over lifetime

입자의 속도를 제한한다. 제한 속도를 초과할 경우 속도가 감소하는 비율 등을 설정할 수 있다.  
 - **Speed** : 값만큼 입자의 속도를 제한한다.
	Dampen(0~1) : 적용정도
 - **Drag** : 입자의 속도를 제한하는 거리  

 | ![](/assets/img/UnityParticleSystem/limitvelocityoverlifetime.gif) |
 | 둘다 같은 속도의 파티클이지만, 오른쪽은 속도가 제한된 파티클 |

<br>

---

## Inherit Velocity

입자가 부모로부터 속도를 상속받도록 설정한다. Simulation Space 가 World 일때만 동작한다.  
Mode Initial은 입자 생성 시 한번만 상속을 받도록 설정하며, Mode Current은 지속적으로 계속 영향을 받는다.  
Multiplier는 속도를 상속받는 비율을 설정한다.  


부모 오브젝트의 속도를 상속받기때문에, Start Speed 값을 0으로 설정하고 사용하면 쉽게 이해가 된다.  

<br>

---

## Force Over Lifetime 

입자가 활성화된 시간동안 힘을 가한다.  
**Velocity over Lifetime** 과 비슷한 기능이지만, 등속도가 아닌 힘을 가하는 것이라 좀더 표현이 자연스럽다.  

<br>

---

## Color over Lifetime 

입자가 활성화된 시간 동안의 색상을 설정한다. Gradient 모드를 사용하여, 색상 및 알파 값을 조절할 수 있다.

<br>

---

## Color by Speed

입자의 속도에 따라 입자의 컬러를 변경한다.

<br>

---

## Size over Lifetime

Lifttime동안 입자의 크기를 변경한다.

<br>

---

## Size by Speed

입자의 속도에 따라 입자의 크기를 변경한다.

<br>

---

## Rotation over Lifetime

Lifttime동안 입자의 각도를 변경한다.  

<br>

---

## Rotation by Speed

입자의 속도에 따른 입자의 각도를 변경한다.  
언덕에서 돌이 굴러떨어지는 경우를 만들때 사용하면 좋다.

<br>

---

## External Forces 

윈드 존 (Wind Zone)에 영향을 받는 정도를 설정한다.  

Game Object → 3D → Wind Zone

<br>

---

## Noise

입자의 이동방향이나 크기 회전의 값을 비규칙적으로 설정하고 싶을때 사용한다.

<br>

---

## Collistion

바닥이나 월드에 출돌처리가 필요할 경우 사용한다. (부하가 심하므로 모바일에선 되도록 사용하지 않는다.)

<br>

---

## Triggers

대상 게임 오브젝트와 충돌 판정을 설정한다. 대상 게임 오브젝트와 충돌하면 입자를 사라지게하거나, 통과하도록 설정한다.  
충돌 후 Callback 함수를 호출하도록 설정할 수 있다.  

<br>

---

## Sub Emitters

입자가 생성, 충돌, 파괴되었을때, 서브 파티클을 방출하도록 설정한다.  
불꽃놀이를 예를 들 수 있다.  
Sub Emitter로 설정된 파티클 시스템은 현재 파티클 시스템의 하위 요소에 있어야 한다.  
파티클은 Sub Emitter의 Bursts를 방출한다.

<br>

---

## Texture Sheet Animation
Texture Sheet 의 이미지를 순서대로 사용하고 싶을때 사용한다.

<br>

---

## Lights

입자에 빛(라이트)를 추가 설정한다.

<br>

---

## Trails
입자가 이동할때 꼬리를 남긴다.
 - **Mode**
    - Particles
	- Ribbon : 담배연기 같은 이펙트를 만들때 사용한다.

 - **Minimum Vertex Distance** : 입자가 이동할때 꼬리가 좀더 자연스럽도록 설정할때 사용한다.

<br>

---

## Custom Data
셰이더를 통해 추가적인 처리가 필요할때 사용한다. 사용하려면 Renderer의 Custom Vertex Streams 가 설정되어야 한다.

<br>

---

## Renderer

 - **Render Mode**  
    Billboard : 항상 카메라를 향하도록 설정한다.  
    Vertical Billboard : 파티클이 월드 Y축과 평행하게 있으며, 카메라를 향한다.  
    Horizontal Billboard : 파티클이 월드 XZ와 평행하게 있는다.  
    Stretched Billboard : 파티클에 다양한 스케일이 적용되며, 카메라를 향한다.  

 - **Normal Direction** : 파티클 그래픽스에 사용되는 조명 노멀의 바이어스(Vias)이다. 값이 1.0이면 노멀이 카메라를 향하고, 값이 0.0이면 화면 중앙을 향한다. (Billboard only)  

 - **Material** : 입자에 적용되는 머티리얼을 설정한다.  

 - **Trail Material** : Trail에 적용되는 머티리얼을 설정한다.  

 - **Sort** : 입자가 그려지는 순서를 설정한다.  

 - **Sorting Fudge** : 다른 파티클 시스템이나 게임 오브젝트와의 파티클 시스템의 정렬 순서 설정이다. 값이 낮으면 다른 파티클 시스템을 포함한 다른 투명한 게임 오브젝트에 그려지는 상대적인 기회가 늘어난다.  

 - **Min Particle Size** : 스크린에 표시할 최소 파티클의 크기를 설정한다.  

 - **Max Particle Size** : 스크린에 표시할 최대 파티클의 크기를 설정한다.  

 - **Render Alignment** : Billboard 모드에서 파티클이 정렬되는 것을 설정한다. View 뷰포트를 바라보도록 설정하거나, Local과 일치하도록 설정 등을 할 수 있다. 

 - **Flip** : 0.0~1.0 사이의 값을 가지며, 지정된 축을 따라 파티클의 일부분을 미러링 한다.

 - **Allow Roll** : 카메라를 향한 파티클이 카메라의 Z 축을 따라 회전 가능한지 여부를 제어합니다. 이 옵션을 비활성화하는 것은 HMD 롤로 인해 파티클 시스템에서 원하지 않는 결과가 도출될 수 있는 VR 애플리케이션의 경우 특히 유용합니다(Unity documents).

 - **Pivot** : 피벗을 설정한다. 피벗의 오프셋을 통해 회전 중심을 변경한다. 

 - **Visualize Pivot** : 피벗을 보이도록 설정한다.

 - **Masking** : Mask 설정을 한다.

 - **Apply Active Color Space** : 리니어 색 공간에서 렌더링 하는 경우 시스템이 파티클을 GPU에 업로드하기 전에 감마 공간의 파티클 컬러를 전환합니다. 

 

 - **Custom Vertex Streams** : 머티리얼의 버텍스 셰이더에서 어떤 파티클 프로퍼티를 사용할지 설정한다. 

 - **Cast Shadows** : 그림자를 사용할지를 설정한다. 

 - **Receive Shadows** : 그림자 효과를 파티클에 캐스팅하도록 설정한다. 불투명한 머티리얼만 그림자가 적용될 수 있다.

 - **Shadow Bias** :  조명 방향으로 그림자를 움직여 빌보드를 사용한 근사로 인해 발생하는 그림자 결함을 제거합니다.

 

 - **Motion Vectors** : 모션 벡터를 설정한다. 

 - **Sorting Layers ID** : 정렬 레이어를 설정한다. 

 - **Order in Layer** : 정렬 레이어 내에서의 렌더링 설정을 한다. 

 - **Light Probes** : 라이트 프로브를 사용하여 빛 효과를 보정할지를 설정한다. 

 - **Reflection Probes** : 반사 프로브를 사용하여, 반사 효과를 보정할지를 설정한다.