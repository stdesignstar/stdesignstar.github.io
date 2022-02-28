---
title: 어드레서블 에셋 시스템
author: stdesignstar
date: 2022-01-29 12:00:00 +09:00
categories: [Unity]
tags: [Addressables]
math: true
mermaid: true
---

## 개요

어드레서블 에셋 시스템 정리.  

## 에셋 이란?

유니티에서 사용될 수 있는 다양한 아이템을 말한다.  
- 3D 모델, 오디오 파일, 이미지  
- Unity 가 지원하는 다른 형식의 파일 등 Unity 외부에서 생성된 파일  
- 애니메이터 컨트롤러, 오디오 믹서 및 렌더 텍스처와 같이 Unity에서 생성할 수 있는 일부 타입의 에셋  

즉, 프로젝트뷰에 보이는 보든 것들을 에셋으로 취급할 수 있다.  

![](https://docs.unity3d.com/kr/2018.4/uploads/Main/AssetWorkflowImportingFiles.png)

## 에셋번들 이란?

에셋 번들(AssetBundle)은 에셋의 묶음.  

왜 사용할까?  

1. 빌드 파일 크기 절감  
2. 런타임 메모리 압박의 감소  
3. 다운로드 가능 콘텐츠(DLC)에 유용  

## 어드레서블 에셋 이란?

에셋 번들의 생성/관리/사용 의 불편함을 해결하기 위해 만들어진 시스템으로, 에셋에 어드레스를 부여하여 에셋의 위치에 상관없이 참조가 가능하도록 만들어진 시스템이다.  

## 시작하기

유니티 프로젝트에 Addressables 패키지를 설치한다  
![](https://docs.unity3d.com/Packages/com.unity.addressables@1.19/manual/images/addr_gettingstarted_pacman.png)  

Windows > Asset Management > Addressables > Group 을 연다.  

![](/assets/img/Addressables/Addressables1.png)

Create Addressables Settings 를 클릭한다.  

![](https://docs.unity3d.com/Packages/com.unity.addressables@1.19/manual/images/addr_gettingstarted_firstuse.png)

## 에셋에 어드레스 지정

적당히 프리팹을 만들고 인스펙터창에서 Addressable 에 체크하면 어드레스를 지정할 수 있다.  

어드레서블 그룹창에서 추가된 어드레서블 에셋을 확인할 수있다.  

![](/assets/img/Addressables/Addressables2.png)

어드레서블 에셋을 사용하기 위해 컨텐츠를 빌드한다.  

Addressables Groups 창을 연 다음 Build > New Build > Default Build Script 를 선택한다.

![](/assets/img/Addressables/Addressables3.png)

여기까지 완료하면 에셋을 로드할 준비가 완료된다.  

## 어드레서블 에셋 로드하기

1. 에셋 참조 사용
    ```cs
    public class LoadAssetReference : MonoBehaviour
    {
        public AssetReference Reference;

        void Start()
        {
            Reference.LoadAssetAsync<GameObject>();
        }
    }
    ```

2. 어드레스 사용
    ```cs
    public class LoadAsset : MonoBehaviour
    {
        public string Address;
        public Transform Parent;

        private AsyncOperationHandle<GameObject> _handle;

        public void Start()
        {
            _handle = Addressables.LoadAssetAsync<GameObject>(Address);
        }
    }
    ```

3. Label 사용  
    어드레스를 사용하는 것과 같다.  
    Label과 어드레스가 같을 경우엔 랜덤하게 생성되는듯 하다. 같은 값을 사용하지 않도록 주의하자.

---

GameObject 에셋을 로드하는 경우 두가지 방법이 있다.  
1. LoadAssetAsync 를 이용해 에셋을 로드하고, Instantiate 하는 경우.
    ```cs
    _handle = Addressables.LoadAssetAsync<GameObject>(Address);
    _handle.Completed += operation =>
    {
        if (operation.Status == AsyncOperationStatus.Succeeded)
        {
            Instantiate(operation.Result, Parent);
        }
        else
        {
            Debug.LogError($"Asset for {Address} failed to load.");
        }
    };
    ```
2. InstantiateAsync 를 이용해 에셋로드와 Instantiate 를 한번에 진행하는 경우.
    ```cs
    _handle = Addressables.InstantiateAsync(Address);
    ```

## 어드레서블 에셋 해제
어드레서블 에셋을 로드한 이후, 사용이 종료되었다면 해제해줘야 한다.  
Addressables.LoadAssetAsync 을 사용한 경우엔 Addressables.Release 를,  
Addressables.InstantiateAsync 을 사용한 경우엔 Addressables.ReleaseInstance 를 사용해 해제한다.