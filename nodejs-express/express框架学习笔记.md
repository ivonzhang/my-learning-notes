# Express框架学习笔记 #
##
> add by zhangivon 2017/03/19
##

- 搭建一个个人博客，参考学习链接[http://www.tuicool.com/articles/jueARjE](http://www.tuicool.com/articles/jueARjE) (转载的)
	
	1. Node.js： 0.10.32

	2. Express： 4.10.2

	3. MongoDB： 2.6.1

##


- 创建一个web应用
	>  通过require()加载了express、path 等模块,以及 routes 文件夹下的index. js和 users.js 路由文件。 下面来讲解每行代码的含义。
	>  
	(1) var app = express()：生成一个express实例 app。  
	(2)app.set('views', path.join(__dirname, 'views’))：设置 views 文件夹为存放视图文件的目录, 即存放模板文件的地方,__dirname 为全局变量,存储当前正在执行的脚本所在的目录。  
	(3)app.set('view engine', 'ejs’)：设置视图模板引擎为 ejs。  
	(4)app.use(favicon(__dirname + '/public/favicon.ico’))：设置/public/favicon.ico为favicon图标。
	(5)app.use(logger('dev’))：加载日志中间件。  
	(6)app.use(bodyParser.json())：加载解析json的中间件。  (7)app.use(bodyParser.urlencoded({ extended: false }))：加载解析urlencoded请求体的中间件。  
	(8)app.use(cookieParser())：加载解析cookie的中间件。  
	(9)app.use(express.static(path.join(__dirname, 'public')))：设置public文件夹为存放静态文件的目录。  
	(10)app.use('/', routes);和app.use('/users', users)：路由控制器。  
##  

- 路由控制  
	> express 封装了多种 http 请求方式，我们主要只使用 get 和  post 两种，即  app.get() 和 app.post() 。  
	> 
	app.get() 和  app.post() 的第一个参数都为请求的路径，第二个参数为处理请求的回调函数，回调函数有两个参数分别是 req 和 res，代表请求信息和响应信息 。
	
	1. req.query ： 处理 get 请求，获取 get 请求参数  
	2. req.params ： 处理 /:xxx 形式的 get 或 post 请求，获取请求参数  
	3. req.body ： 处理 post 请求，获取 post 请求体  
	4. req.param() ： 处理 get 和 post 请求，但查找优先级由高到低为 
	5. req.params→req.body→req.query  
	> **路径规则还支持正则表达式**
	> 举例  
	>  

		req.query  

		// GET /search?q=tobi+ferret  
		req.query.q  
		// => "tobi ferret"  
		
		// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse  
		req.query.order  
		// => "desc"  
		
		req.query.shoe.color  
		// => "blue"  
		
		req.query.shoe.type  
		// => "converse"  
		req.body
		
		// POST user[name]=tobi&user[email]=tobi@learnboost.com  
		req.body.user.name  
		// => "tobi"  
		
		req.body.user.email  
		// => "tobi@learnboost.com"  
		
		// POST { "name": "tobi" }  
		req.body.name  
		// => "tobi"  
		req.params
		
		// GET /user/tj  
		req.params.name  
		// => "tj"  
		
		// GET /file/javascripts/jquery.js  
		req.params[0]  
		// => "javascripts/jquery.js"  
		req.param(name)
		
		// ?name=tobi  
		req.param('name')  
		// => "tobi"  
		
		// POST name=tobi  
		req.param('name')  
		// => "tobi"  
		
		// /user/tobi for /user/:name   
		req.param('name')  
		// => "tobi"  `    

##

- 使用模板引擎(ejs)
	> 前面我们通过以下两行代码设置了模板文件的存储位置和使用的模板引擎：  
	> 
		app.set('views', __dirname + '/views');
		app.set('view engine', 'ejs');  

	> ejs 的标签系统非常简单，它只有以下三种标签：

	1. <% code %>：JavaScript 代码。
	2. <%= code %>：显示替换过 HTML 特殊字符的内容。
	3. <%- code %>：显示原始 HTML 内容。    
	>  

##

- 使用MongoDB数据库  
	
	1. 使用官方提供的 node-mongodb-native 驱动模块  
	2. 把会话信息存储在数据库中，便于持久维护: 借助**express-session** 和 **connect-mongo** 这两个第三方中间件

	> 
##

- API文档  
	1. Request ： 用于处理http请求
	2. Response ： 返回请求的结果
	3. Router ： 路由器
	> 参考链接 [http://www.expressjs.com.cn/4x/api.html](http://www.expressjs.com.cn/4x/api.html)