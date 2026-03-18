## 数据流转
---
1. 底层逻辑：**客户端 --> 打包请求 --> 互联网送达 -->  服务器拆包处理 --> 打包响应 --> 回给客户端**。
2. 整个过程就像寄快递：写地址、写信（请求）、贴邮票（headers）、放内容（body）；快递公司（HTTP）送到；对方签收、处理、回寄（响应）。
## HTTP 协议
---
1. HTTP 就是“寄信规则”
	1. **GET = “问路”**：你只问，不带东西，地址写在信封（URL）上，大家都可以看到。问10次都一样（幂等）。
	2. **POST = “寄包裹”**：你带行李（body）给对方，箱子里可以放很多东西，也可以让对方“改库存”。寄10次结果可能都不一样。
2. 核心区别：
	1. GET ： 无 Body、参数在 URL 后面、适合“查”，可缓存、安全。
	2. POST ： 有 Body、适合“增/改”，不能缓存。
3. 补充：HTTP 还有 PUT（全量更新）、DELETE（删除）、PATCH（局部更新）。
4. **Demo（立刻复制到 Postman）**：
	1. 新建 Request
	2. **GET Demo**（查数据）： Method: GET URL: https://jsonplaceholder.typicode.com/posts/1 点击 Send 返回 JSON（数据就这样“跑回来了”）。
	3. **POST Demo**（提交数据）： Method: POST URL: 同上 Body → raw → JSON，粘贴：
    ```JSON
	    {
      "title": "仕杰的第一篇帖子",
      "body": "API 真好玩",
      "userId": 1
	    }
    ```
    点击 Send → 返回新创建的 JSON（id 是服务器自动给的）。
	如果返回 400 → 检查 JSON 少了个逗号；500 → 服务器临时抽风。
## RESTful API
---
1. 概念：RESTful 不是新语言，而是一种“聪明点菜方式”--把一切东西的当成“资源”（像菜单上的菜），用 URL 代表资源，用 HTTP 方法决定你要干嘛。
2. 经典规则：
	- GET /posts --> 拿所有帖子
	- GET /posts/1 --> 拿第一个帖子
	- POST /posts --> 新建帖子
	- PUT /posts/1 --> 全量更新第一个
	- DELETE /posts/1 --> 删除
	- 优点：URL 一看就知道是什么，方法一看就知道要干什么，全球都统一
3. **补充知识**： 现在很多公司还在用 REST，但 GraphQL 正在取代它（一次请求就能拿多给资源，，像“点一桌菜”）。
4. **Demo**：
	-  用同一个免费测试 API（它就是标准的 RESTful）：

	- GET https://jsonplaceholder.typicode.com/users → 拿所有用户（资源列表）
	- GET https://jsonplaceholder.typicode.com/users/1 → 拿用户1（单个资源）
	- POST https://jsonplaceholder.typicode.com/users + Body（同上面 JSON）→ 创建新用户。
	看 URL 和 Method 就知道在操作什么资源，这就是 RESTful 的灵魂。
## JSON 数据格式的结构
---
1. 概念：JSON就是“**用大括号写的超级表格**”，电脑最爱吃。
2. **规则**：
	- {} = 对象（一个对象）
	- [] = 数组（一堆东西）
	- "key":value 键值对（key 必须用双引号）
3. 典型结构：
```JSON
	1.{
  "name": "仕杰",
  "age": 25,
  "isStudent": false,
  "hobbies": ["编程", "旅行"],
  "address": {
    "city": "Los Angeles",
    "zip": "90001"
  }
}
```
4. **补充知识**：以前用 XML （一大堆标签），现在 JSON 胜出是因为快、轻、人类可读。注意：中文必须 UTF-8，否则乱码。
5. **Demo**：用上面任意一个 GET 请求，返回的就是 JSON。 在 Postman 右边面板你会看到一堆 {} []，鼠标点开就能看到每一层的 key。 试着自己写个错的 JSON（多一个逗号）再 POST，看报 400，就懂了。
## Postman
---
1. HTTP接口：
	1. 方法 + 地址URL（必填）
	2. 数据：
		1. 查询字符串（出现在URL中）- Params
		2. 鉴权：证明身份（选填）- Auth
		3. 头：请求头（修饰正文，选填）- headers
		4. 正文：请求正文（请求的核心数据，选填）- body
			- 数据的类型：
				- 表单参数
				- 文件上传
				- JSON
				- XML
				- JSON-RPC
	3. 测试脚本（断言）：
		1. 请求前执行的脚本
		2. 请求后执行的脚本（接口关联理、测试用例、断言）
	4. **HTTP版本**：1、2、3（版本不同测试方法不同）
2. Postman 特点
	1. 界面好看
	2. 满足HTTP接口测试的基本请求
	3. 支持代码
	4. 商业软件
	5. 扩展性比较差
## 接口测试实战
---
1. 接口文档：
	1. 请求
	2. 响应：
		- 200：成功
		-  400：请求有问题
		- 401：没有身份凭据
		- 403：权限问题
		- 422：参数不符合要求
## 自动化测试脚本
---
1. 使用Python的方式：
	1. 基础编程
	2. 自带电池
	3. 第三方库：requests
		1. requests响应格式：Response对象
			1. 状态码：Status_code
			2. 响应头：headers
			3. 正文：text
			4. JSON：json()
2. 自动化测试框架
	1. 用途：专业、复杂的大规模测试环境，推荐Pytest