# shiro-redis 用例

注：filter不知道怎样注入service


### 管理在线会话说明、并发登陆控制思路

利用redis中保存token情况管理在线用户，删除相应的key则表示下线相应的用户

另外添加字段说明是什么设备，用户名.设备id为redis中保存token的key

删除相应的key则表示下线相应的用户

使用用户名作为键，按照设备登录时间为顺序的列表作为值，表示登录登录情况，当超过限定后，则根据需求选择不登陆，还是将最早登录的下线


### 失败次数过多锁定

每个用户使用一个键记录登录失败次数

当登录失败次数过多后强制下线所有用户，并将用户状态修改为锁定状态

在没有超过限制登录成功，将该键删除，或将数值置为0



**最好使用另外filter，每个filter作为一个检查项**

**如果不知道怎样实现，则可以在jwt上进行功能上的添加，但不建议这样**


