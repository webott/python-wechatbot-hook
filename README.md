# python-wechatbot-hook
python 聊天机器人，python写聊天机器人，python聊天机器人库，python聊天机器人代码，python智能聊天机器人，python自动聊天机器人，python制作聊天机器人，python训练聊天机器人，python微信聊天机器人，基于python的语音聊天机器人，python聊天机器人的功能
7. 4. 3 钩子实例Windows钩子的应用比较广。无论是安全产品还是恶意软件，到Windows提供的钩子功能。1.全局键盘钩子下面来写一个可以截获键盘消息的钩子程序，其功能非常简单，字符显示出来。既然要截获键盘消息，那么肯定是截获系统范围内的键盘消息，因此需要安装全局钩子，这样就需要DLL文件的支持。先来新建一个DLL文件，在该DLL文件中需要定义两个导出函数和两个全局变量，定义如下：extern "c"_declspec (dllexport) VOID SetHookon():extern"c"_declspec (dllexport) VOID SetHookoff():甚至是常规软件，都会用就是把按下的键对应的
／／ 钩子句柄HHOOK g_Hook-NULL:／／ DLL 模块句柄HINSTANCE g_Inst-NULL:在DIIMain0函数中，需要保存该DLL模块的句柄，以方便安装全局钩子。代码如下：BOOL APIENTRY DIIMain ( HANDLE hModule,DWORD ul_reason_for_call,LPVOID 1pReserved）
／／ 保存DLL的模块句柄g_Inst- (HINSTANCE) hModule:
return TRUE:
1
安装与卸载钩子的函数如下：VOID SetHookon ()1／／ 安装钩子g_Hook-SetWindowsHookEx (WH_KEYBOARD, KeyboardProc,g_Inst, 0) ;
VOID SetHookoff ()（／／ 卸载钩子UnhookWindowsHookEx (g_Hook) ;
对于Windows钩子来说，上面的这些步骤基本上都是必需的，于钩子函数的实现。这里是为了获取键盘按下的键，钩子函数如下：／7 钩子函数LRESULT CALLBACK KeyboardProcl或者是差别不大，关键在int code.WPARAM wParam,LPARAM 1Param
／／ 钩子编码11 虚拟键编码／／ 按建信息
if (code<0)
return CallNextHookEx (g_Hook,code,wParam, 1Param) ;1（codeHC_ACTION && 1Param> 0)if
1
char szBuf [MAXBYTE] - (0} ;GetKeyNameText (1Param,szBuf, MAXBYTE) :MessageBox (NULL,szBuf, NULL, MB_OK) ;
return CallNextHookEx (g_Hook,code,wParam, 1Param) :
关于钩子函数，if (code <0)这里简单地解释一下，首先是进入钩子函数的第一个判断。
return CallNextHookEx (g_Hook,code,wParam, 1Param) ;
如果code的值小于0,则必须调用CallNextHookEx(,将消息继续传递下去，不对该消息进行处理，并返回CallNextHookEx(函数的返回值。这一点是MSDN上要求这么做的。if (code=-HC_ACTION && 1Param> 0)
char szBuf [MAXBYTE] - (0) ;GetKeyNameText (1Param,szBuf, MAXBYTE) ;MessageBox (NULL,szBuf, NULL, MB_OK) ;
如果 code 等于HC_ACTION,表示消息中包含按键消息；如果为WM_KEYDOWN,则显示按键对应的文本。
区
Meoa
Mesoff
将该DLL 文件编译连接。为了测试该DLL文件，新建一个MFC的Dialog工程，添加两个按钮，如图7-35所示。
![image](https://user-images.githubusercontent.com/73727649/197325944-82e43898-620a-4196-88c4-3c3ab93fc29e.png)
HookTestDlg.obj:error LNK2001: unresolved external symbol_SetHookoftDebug/HookTest.exe:fatal error LNK1120: 2 unresolved externalsError executing link.exe.
HookTest.exe-3 error (s) , 0 warning (s)从给出的提示可以看出是连接错误，找不到外部的符号。将DLL编译连接后生成的DL文件和LIB文件都复制到测试工程的目录下，并将LIB文件添加到工程中。在代码中添加如下语句：
pragma comment (Iib,KeyBoradHookTest)再次连接，成功！运行测试程序，并单击“HookOn”按钮，随便按下键盘上的任意一个键，会出现提示对话框，如图7-36所示。
从图7-36中可以看出，当按下键盘上的按键时，程序将捕获到按键。到此，键盘钩子的例子程序就完成了。2.低级键盘钩子数据防泄露软件通常会禁止PrintScreen键，防止通过截屏将数据保存为图片而导致泄密。这类软件想要实现是比较简单的，但是想要将功能做得强大些，还是需要下功夫的。数据防泄露的软件除了要有兼容性好的底层驱动的设计，还要有完善的规则设置。此外就是需要软件安全人员对其进行各种各样的攻击，避免数据防泄露软件因为各种各样的原因而被心怀恶意者突破。这里介绍如何禁止 PrintScreen键。其实很简单，只要安装低级键盘钩子（WH_KEYBOARD_LL)就可以搞定。普通的键盘钩子（WH_KEYBOARD)是无法过滤一些系统按键的。在低级键盘钩子的回调函数中，判断是否为PrintScrecn键，如果是，则直接返回TRUE(首面提到，如果想屏蔽某个消息的话，那么在钩子函数中对该消息进行处理后，直接返回一个非零值），如果不是，则传递给钩子链的下一处。代码如下：extern "c"_declspec (dllexport) BOOL SetHookon数定截获到的键盘输入
个人微信
目前已经实现了很多有趣的功能，运行稳定，比如：发各种消息，
接收各种消息，群管，下载文件，加好友，检测僵尸粉，朋友圈等等功能，
可提供接口，方便各种语言二次开发，欢迎技术交流，Q：2645542961
，请勿用于商业用途。
![image](https://user-images.githubusercontent.com/73727649/197325965-890fb10b-1fb5-497c-9c4c-5c86b52edc82.png)

企业微信：
目前已经实现了大部分功能，运行稳定，比如：发各种消息，
接收各种消息，外部群内部群管理，下载文件，加好友等等功能，
可提供接口，方便各种语言二次开发，欢迎技术交流。
