流程：

1，进入页面
检查浏览器本地检查是否具有用户ID，
如果没有，设置昵称，发送给后端，后端返回用户ID并写入 localstorage 中

2，判断链接是否存在房间ID，如：127.0.0.1:8080?room_id=123&&room_name=xxxx

有：询问是否进入该房间
无：弹窗是否创建房间，进入流程3

3，创建房间
自动生成房间ID，
用户设置房间昵称，
发送到后端，（接口1，创建房间）
点击按钮复制一段文件：来你画我猜吗？我在[链接]等你，
点击链接进入该房间

4，进入房间

[退出房间]按钮，点击返回2，去除 url 参数

前端查询房间状态（接口2，查询房间状态）

房间状态：
a，准备
分为候补区，座位区，座位区第一个位置的玩家才能开始游戏，满两个人才能开始游戏，满8个人自动开始游戏

前端发送房间ID和所有玩家ID（接口3，更新房间信息）

b，游戏进行中
前端请求房间信息（接口4，请求房间数据）
- 用户ID-题目-画布hashID的索引表
- 当前画布的数据
- 全部的聊天记录
- 所有玩家的ID
- 所有玩家的当前分数

Socket
以前端为例：
发送 用户ID，表示该用户回合开始
发送 画布hashID + 画布内容
发送 用户ID + 聊天内容
接受 用户ID + 加分
接受 新的聊天记录以及标签（正确/错误/无关）
接受 用户ID + 画布信息

c，结束
前端请求房间信息（接口5，请求房间信息）
- 用户ID-画布信息-最终得分 的索引

## 积分规则：

如果每次有人答对，答题者得1分；
答题者按 递减序列 记分