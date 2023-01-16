---
title: Arduino学习之一（红外遥控接收）
author: 黄俭
date: '2023-01-16'
slug: arduino_IR_Remote
categories:
  - Computer
tags:
  - Arduino
---

1. 安装的IR版本是IRremote by Shirriff, zt30, ArminJo，版本3.9.0或IRRemoteControl By Cristiano Borges 1.0.0

2. 代码
 ``` C++
 #include <IRremote.h>

const int irReceiverPin = 7;
const int ledPin = 13;
IRrecv irrecv(irReceiverPin);
decode_results results;

void setup() {
  pinMode(ledPin,OUTPUT);// put your setup code here, to run once:
  Serial.begin(9600);
  irrecv.enableIRIn();

}

void loop() {
  // put your main code here, to run repeatedly:
  if(irrecv.decode(&results)){
    Serial.print("irCode:");
    Serial.print(results.value,HEX);
    Serial.print(",bits:");
    Serial.println(results.bits);
    irrecv.resume();
  }

  delay(600);

  if(results.value == 0xFFA25D){
    digitalWrite(ledPin, HIGH);
  }
  else{
    digitalWrite(ledPin,LOW);
  }

}

 
 ```