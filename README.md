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
              import也要修改。
              
              蓝本的好处是可以有条理的归类内容，不容易搞混，检查起来方便。
              
              
