# 분리수거 교육 프로그램
## 1. Introduction
### 1.1 Background
### 1.2 Target
### 1.3 Goal


## 2. Main Contents
### 2.1 Scenario
### 2.2 Prototype
### 2.3 User Test
### 2.4 Source Code
#### 2.4.1 기본 움직임
- 주 움직임: 손가락 굽혔다 폄. 'bool finger.IsExtended' method 사용
- `bool finger[n].IsExtended` : Whether or not this Finger is in an extended posture. True, if the pointable is extended.
- 굽힘 -> 요소 선택, 잡고 요소 이동

Leap motion을 통해 인식되는 손(Hand)과 손가락(Finger) Import.
```c#
controller = new Controller();
Frame frame = controller.Frame();
List<Hand> hands = frame.Hands;
List<Finger> fingers = hands[0].Fingers;
```

leapmotion 연결 -> `controller.IsConnected`가 ture일 경우 
손 움직임에 따라 Hand Object 위치 이동

```c#
if (controller.IsConnected){
	this.transform.position = new Vector3(hands[0].PalmPosition[0] / 30, -hands[0].PalmPosition[2] / 30, 0);
        }
else this.transform.position = new Vector3(0, 0, 0);
```

'fingers[n]' : n번째 손가락 인식

손가락 접히는 것 인식하면 "Sprites/hand" 폴더의 0번째 이미지로 변경 (주먹) , 
그 외 "Sprites/hand"폴더의 1번째 이미지로 변경 (손 펼침)
```c#
if (fingers[1].IsExtended == false &
    fingers[2].IsExtended == false &
    fingers[3].IsExtended == false){
    	SpriteRenderer spriteR = gameObject.GetComponent<SpriteRenderer>(); // gameObject의 SpriteRenderer
	Sprite[] sprites = Resources.LoadAll<Sprite>("Sprites/hand");
	spriteR.sprite = sprites[0];
        }
else {
	SpriteRenderer spriteR = gameObject.GetComponent<SpriteRenderer>();
	Sprite[] sprites = Resources.LoadAll<Sprite>("Sprites/hand");
	spriteR.sprite = sprites[1];
}
```

gameObject(=this)(사용자 손)의 위치가 'target1' object의 범위 안에 있으면서 손가락을 굽히면 'How to play' Scene으로 씬 전환 
```c#
if (this.transform.position.y > target1.transform.position.y - 0.5f &
    this.transform.position.y < target1.transform.position.y + 0.5f &
    this.transform.position.x > target1.transform.position.x - 1.0f &
    this.transform.position.x < target1.transform.position.x + 1.0f &
    fingers[1].IsExtended == false){
    	SceneManager.LoadScene("How to play");
        }
```
--------

#### 2.4.2 Stage 1 미션

`hand.ParmVelocity` : The speed and movement direction of the palm in millimeters per second.

`hands[0].PalmVelocity.y' : y축에 대해 손 움직임의 속도를 측정.

-3500 이하일 때 
```c#
if (hands[0].PalmVelocity.y < -3500){
	SpriteRenderer spriteR = full.GetComponent<SpriteRenderer>();
	Sprite[] sprites = Resources.LoadAll<Sprite>("Sprites/stage1");
	spriteR.sprite = sprites[0];
        Invoke("Scenechange", 3);
}
```







## 3. Discussion
### 3.1 Limitations and future studies
### 3.2 Conclusion
### 3.3. Reference
https://developer-archive.leapmotion.com/documentation/csharp/api/Leap.Finger.html#extension-functions 
