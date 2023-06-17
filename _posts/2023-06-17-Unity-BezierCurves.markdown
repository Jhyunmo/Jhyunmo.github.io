---
title:  "[Unity C#] Bezier Curves with Unity"
date: 2023-06-17
categories:
  - UnityStudy
tags:
  - [UnityStudy]

toc: true
toc_sticky: true

last_modified_at: 2023-06-17
---

# Bezier Curves
![Bezier_quadratic_anim-kyuniitale](https://github.com/Jhyunmo/Jhyunmo.github.io/assets/88092754/71c20a40-e9ec-459a-ac73-8850136b0457.gif){: width="80%" height="80%"}{: .align-center}
>점과 점 사이의 선형 보간(Lerp, Linear interpolation)을 이용해 그려내는 곡선

## 1. Bezier Curves의 경로를 target 객체가 계속 이동하게 하는 코드이다.

  ```c#
public class BezierCurves : MonoBehaviour 
{
    public Transform target;
    public Transform p1, p2, p3;
    public float duration;
    
    private void Start() 
    {
        StartCoroutine();
    }

    IEnumerator BezierLoop(float time)
    {
      float t = 0;

      while(true)
      {
        if(t > 1f)
        {
          t = 0;
        }

        Vector3 p4 = Vector3.Lerp(p1.position, p2.position, t);
        Vector3 p5 = Vector3.Lerp(p2.position, p3.position, t);
        target.position = Vector3.Lerp(p4, p5, t);

        t += Time.deltaTime;

        yield return null;
      }
    }
    
}
  ``` 

## 2. Gizmos를 통해 실제 곡선의 경로를 확인하는 코드이다.(위 코드에 추가)

  ```c#
  public class BezierCurves : MonoBehaviour 
{
    public float gizmoLine;

    List<Vector3> gizmoPoints = new List<Vector3>();
    private void OnDrawGizmos()
    {
      gizmoPoints.Clear();

      if (p1 != null && p2 != null && p3 != null && gizmoLine > 0)
      {
        for (int i = 0; i < gizmoLine; i++)
        {
          float s = (i / gizmoLine);
          Vector3 p4 = Vector3.Lerp(p1.position, p2.position, s);
          Vector3 p5 = Vector3.Lerp(p2.position, p3.position, s);
          gizmoPoints.Add(Vector3.Lerp(p4, p5, s));
        }
      }

      for (int i = 0; i < gizmoPoints.Count - 1; i++)
      {
        Gizmos.DrawLine(gizmoPoints[i], gizmoPoints[i + 1]); 
      }

    }
    
}
  ```
