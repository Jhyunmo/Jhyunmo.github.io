---
title:  "[Unity C#] Notch Design에 대응하는 SafeArea" 
date: 2023-05-29
categories:
  - UnityStudy
tags:
  - [UnityStudy]

toc: true
toc_sticky: true

last_modified_at: 2023-05-29
---

# Notch Design
>모바일 해상도를 대응하는 과정에서 Notch Design이라는 카메라가 전면부로 노출되면서 이에 대한 대응이 필요하게 되었다.

# SafeArea
>Game창에서 Simulator로 상태를 변경한 후 SafeArea를 켜주면 노란색으로 나오는 테두리를 확인할 수 있다.
>유니티에서 제공하는 Screen.safeArea로 Notch 영역의 폭과 너비를 가져올 수 있다.

## 1. Canvas 하위에 빈 오브젝트를 만들고, 해상도에 영향을 받지 않도록 Anchor Preset을 Stretch Stretch로 변경한다.
## 2. 빈 오브젝트에 SafeArea script를 적용한다.

  ```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SafeArea : MonoBehaviour 
{
    private void Awake() 
    {

        RectTransform rt = GetComponent<RectTransform>();
        Rect safeArea = Screen.safeArea;
        Vector2 minAnchor = safeArea.position;
        Vector2 maxAnchor = minAnchor + safeArea.size;

        minAnchor.x /= Screen.width;
        minAnchor.y /= Screen.height;
        maxAnchor.x /= Screen.width;
        maxAnchor.y /= Screen.height;

        rt.anchorMin = minAnchor;
        rt.anchorMax = maxAnchor;

    }
    
}
  ``` 
