---
title: 从command line到GUI的小程序
author: 黄俭
date: '2022-09-28'
slug: python-from-command_line-to-gui
categories:
  - Computer
tags:
  - Python
---

一道计算机等级考试Python二级的大题，输入各科成绩（科目+空格+分数），统计其中最高分科目，最低分科目和平均分。

Command Line Version:

 ```python
data = input("请输入各科成绩，科目与分数之间用空格隔开，空行回车结束输入：")
d={}
while data:
    t = data.split()
    d[t[0]] = t[1]
    data = input()
ls = list(d.items())

ls.sort(key=lambda x:x[1], reverse=True)
s1,g1=ls[0]
s2,g2=ls[len(ls)-1]

a = 0

for i in d.values():
    a = a+int(i)

a=a/len(ls)

print("最高分课程是{} {}, 最低分课程是{} {}, 平均分是{:.2f}".format(s1,g1,s2,g2,a))
 ```
 
Pyside2 GUI Version:

 ```python
from PySide2.QtWidgets import QApplication, QMainWindow, QPushButton,  QPlainTextEdit, QMessageBox

def handleCalc():
    info = textEdit.toPlainText()
    d = {}
    for line in info.splitlines():
        if not line.strip():
            continue
        parts = line.split(' ')
        parts = [p for p in parts if p]

        s,g = parts

        d[s] = g
        
    ls = list(d.items())

    ls.sort(key=lambda x:x[1], reverse=True)
    s1,g1=ls[0]
    s2,g2=ls[len(ls)-1]

    a = 0

    for i in d.values():
        a = a+int(i)

    a=a/len(ls)

    QMessageBox.about(window,'统计结果',f'''最高分的课程是：\n{s1}{g1}\n最低分的课程是：\n{s2}{g2}\n平均分是：\n{a}\n''')

app = QApplication([])

window = QMainWindow()
window.resize(500, 400)
window.move(300, 310)
window.setWindowTitle('成绩统计')

textEdit = QPlainTextEdit(window)
textEdit.setPlaceholderText("请输入各科成绩")
textEdit.move(10,25)
textEdit.resize(300,350)

button = QPushButton('统计', window)
button.move(380,80)

window.show()

button.clicked.connect(handleCalc)

app.exec_()
 ```