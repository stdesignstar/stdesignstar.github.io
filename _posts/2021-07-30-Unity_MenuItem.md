---
title: 유니티 에디터 MenuItem Attribute
author: stdesignstar
date: 2021-07-30 12:00:00 +09:00
categories: [Unity]
tags: [UnityEditor]
math: true
mermaid: true
---

## 개요

유니티 에디터 커스터마이징 기능 중 MenuItem Attribute에 대해 알아보도록 하자.  
해당 Attribute를 추가하면 유니티 에디터의 메뉴에 새로운 항목이 생성된다.  
이 기능은 **정적 함수** 에만 사용할 수 있다.  

| ![](/assets/img/UnityEditor/MenuItem1.png) |
| 프로젝트-메뉴1 항목이 생성되었다. |

## 정의

```cs
namespace UnityEditor
{
    public sealed class MenuItem : Attribute
    {
        public MenuItem(string itemName);
        public MenuItem(string itemName, bool isValidateFunction);
        public MenuItem(string itemName, bool isValidateFunction, int priority);
    }
}
```

## 메뉴 추가  
"string itemName" 에 원하는 이름으로 추가한다. 하위메뉴 구분은 "/"로 한다.  

## 단축키 사용
"string itemName" 에 메뉴이름을 적고 **공백** 을 준뒤 아래의 코드를 입력한다.  


- % :  Winows의 Ctrl, macOS의 cmd키  
- ＃ : shift  
- & : alt  
- 숫자나 문자 등을 사용하려면 _를 같이 사용한다. ex) G키를 사용하려면 _g  
- LEFT, RIGHT, UP, DOWN, F1 .. F12, HOME, END, PGUP, PGDN. 의 키도 사용가능  

```cs
    [MenuItem("프로젝트/메뉴1 &_g")]
    public static void Test()
    {
    }
```

| ![](/assets/img/UnityEditor/MenuItem4.png) |
| alt + G 를 누르면 메뉴가 실행된다. |


## 메뉴의 활성화
"bool isValidateFunction" 을 이용하면 메뉴를 활성화 또는 비활성화 할 수 있다.

| ![](/assets/img/UnityEditor/MenuItem2.png) |
| 메뉴가 비활성화되었다. |

```cs
    [MenuItem("프로젝트/메뉴1", false)]
    public static void Test()
    {
    }

    [MenuItem("프로젝트/메뉴1", true)]
    public static bool IsValidTestMenu()
    {
        // 이 함수의 리턴값이 "프로젝트/메뉴1" 의 활성화를 결정한다.
        // true 활성화
        // false 비활성화
        return true;
    }
```

isValidateFunction 값이 true라면 동일한 itemName 을 가지는 MenuItem 을 찾아 활성화 상태를 결정한다.  


isValidateFunction 가 true인 정적 함수가 여럿일때 하나라도 false 를 리턴하면 해당 메뉴는 비활성화된다.  

```cs
    [MenuItem("프로젝트/메뉴1", false)]
    public static void Test()
    {
    }

    [MenuItem("프로젝트/메뉴1", true)]
    public static bool IsValidTestMenu()
    {
        // 여기에선 true를 리턴했지만
        return true;
    }

    [MenuItem("프로젝트/메뉴1", true)]
    public static bool IsValidTestMenu2()
    {
        // 여기선 false를 리턴했기에 프로젝트/메뉴1 메뉴는 비활성화된다.
        return false;
    }
```

## 우선순위
"int priority" 값으로 메뉴의 우선순위를 정할 수 있다.  
값이 낮을수록 위쪽에 출력된다.  

```cs
    [MenuItem("프로젝트/메뉴2", false, 20)]
    public static void Test2()
    {
        Debug.Log("메뉴2실행");
    }

    [MenuItem("프로젝트/메뉴3", false, 10)]
    public static void Test3()
    {
        Debug.Log("메뉴3실행");
    }
```

| ![](/assets/img/UnityEditor/MenuItem3.png) |
| priority 값이 낮은 프로젝트/메뉴3 메뉴가 위쪽에 출력되었다. |

## Reference
https://docs.unity3d.com/ScriptReference/MenuItem.html  

