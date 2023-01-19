---
title: Arduino学习之4位LED数码管
author: 黄俭
date: '2023-01-16'
slug: arduino-4-led
categories:
  - Computer
tags:
  - Arduino
---
我用器件是老版本，2481QL，14针，单边。

其中，D5和D6（时钟冒号），7脚接地，11号正向偏置。

1，12，5，9分别是第1，2，3，4个数码管的共阴极。

ABCDEFG，分别对应的引脚分别是14, 8, 6, 2, 4, 13, 10

DP对应第3引脚。

点亮所有LED的代码(共阳极)：

 ```C++
void setup() {
  for(int i = 2;i <= 13;i++){
    pinMode(i,OUTPUT);
  }
}
void loop() {
  for(int i = 2;i <= 9;i++){
    digitalWrite(i,LOW);
  }
  for(int i = 10;i <= 13;i++){
    digitalWrite(i,HIGH);
  }
}

 
 ```


输出数字1234（共阳极5）:

 ```C++
void setup() {
  for(int i = 2;i <= 13;i++){
    pinMode(i,OUTPUT);
  }
}
void num1(){
  digitalWrite(2,HIGH);
  digitalWrite(3,LOW);
  digitalWrite(4,LOW);
  digitalWrite(5,HIGH);
  digitalWrite(6,HIGH);
  digitalWrite(7,HIGH);
  digitalWrite(8,HIGH);
  digitalWrite(9,HIGH);
  digitalWrite(10,HIGH);
  digitalWrite(11,LOW);
  digitalWrite(12,LOW);
  digitalWrite(13,LOW);
}
void num2() {
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
  digitalWrite(4,HIGH);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(7,HIGH);
  digitalWrite(8,LOW);
  digitalWrite(9,HIGH);
  digitalWrite(10,LOW);
  digitalWrite(11,HIGH);
  digitalWrite(12,LOW);
  digitalWrite(13,LOW);
}
void num3() {
  digitalWrite(2,LOW);
  digitalWrite(3,LOW);
  digitalWrite(4,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,HIGH);
  digitalWrite(7,HIGH);
  digitalWrite(8,LOW);
  digitalWrite(9,HIGH);
  digitalWrite(10,LOW);
  digitalWrite(11,LOW);
  digitalWrite(12,HIGH);
  digitalWrite(13,LOW);
}
void num4() {
  digitalWrite(2,HIGH);
  digitalWrite(3,LOW);
  digitalWrite(4,LOW);
  digitalWrite(5,HIGH);
  digitalWrite(6,HIGH);
  digitalWrite(7,LOW);
  digitalWrite(8,LOW);
  digitalWrite(9,HIGH);
  digitalWrite(10,LOW);
  digitalWrite(11,LOW);
  digitalWrite(12,LOW);
  digitalWrite(13,HIGH);
}
void loop() {
  num1();
  delay(5);
  num2();
  delay(5);
  num3();
  delay(5);
  num4();
  delay(5);
}
 
 ```
 
0-9依次点亮（共阴极）

```C++
int Pin[8] = {2,3,4,5,6,7,8};//定义引脚数组
unsigned char Num[10][7] =
//a  b  c  d  e  f  g
{{1, 1, 1, 1, 1, 1, 0},   //0
 {0, 1, 1, 0, 0, 0, 0},   //1
 {1, 1, 0, 1, 1, 0, 1},   //2
 {1, 1, 1, 1, 0, 0, 1},   //3
 {0, 1, 1, 0, 0, 1, 1},   //4
 {1, 0, 1, 1, 0, 1, 1},   //5
 {1, 0, 1, 1, 1, 1, 1},   //6
 {1, 1, 1, 0, 0, 0, 0},   //7
 {1, 1, 1, 1, 1, 1, 1},   //8
 {1, 1, 1, 1, 0, 1, 1},   //9
};
void setup() {
  for(int i = 2;i < 9;i++){
     pinMode(i,OUTPUT);
     digitalWrite(i,HIGH);
  } 
  
}
void loop() {
 
  for(int j = 0;j < 10;j++){
    for(int i = 0;i < 9;i++){
      digitalWrite(Pin[i],Num[j][i]);
    }
    delay(1000);
  }
}

```