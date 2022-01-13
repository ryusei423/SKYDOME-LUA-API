# SKYDOME-LUA-API
```
SKYDOME.PW LUA-API
```

我们的LUA系统基于lua5.3编写，已开放的扩展库:string,math,table。

lua系统暂时基于vanilla Lua框架，更换性能更高的框架已经在我们的计划中。请向我们报告您遇到的任何lua性能问题，更新的优先级取决于遇到性能问题的概率。

------

API主要分为两个部分 

**功能**：我们提供的API函数。

**成员函数**：各种类型的成员函数。



测试初期，如果遇到bug可以在反馈板块向我们报告！谢谢谢谢谢谢谢谢。

如果您对api有任何建议也都可以在论坛向我们报告哦。



​	1.功能

```
callback:
	回调事件:
		paint
		输入参数:无
		在游戏绘图函数被执行时被回调，我们可以在这时进行绘制。
		
		createmove
		输入参数:CUserCmd指针
		在游戏创建命令时被回调，我们可以在此时修改数据包。
		此回调将在我们完成操作之后，进行bsendPacket设置和快进处理前进行。
		
		GameEvent
		输入参数:游戏事件对象。
		在游戏事件被触发时被回调，我们可以监听游戏事件。
		
		OnShot
		输入参数:射击详细信息对象。
		在ragebot进行射击时被回调，输入参数包含一些关于本次射击的信息。
		
		OnShotEnd
		输入参数:射击结果对象。
		在射击的结果被处理时回调，包含射击是否命中等信息。
		//WARNING//未实装//WARNING//
		
		
		关于类型的方法请看成员函数API。
		
	
	regcallback(string event,function)
	注册一个回调。
	参数:参数1为回调事件的名称，参数2为被调用的函数。
	示例:callback.regcallback("paint",on_paint);

client:
    print(string text)
    在游戏控制台进行打印。
    参数:参数为打印内容。
    示例:client.print("Hello world!");

	IsInGame()
	如果在对局中则返回true，否则返回false。
	参数:无。
	示例:client.IsInGame();
	
	IsConnected()
	如果已经连接到服务器则返回true，否则返回false。
	参数:无。
	示例:client.IsConnected();
	
	GetMaxClients()
	返回最大玩家数量。
	参数:无。
	示例:client.GetMaxClients();
	
	ExecuteClientCmd(string cmd)
	执行客户端命令。
    参数:参数为命令字符串
    示例:client.ExecuteClientCmd("quit");
    
global:
	GetbsendPacket()
	返回一个bool值,只能读取。
	
	SetbsendPacket(bool bsendPacket)
	设置是否发送数据包,应由createmove进行回调。



render:
	信息:
	由于我们使用Surface作为渲染管理器(Surface good,FUCK DX)，您需要把字体安装到系统上才能进行加载。
	
	绘制函数只能从paint回调！
	
    GetScreenSize()
    返回一个Vector对象，为屏幕高宽。
    参数:无
    示例:local screenw = render.GetScreensize().X;
    
    DrawLine(int x1,int y1,int x2,int y2,int r,int g,int b,int a)
    在你的屏幕上画一条线。
    参数:x1,y1为起始点，x2,y2为终点，rgba为颜色。
    示例:render.DrawLine(0,0,1920,1080,255,255,255,255);
    
    DrawFilledRect(int x1,int y1,int x2,int y2,int r,int g,int b,int a)
    画一个填充(实心)的矩形。
    参数:x1,y1为左上角,x2,y2位右下角，rgba为颜色。
    示例:render.DrawFilledRect(0,0,1920,1080,255,255,255,255);
    
    GetTextSize(DWORD font,string text)
    计算字体大小。
    参数:font为字体，text为内容。
    示例:render.GetTextSize(render.DefaultFont,"Hello skydome!");
    
    DrawText(int x,int y,int r,int g,int b,int a,DWORD font,string text)
    在你的屏幕上绘制文字。
    参数:x,y为绘制坐标,r,g,b,a为绘制颜色,font为字体,text为绘制内容。
    示例:render.DrawText(300,300,255,255,255,255,render.DefaultFont,"Hello world!");
    
    
    WorldToScreen(Vector world)
    把世界坐标转为屏幕坐标。返回值为屏幕坐标。
    参数:world为世界坐标。
    示例:无。
    
    
    
cvar:
	信息:详情请看cvar
	
	FindCvar(string cvarname)
	根据名称查找cvar。
	参数:cvar名称。
	示例:local sv_cheat = cvar.FindCvar("sv_cheat");
    
    
EntityList:
	信息:我们使用CBasePlayer作为所有实体的类型。

	CBasePlayer* GetEntity(int id)
	CBasePlayer* GetLocal()
	bool CheckEntity(CBasePlayer* entity,bool checknull,bool checkalive)
	
	Vector GetVectorNetvar(C_BasePlayer entity, string classname,string varname)
	int GetIntNetvar(C_BasePlayer entity, string classname,string varname)
	float GetFloatNetvar(C_BasePlayer entity, string classname,string varname)
	bool GetBoolNetvar(CBasePlayer entity, string classname,string varname)
	
	SetVectorNetver(C_BasePlayer entity,Vector value, string classname,string varname)
	SetIntNetvar(C_BasePlayer entity, int value,string classname,string varname)
	SetFloatNetvar(C_BasePlayer entity,float value, string classname,string varname)
	SetBoolNetvar(CBasePlayer entity, bool value,string classname,string varname)
	
	
	
    
 
utilities:

	SetEspFont(string WindowsFontname)	//WARNING//未实装//WARNING//
    SetBackground(string path)			//WARNING//未实装//WARNING//
    
    
ui:
	信息:目前您只能在lua选项卡中创建ui，对于其他选项卡的支持暂时不在计划中。
	
	
	
    
    
```





