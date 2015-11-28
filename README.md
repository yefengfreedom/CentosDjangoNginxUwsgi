# CentosDjangoNginxUwsgi


yum install libxml*
1,pip install uwsgi
2,在你的机器上写一个test.py

# test.py
def application(env, start_response):
    start_response('200 OK', [('Content-Type','text/html')])
    return "Hello World"

然后执行shell命令：
uwsgi --http :8001 --wsgi-file test.py
访问网页：
http://127.0.0.1:8001/
看在网页上是否有Hello World

编写django_wsgi.py文件，将其放在与文件manage.py同一个目录下。
注意： 编写文件时需要注意语句os.environ.setdefault。比如，如果你的项目为mysite，则你的语句应该是 os.environ.setdefault("DJANGO_SETTINGS_MODULE", "mysite.settings")
#!/usr/bin/env python 
# coding: utf-8 

import os
import sys

reload(sys)
sys.setdefaultencoding('utf8')
sys.path.append('/usr/lib/python2.7/site-packages/django')

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "mysite.settings")

from django.core.wsgi import get_wsgi_application

application = get_wsgi_application()


3,

我们假设你的Django项目的地址是/home/work/src/sites/testdjango1/testdjango/mysite，

然后，就可以执行以下命令：


uwsgi --http :8000 --chdir /home/work/src/sites/testdjango1/testdjango/mysite --module django_wsgi

test ok:    uwsgi --http :8000 --chdir /usr/opt/test/hellp/ --wsgi-file /usr/opt/test/hellp/django_wsgi.py


4,

djangochina_socket.xml，将它放在 /home/work/src/sites/testdjango1/testdjango/mysite 目录下：


<uwsgi>
    <socket>:8077</socket>
    <chdir>/home/work/src/sites/testdjango1/testdjango/mysite</chdir>
    <module>django_wsgi</module>
    <processes>4</processes> <!-- 进程数 -->
    <daemonize>uwsgi.log</daemonize>
</uwsgi>



在上面的配置中，我们使用 uwsgi.log 来记录日志，开启4个进程来处理请求。

这样，我们就配置好uWSGI了。





