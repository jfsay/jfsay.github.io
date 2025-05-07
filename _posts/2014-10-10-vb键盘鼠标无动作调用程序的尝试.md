---
title: "VB键盘鼠标无动作调用程序的尝试"
date: 2014-10-10
categories: 
  - "software_programming"
tags: 
  - "vb"
---

我想要实现的功能是，当键盘无输入、鼠标无移动或点击动作时调用程序。首先想到的是用钩子HOOK来获取键盘或者鼠标的动作，如果无动作时调用程序。我尝试的结果是HOOK来HOOK去总是有问题。

后来想到Windows的屏幕保护程序就是当键盘鼠标无动作时进入屏幕保护的，于是改变思路，想把程序做成这样的形式，键盘鼠标无动作，系统进入屏幕保护，然后检测系统是否运行屏幕保护程序，如果运行的话则调用程序。这种方式就是以屏幕保护程序作为中介，把检测键盘鼠标动作的工作交给屏幕保护程序来完成了。SystemParametersInfo可以实现获取屏幕保护信息的函数。参考代码如下：

```
'API调用与常用定义：
Private Declare Function SystemParametersInfo _
    Lib "user32" _
    Alias "SystemParametersInfoA" _
      (ByVal uiAction As Long, _
       ByVal uiParam As Long, _
       pvParam As Any, _
       ByVal fWInIni As Long) As Boolean

Private Const SPI_GETSCREENSAVEACTIVE As Long = &H10   '屏保是否启用的常量
Private Const SPI_GETSCREENSAVERRUNNING As Long = &H72 '屏保是否运行的常量

Private Sub Timer1_Timer()
    Dim bRunning As Boolean     '屏保是否运行的变量,当然你可以定义全局变量
    SystemParametersInfo SPI_GETSCREENSAVERRUNNING, 0, bRunning, False '调用API,bRunning返回屏保运行状态
    Debug.Print Time; "屏保运行="; bRunning '演示:打印屏保是否运行的信息
End Sub

'另外,查看屏保是否启用,也可以用下面方法:
SystemParametersInfo SPI_GETSCREENSAVEACTIVE, 0, bActive, False 'bActive为返回值(逻辑型)
```

可是不知道为什么我在WIN7下调试还是有问题，提示SystemParametersInfo SPI\_GETSCREENSAVERRUNNING, 0, bRunning, False  
中的bRunning类型错误，只能作罢。

最后来说一下最终实现的方案是使用GetLastInputInfo函数获取系统的空闲时间，参考代码如下：

```
Option Explicit
Private Declare Function GetLastInputInfo Lib "user32" (plii As LASTINPUTINFO) As Boolean
Private Declare Function GetTickCount Lib "kernel32" () As Long
Private Type LASTINPUTINFO
    cbSize As Long
    dwTime As Long
End Type

Private Sub Form_Load()
     Timer1.Interval = 1000    
End Sub

Private Sub Timer1_Timer()
    Dim lii As LASTINPUTINFO
    lii.cbSize = Len(lii)
    If GetLastInputInfo(lii) Then
        If (GetTickCount - lii.dwTime) / 60000 >= 15 Then            
            Call MsgBox("由于本机15分钟没有操作，如果3分钟后没有反应，系统将强制关机", vbYesNo + vbExclamation + vbDefaultButton2, "提示")
        End If
    End If
End Sub
```