​	2.成员函数

```
Vector:
	float x
	float y
	float z
	
	float Length()
	float LengthSqr()
	float Length2D()
	bool IsValid()
	void SetZero()
	float DistTo()
	float DistToSqr()
	Vector Cross()
	void Normalized()
	
Qangle:
	float pitch
	float yaw
	float roll
	
	float Length()
	float LengthSqr()
	void Normalized()

Convar:
	bool GetBool()
	int GetInt()
	float GetFloat()
	void SetBool(bool)
	void SetInt(int)
	void SetFloat(float)
	void SetString(string)

CUserCmd:
	int command_number
	int tick_count
	Qangle viewangles
	Vector aimdirection
	float forwardmove
	float sidemove
	float upmove
	int buttons
	char impulse
	int weaponselect
	int weaponsubtype
	int random_seed
	short mousedx
	short mousedy
	bool hasbeenpredicted
	
	
CBasePlayer
	bool IsAlive()
	说明:如果玩家活着则返回true。
	
	bool IsPlayer()
	说明:如果实体是一个玩家则返回true。

	int GetIndex()
	说明:返回实体索引。

	int GetClassId()
	说明:返回实体类型。
	
	Vector GetHitboxPos(int hitboxid)
	说明:返回hitbox位置，需要传入hitboxid。
	
	信息:
	只用常用数据由api直接提供，其他请使用netvar。
	我们设立了独立的函数来处理netvar，如果需要访问netvar请查看EntityList中的函数。
	
	
```







回不了家的旅行者...应该称之为流浪者.

Copyright © 2021 SKYDOME.PW-天穹之下

```
德丽莎等了一天，天都没有放晴，即使雨停了，天还是灰蒙蒙的。
她无奈地和芽衣一起做好了饭。迎接着没有夕阳的黄昏。

……
家啊。

甲板上还有些许雨水，少女面向灰色的天，裙子被风轻轻吹动。巨大的云彩仿佛触手可及。
愿每个想家的人都能找到回家的路吧。
十二岁的少女，站在巨大战舰的甲板上。
默默地祈祷着。
```
