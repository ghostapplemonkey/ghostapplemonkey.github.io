Amazing_Golfgame
================

This is a minigolf game which has 1 level. It's very exciting, and has a lot of fun!
![minigolf](https://user-images.githubusercontent.com/87847262/230893120-40314e34-cb8c-4531-876f-7b18283bc22b.jpg)

Instruction
-----------
  - Use space to push the ball, hold space can choose the force.
  - turn your sight with right and left arrows.
  - You will win when you push your ball into the holl.
  
How it works
------------
Camera following code:
~~~c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Cameramovement : MonoBehaviour
{
    
    public GameObject ball;

    void LateUpdate()
    {
        transform.position = ball.transform.position;
    }
}
~~~
the ball moving code :
~~~c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class Club : MonoBehaviour
{
    public Rigidbody ballrb;
    public float force = 1.5f;
    public GameObject ball;
    public GameObject camera;
    public GameObject club;
    public MeshRenderer clubmr;
    float power=0;
    bool is_increase=true;
    
    void Update()
    {
        if(ball.transform.position.y<-10){
            SceneManager.LoadScene("SampleScene");
        }
        transform.position = ball.transform.position;
        if(Input.GetKey("left")){
            transform.localEulerAngles -= new Vector3(0,60,0) * Time.deltaTime;
            camera.transform.localEulerAngles -= new Vector3(0,60,0) * Time.deltaTime;
        }
        if(Input.GetKey("right")){
            transform.localEulerAngles += new Vector3(0,60,0) * Time.deltaTime;
            camera.transform.localEulerAngles += new Vector3(0,60,0) * Time.deltaTime;
        }
        if(Input.GetKey("space")){
            if(is_increase==true){
                power+=Time.deltaTime*3;
                if(power>5){
                    is_increase=false;
                    power=5;
                }
            }else{
                power-=Time.deltaTime*3;
                if(power<0.05){
                    is_increase=true;
                    power=0.05f;
                }
            }
            clubmr.enabled=true;
            club.transform.localScale = new Vector3(0.5f, 0.5f, power);
        }else{    
            ballrb.AddForce(transform.forward*force*power, ForceMode.Impulse);
            power = 0;
            clubmr.enabled=false;
        }
    }
}
~~~

Resources and Assets
--------------------
  - [Kenney Assets](https://www.kenney.nl/assets)
  - C#
  - [Unity](https://unity.com/)


