Amazing_Golfgame
================

This is a minigolf game which has 1 level. It's very exciting, and it's a lot of fun!

![minigolf](https://user-images.githubusercontent.com/87847262/230893120-40314e34-cb8c-4531-876f-7b18283bc22b.jpg)

Instructions
-----------
  - Use space to push the ball, hold space to change the force.
  - Turn your sight with the right and left arrows.
  - You will win when you push your ball into the hole.
  - In some parts of the level, you will have to jump to another platform.

[Click Here to Play](file:///C:/Users/peanuts-english/Desktop/Amazzzzzing_golfgame_v1/index.html)
  
How it works
------------
Camera following code:

~~~c#
public GameObject ball;

void LateUpdate()
{
    transform.position = ball.transform.position;
}
~~~

Adding force to the ball code:
  - clubmr is the mesh renderer of the club which shows the power of the ball.
  - power will increase and decrease when you hold the space in line 34~49.

~~~c#
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

~~~

Level restart code :
  - SampleScene is level 1.
~~~c#
if(ball.transform.position.y<-10){
    SceneManager.LoadScene("SampleScene");
}
~~~

Camera rotate code :
  - localEulerAngles is use for changing the rotation of the ball.

~~~c#
if(Input.GetKey("left")){
    transform.localEulerAngles -= new Vector3(0,60,0) * Time.deltaTime;
    camera.transform.localEulerAngles -= new Vector3(0,60,0) * Time.deltaTime;
}
if(Input.GetKey("right")){
    transform.localEulerAngles += new Vector3(0,60,0) * Time.deltaTime;
    camera.transform.localEulerAngles += new Vector3(0,60,0) * Time.deltaTime;
}
~~~


This is the setting of the golfball :
  - I add some bouncy material to the ball, make it more realistic.

![ballphysicmaterial](https://user-images.githubusercontent.com/87847262/230895362-416db75e-d009-419a-8629-4b31fd9e4f62.jpg)
![ballrb](https://user-images.githubusercontent.com/87847262/230895669-da459d42-7050-4732-b462-6376832ad9e8.jpg)

Resources and Assets
--------------------
  - [Kenney Assets](https://www.kenney.nl/assets)
  - [MiniGolf Assets Package](https://www.kenney.nl/assets/minigolf-kit)
  - C#
  - [Unity](https://unity.com/)
