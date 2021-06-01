# 분리수거를 위한 
이렇게 하면 된다. 



```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using Leap;
using Leap.Unity;
using UnityEngine.SceneManagement;
```

```c#
public class First : MonoBehaviour
{
    Controller controller;
    public GameObject target1;
    public GameObject target2;
    public GameObject target3;

    // Start is called before the first frame update
    void Start()
    {
    }

    // Update is called once per frame
    void Update()
    {
        controller = new Controller();
        Frame frame = controller.Frame();
        List<Hand> hands = frame.Hands;
        List<Finger> fingers = hands[0].Fingers;
        
        if (controller.IsConnected){
            this.transform.position = new Vector3(hands[0].PalmPosition[0] / 30, -hands[0].PalmPosition[2] / 30, 0);
            }
        else this.transform.position = new Vector3(0, 0, 0);
        
        if (fingers[1].IsExtended == false &
            fingers[2].IsExtended == false &
            fingers[3].IsExtended == false){
                SpriteRenderer spriteR = gameObject.GetComponent<SpriteRenderer>();
	            Sprite[] sprites = Resources.LoadAll<Sprite>("Sprites/hand");
	            spriteR.sprite = sprites[0];
            }
        else {
            SpriteRenderer spriteR = gameObject.GetComponent<SpriteRenderer>();
	            Sprite[] sprites = Resources.LoadAll<Sprite>("Sprites/hand");
	            spriteR.sprite = sprites[1];
        }

        if (this.transform.position.y > target1.transform.position.y - 0.5f &
            this.transform.position.y < target1.transform.position.y + 0.5f &
            this.transform.position.x > target1.transform.position.x - 1.0f &
            this.transform.position.x < target1.transform.position.x + 1.0f &
            fingers[1].IsExtended == false){
                SceneManager.LoadScene("How to play");
            }

        if (this.transform.position.y > target2.transform.position.y - 0.5f &
            this.transform.position.y < target2.transform.position.y + 0.5f &
            this.transform.position.x > target2.transform.position.x - 1.0f &
            this.transform.position.x < target2.transform.position.x + 1.0f &
            fingers[1].IsExtended == false){
                SceneManager.LoadScene("Loading");
            }

        if (this.transform.position.y > target3.transform.position.y - 0.5f &
            this.transform.position.y < target3.transform.position.y + 0.5f &
            this.transform.position.x > target3.transform.position.x - 0.5f &
            this.transform.position.x < target3.transform.position.x + 0.5f &
            fingers[1].IsExtended == false){
                SceneManager.LoadScene("quit");
            }
    }
}

```
