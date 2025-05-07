---
title: "屏幕锁PcLocker更新"
date: 2014-10-11
categories: 
  - "software_programming"
tags: 
  - "vb"
---

最近把以前写的一个小程序[PClock](http://www.jfsay.com/archives/37.html "电脑屏幕锁PClock")做了一次更新，以前的程序是程序运行后系统界面锁定，需输入密码方能解锁。这次更新后的效果是，程序运行以后在后台监视空闲的时间（键盘和鼠标无动作），当空闲的时间等于设定时间时Windows系统界面锁定。

就是这么一个小功能的更新，花了我3天的时间，主要原因是走了不少的弯路。在差不多要放弃的时候让我找到了[解决的方法](http://www.jfsay.com/archives/812.html "VB键盘鼠标无动作调用程序的尝试")。

程序的界面和功能没有太大的改变，以下是程序的ChangeLog：

1、程序的名称从PClock改为PcLocker

2、程序转为后台运行，当系统空闲时锁定Windows系统，类似于进入屏幕保护程序

3、改变了[禁用任务管理器](http://www.jfsay.com/archives/813.html "VB禁用Ctrl-Alt-Delete/任务管理器的方法")的方式

4、实现了[手工无法修改配置文件](http://www.jfsay.com/archives/969.html "防止文件被改写的简单实现方式")

5、优化并精简了代码

6、程序适用于Windows XP、Windows 7，其他的系统没有测试

7、初始密码123，程序默认空闲启动时间为10分钟，默认随机自启动关闭

源程序的下载地址：[点我](https://drive.google.com/file/d/0BylPy_4csyrXdmJpLUZlRnRwTU0/view?usp=sharing)

下面就是整个程序的源码，主要包括1个模块module1.bas，1个主程序窗口MainForm.frm，1个设置窗口setform.frm

主程序窗口MainForm.frm的代码如下，程序的主要功能集中在此。

```
'计算空闲时间
Private Declare Function SetWindowPos Lib "user32" (ByVal hWnd As Long, ByVal hWndInsertAfter As Long, ByVal X As Long, ByVal Y As Long, ByVal cx As Long, ByVal cy As Long, ByVal wFlags As Long) As Long
Private Declare Function EnableWindow Lib "user32" (ByVal hWnd As Integer, ByVal aBOOL As Integer) As Integer
Private Declare Function IsWindowEnabled Lib "user32" (ByVal hWnd As Integer) As Integer
Private Declare Function GetMenu Lib "user32" (ByVal hWnd As Integer) As Integer
Private Declare Function FindWindow Lib "user32" Alias "FindWindowA" (ByVal lpClassName As String, ByVal lpWindowName As String) As Long
Private Declare Function SystemParametersInfo Lib "user32" Alias "SystemParametersInfoA" (ByVal uAction As Long, ByVal uParam As Long, ByVal lpvParam As Any, ByVal fuWinIni As Long) As Long

'常量声明
Const SWP_NOMOVE = &H2    '保持当前位置（x和y设定将被忽略）
Const SWP_NOSIZE = &H1   '保持当前大小（cx和cy会被忽略）
Const HWND_TOPMOST = -1
Const HWND_NOTOPMOST = -2
Const flags = SWP_NOMOVE Or SWP_NOSIZE

'使用GetLastInputInfo来检测键盘、鼠标无动作
Private Declare Function GetLastInputInfo Lib "user32" (plii As LASTINPUTINFO) As Boolean
Private Declare Function GetTickCount Lib "kernel32" () As Long
Private Type LASTINPUTINFO
    cbSize As Long
    dwTime As Long
End Type

Private Sub Form_Load()
    If App.PrevInstance = True Then
        '用APP对象的PrevInstance属性，防止同时运行屏幕保护程序的两个实例
        Unload Me
        Exit Sub
    End If
    
    Timer1.Interval = 1000
    '读取配置信息
    Call GetConfig
    '打开配置文件,防止手工修改
    FileName = App.Path + "\CONFIG"
    Open FileName For Binary As #99
End Sub

Private Sub BntOk_Click()
    If (Text1.Text = password) Then
         ' 卸载钩子
        UnhookWindowsHookEx lHook
    
        Timer1.Enabled = True
        Me.Visible = False
        Text1.Text = ""
        Timer2.Enabled = False
    Else
        Label2.Visible = True
        Label2.Caption = "输入密码不正确，请重新输入！"
        Text1.Text = ""
        Text1.SetFocus
    End If
End Sub

Private Sub BntEmpty_Click()
    Text1.Text = ""
End Sub

'显示主程序界面
Private Sub ShowForm()
    ' 安装钩子
    lHook = SetWindowsHookEx(WH_KEYBOARD_LL, AddressOf CallKeyHookProc, App.hInstance, 0)
    
    '如果更改的背景文件不存在，或者文件目录为空，则显示默认背景
    If (filedir <> "" And Dir(filedir) <> "") Then
        '开始的时候使用的是改变窗口的默认背景，这样的话这个背景不会被拉伸，只能保持默认大小，舍弃 Me.Picture = LoadPicture(filedir)
        '现在使用image控件来实现
        Image1.Width = Screen.Width
        Image1.Height = Screen.Height
        
        '这里把窗口设为全屏，因为image 要随着窗口变化
        Top = 0
        Left = 0
        Me.Width = Screen.Width
        Me.Height = Screen.Height
        
        Me.Image1.Visible = False
        Me.Image1.Picture = LoadPicture(filedir)
        Me.AutoRedraw = True
        Me.PaintPicture Image1.Picture, 0, 0, Me.ScaleWidth, Me.ScaleHeight
    End If
    
    Me.Show 'setFocus前面须有这个
    '设置窗口在最上面
    Dim Ok
    Ok = SetWindowPos(Me.hWnd, HWND_TOPMOST, 0, 0, 0, 0, flags)
    '设置全屏
    Top = 0
    Left = 0
    Me.Width = Screen.Width
    Me.Height = Screen.Height
    '设置输入框的位置
    Frame1.Top = Screen.Height - Frame1.Height
    Frame1.Left = Screen.Width - Frame1.Width
    Label2.Left = Frame1.Left
    Label2.Top = Frame1.Top - Label2.Height
    Label2.Width = Frame1.Width
    Label2.Visible = False
    Text1.SetFocus
    '禁用alt+ctrl+delete
    'Open Environ$("WinDir") & "\system32\taskmgr.exe" For Binary As #1
    Timer1.Enabled = False
    Timer2.Enabled = True
    Text1.SetFocus
End Sub
'设置窗口
Private Sub BntSet_Click()
    If (Text1.Text = password) Then
        ' 卸载钩子
        UnhookWindowsHookEx lHook
        Me.Visible = False
        Text1.Text = ""
        setform.Show
        Timer1.Enabled = True
    Else
        Label2.Visible = True
        Label2.Caption = "输入密码不正确，请重新输入！"
        Text1.Text = ""
        Text1.SetFocus
    End If
End Sub

'回车之后的动作
Private Sub Text1_KeyPress(KeyAscii As Integer)
    ' Text1 响应回车键
    If KeyAscii = 13 Then
        If (Text1.Text = password) Then
            ' 卸载钩子
            UnhookWindowsHookEx lHook
            Me.Visible = False
            Text1.Text = ""
            Timer1.Enabled = True
            Timer2.Enabled = False
        Else
            Label2.Visible = True
            Label2.Caption = "输入密码不正确，请重新输入！"
            Text1.Text = ""
            Text1.SetFocus
        End If
    End If
End Sub
'当空闲时间大于IntervalTime时，调用ShowForm
Private Sub Timer1_Timer()
    Dim lii As LASTINPUTINFO
    lii.cbSize = Len(lii)
    If GetLastInputInfo(lii) Then
        If (GetTickCount - lii.dwTime)/60000 > IntervalTime Then
            Call ShowForm
        End If
    End If
End Sub
'禁用任务管理器
Private Sub Timer2_Timer()
   Shell ("cmd /c taskkill /f /im taskmgr.exe"), vbHide
End Sub
```

设置窗口setform.frm的代码，包括密码设置、背景图片设置、开机自启动设置和空闲启动时间设置。

```
Dim change As Boolean
Private Sub Command1_Click()

    '先读出密码
    passwordstr = password
    FileName = App.Path + "\CONFIG" '配置文件路径
    '验证密码
    If Text1.Text = passwordstr And Text3.Text = Text2.Text Then
        NewPassword = Encode(Text2.Text)
        change = SetConfig(NewPassword, 0)
        '设置以后重新读取配置文件
        Call GetConfig
        If (change = True) Then MsgBox "口令修改成功"
    Else
    If Text2.Text <> Text3.Text Then
        MsgBox "两次口令输入不一致，请重新输入"
    Else
        MsgBox "旧口令错，请重新输入"
    End If
    End If
End Sub

Private Sub Command2_Click()
    Unload Me
End Sub

Private Sub Command3_Click()
    Set w = CreateObject("wscript.shell")
    w.regwrite "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\" & App.EXEName, App.Path & "\" & App.EXEName & ".exe"
    MsgBox "已经设置为开机自启动"
End Sub

Private Sub Command4_Click()
    Set w = CreateObject("wscript.shell")
    w.regdelete "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\" & App.EXEName
    MsgBox "已经取消开机自启动"
End Sub

Private Sub Command5_Click()
    
    CommonDialog1.Filter = "jpg|*.jpg"
    CommonDialog1.ShowOpen
    filedir = CommonDialog1.FileName
    If (filedir <> "") Then change = True
    
    change = SetConfig(filedir, 2)
    '设置以后重新读取配置文件
     Call GetConfig
    If (change = True) Then MsgBox "背景替换成功"
End Sub

Private Sub Command6_Click()
    change = SetConfig("", 2)
    '设置以后重新读取配置文件
    Call GetConfig
    If (change = True) Then MsgBox "已恢复为默认背景"
End Sub

Private Sub Command7_Click()
    Unload Me
End Sub

Private Sub IntervalBnt_Click()
    change = SetConfig(setform.IntervalTxt.Text, 1)
    '设置以后重新读取配置文件
    Call GetConfig
    If (change = True) Then MsgBox "修改成功"
End Sub
```

模块module1.bas代码，主要是禁用键盘和加密函数。

```
Option Explicit

Public Declare Sub CopyMemory Lib "kernel32" Alias "RtlMoveMemory" (Destination As Any, Source As Any, ByVal Length As Long)
Public Declare Function GetKeyState Lib "user32" (ByVal nVirtKey As Long) As Integer
Public Declare Function SetWindowsHookEx Lib "user32" Alias "SetWindowsHookExA" (ByVal idHook As Long, ByVal lpfn As Long, ByVal hmod As Long, ByVal dwThreadId As Long) As Long
Public Declare Function CallNextHookEx Lib "user32" (ByVal hHook As Long, ByVal ncode As Long, ByVal wParam As Long, lParam As Any) As Long
Public Declare Function UnhookWindowsHookEx Lib "user32" (ByVal hHook As Long) As Long
Public Const HC_ACTION = 0
Public Const WM_KEYDOWN = &H100
Public Const WM_KEYUP = &H101
Public Const WM_SYSKEYDOWN = &H104
Public Const WM_SYSKEYUP = &H105
Public Const VK_TAB = &H9
Public Const VK_CONTROL = &H11
Public Const VK_ESCAPE = &H1B
Public Const VK_DELETE = &H2E
Public Const WH_KEYBOARD_LL = 13
Public Const LLKHF_ALTDOWN = &H20

'禁用键盘的功能键
Public Type KBDLLHOOKSTRUCT
    vkCode As Long
    scanCode As Long
    flags As Long
    time As Long
    dwExtraInfo As Long
End Type
Public lHook As Long
Dim p As KBDLLHOOKSTRUCT
Dim key()     As Byte
'全局变量
Public password As String
Public IntervalTime As Integer
Public filedir As String
Public FileName As String

'键盘钩子
Public Function CallKeyHookProc(ByVal ncode As Long, ByVal wParam As Long, ByVal lParam As Long) As Long
    Dim fEatKeystroke As Boolean
    
    If (ncode = HC_ACTION) Then
        If wParam = WM_KEYDOWN Or wParam = WM_SYSKEYDOWN Or wParam = WM_KEYUP Or wParam = WM_SYSKEYUP Then
            CopyMemory p, ByVal lParam, Len(p)
            fEatKeystroke = _
            ((p.vkCode = VK_TAB) And ((p.flags And LLKHF_ALTDOWN) <> 0)) Or _
            ((p.vkCode = VK_ESCAPE) And ((p.flags And LLKHF_ALTDOWN) <> 0)) Or _
            ((p.flags And LLKHF_ALTDOWN) <> 0) Or _
            ((p.vkCode = VK_ESCAPE) And ((GetKeyState(VK_CONTROL) And &H8000) <> 0)) Or _
            ((p.vkCode = 91) Or (p.vkCode = VK_ESCAPE) Or (p.vkCode = 92) Or (p.vkCode = 93))
            '判断是否按下了：TAB+ALT、Esc+ALT、Alt(Alt+F4)、Esc+Ctrl、左右 Win 和徽标键\Esc
        End If
    End If
    
    If fEatKeystroke Then
        ' 设置为 1 可以屏蔽按键
        CallKeyHookProc = 1
    Else
        CallKeyHookProc = CallNextHookEx(0, ncode, wParam, ByVal lParam)
    End If
End Function

Sub initkey()       '这里为密匙，建议定义的复杂些，我这里仅仅是个示例
          ReDim key(9)
          key(0) = 12
          key(1) = 43
          key(2) = 53
          key(3) = 67
          key(4) = 78
          key(5) = 82
          key(6) = 91
          key(7) = 245
          key(8) = 218
          key(9) = 190
  End Sub
    
 Function Encode(ByVal s As String) As String                 '加密
          On Error GoTo myerr
          initkey
          Dim buff()     As Byte
          buff = StrConv(s, vbFromUnicode)
          Dim i     As Long, j       As Long
          Dim k     As Long
          k = UBound(key) + 1
          For i = 0 To UBound(buff)
                  j = i Mod k
                  buff(i) = buff(i) Xor key(j)
          Next
          Dim mstr     As String
          mstr = "abcdefghijklmnopqrstuvwxyz0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
          Dim outstr     As String
          Dim temps     As String
          For i = 0 To UBound(buff)
                  k = buff(i) \ Len(mstr)
                  j = buff(i) Mod Len(mstr)
                  temps = Mid(mstr, j + 1, 1) + Mid(mstr, k + 1, 1)
                  outstr = outstr + temps
          Next
          Encode = outstr
          Exit Function
myerr:
          Encode = ""
  End Function
 Function Decode(ByVal s As String) As String                 '解密
          On Error GoTo myerr
          initkey
          Dim i     As Long, j       As Long
          Dim k     As Long, n       As Long
          Dim mstr     As String
          mstr = "abcdefghijklmnopqrstuvwxyz0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
          Dim outstr     As String
          Dim temps     As String
          If Len(s) Mod 2 = 1 Then
                  Decode = ""
                  Exit Function
          End If
          Dim t1     As String
          Dim t2     As String
          Dim buff()     As Byte
          Dim m     As Long
          m = 0
          For i = 1 To Len(s) Step 2
                  t1 = Mid(s, i, 1)
                  t2 = Mid(s, i + 1, 1)
                  j = InStr(1, mstr, t1)
                  k = InStr(1, mstr, t2)
                  n = j - 1 + (k - 1) * Len(mstr)
                  ReDim Preserve buff(m)
                  buff(m) = n
                  m = m + 1
          Next
          k = UBound(key) + 1
          For i = 0 To UBound(buff)
                  j = i Mod k
                  buff(i) = buff(i) Xor key(j)
          Next
          Decode = StrConv(buff, vbUnicode)
          Exit Function
myerr:
          Decode = ""
End Function

'配置信息
'定义变量，password密码，IntervalTime空闲时间

Function GetConfig()
    Dim s As String, t() As String, a As String
    FileName = App.Path + "\CONFIG"
    '如果文件不存在，则创建文件
    If Dir(FileName) = "" Then
       Open FileName For Output As #1 '打开顺序文件，我们可以使用Open语句
       a = Encode("123") + vbCrLf + "10" + vbCrLf 'vbCrLf为回车
       Print #1, a '写数据
       Close #1 '关闭文件
       '隐藏文件
       'SetAttr FileName, vbSystem Or vbHidden
    End If
    Open FileName For Binary As #11
    s = Input(LOF(11), #11)
    Close #11
    t = Split(s, vbCrLf)
    password = Decode(t(0))
    IntervalTime = t(1) '第三行是2，第四行是3，类推
    filedir = t(2)
End Function

Function SetConfig(ByVal Value As String, ByVal Weizhi As Integer) As Boolean
    Close #99 '关闭打开的配置文件
    FileName = App.Path + "\CONFIG"
    Dim s As String, t() As String
    Open FileName For Binary As #123
    s = Input(LOF(123), #123)
    Close #123
    t = Split(s, vbCrLf)
    t(Weizhi) = Value  '第三行是2，第四行是3，类推
    s = Join(t, vbCrLf)
    Kill FileName
    Open FileName For Binary As #11
    Put #11, , s
    Close #11
    SetConfig = True
    Open FileName For Binary As #99 '打开配置文件,防止手工修改
End Function
```
