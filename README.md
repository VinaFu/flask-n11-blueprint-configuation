# flask-n11-blueprint-configuation
如题，讲了两个内容：blueprint和密码

1. 建立main，posts，users三个文件夹。在每个文件夹下建立
  
                <main>    home + about
                __init__
                routes.py

                <posts>    和post相关的东西
                 __init__
                routes.py
                forms.py

                <users>    和users相关的
                 __init__
                routes.py
                forms.py
                utils
                
              都是根据各自的功能来进行分类的，有什么就加什么。最后删除forms.py + routes.py
              同时，在url——for要进行修改，归在哪个项下，就用main.home 来引导方向。
              import也要修改。用find来修改。
              
              蓝本的好处是可以有条理的归类内容，不容易搞混，检查起来方便。
              
              
2. configuration 配置

    为什么要用配置呢？—— 来自知乎：https://zhuanlan.zhihu.com/p/24055329 
    在Flask项目中，我们会用到很多配置（Config）。比如说设置秘钥，设置数据库地址，像下面这样：
    app.config['SECRET_KEY'] = 'some strange words'

    Flask的配置对象（config）是一个字典的子类（subclass），所以你可以把配置用键值对的方式存储进去。
    这是一个通用的处理接口，Flask内置的配置，扩展提供的配置，你自己的配置，都集中在一处。

    为什么需要使用自己的配置？
    假设你在做一个博客，有十个视图函数都定义了每页显示的文章数。当你写好以后，发现每页的文章太多，
    想把这个值改小一点，这时你要找到这十个视图函数，分别修改这个值，很蠢吧？使用配置你就使用一行控制所有的变量：
    app.config['POST_PER_PAGE'] = 12
    直接写出配置的值，像上面那样。
    对于不适合写在程序里的配置，比如密码等，需要把配置写入系统环境变量，然后使用os模块的getenv()方法获取，
    第二个参数作为默认值：
    set MAIL_USERNAME=me@greyli.com  # windows
    export MAIL_USERNAME=me@greyli.com  # *unix

# 这一块还是没有完全搞懂，视频28:00左右，用了sublime来存配置路径。可是我不知道怎么把sublime里面的东西加进文件里。


    2.1 修改地方- init.py
    from flaskblog.config import Config
    
    def create_app(config_class=Config): 把之前定义的app放到这里，以后可以用current——app代替，速度会快一些？
    app = Flask(__name__)
    app.config.from_object(Config)

    db.init_app(app)
    bcrypt.init_app(app)
    login_manager.init_app(app)
    mail.init_app(app)

    from flaskblog.users.routes import users
    from flaskblog.posts.routes import posts
    from flaskblog.main.routes import main
    app.register_blueprint(users)
    app.register_blueprint(posts)
    app.register_blueprint(main)

    return app
    
    2.2 在utils.py + models.py + run.py 里面都修改成current——app。
