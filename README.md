ihome合租项目大纲之python版

    项目初始化
    登录注册
    用户信息
    房屋信息
    订单模块

项目初始化
项目分析

    Ihome
        基于移动端的出租寻租的房屋o2o房屋平台项目 。主要目标是位用户提供租房，寻租的一个平台
        基于Flask框架，以前后端分离的形式实现具体功能业务，前后端交互的数据主要使用JSON
            后台接口值否则提供响应数据，前端页面负责展示数据和效果
            项目的各接口设计符合RESTfulAPI风格

    技术实现
        python实现后台接口
        前端页面使用Bootstrap框架实现
        数据库存储使用Redis+MySQL
        第三方扩展
            七牛云：存储房屋图片
            云通信：短信验证码
            captcha:图片验证码

    项目模块
        用户模块
        房屋模块
        订单模块

    具体需求
        1.主页
            最多5个房屋logo图片展示，点击可跳转至房屋详情页面
            提供登录/注册入口，登陆后显示用户名,点击可跳转至个人中心
            用户可以选择城区，入住时间，离开时间等条件进行搜索
            城区的区域信息需要动态加载 
        2.注册
            用户账号默认为手机号
            图片验证码正确后才能发送短信验证码
            短信验证码每60秒可发送一次
            每隔条件出错时又响应错误提示 
        3.登录
            用手机号与密码登陆
            错误时有响应提示 
        4.房屋列表页
            可根据入住时间，区域进行筛选，并可进行排序
            房屋信息分页加载
            区域信息动态加载
            筛选条件更新后，页面立即更新 
        5.房屋详情页
            需展示的详细信息参考设计图
            提供预定入口
            若是房东本人查看房屋信息时，预定入口不显示 
        6.房屋预定
            由用户确定入住时间
            根据用户确定的入住时间实时显示合计天数与总金额 
        7.个人主页
            显示个人头像，手机号，用户名（用户名未设置时为用户手机号）
            提供需改个人信息的入口
            提供做为房客下单的查询入口
            提供成为房东所需实名认证的入口
            提供做为房东发布房屋信息的入口
            提供作为房东查询客户订单的入口
            提供退出的入口 
        8.个人信息修改
            可以修改个人头像
            可以修改用户名
            登陆手机号不能修改
            上传头像与用户名分开保存
            上传新头像后页面立即显示新头像 
        9.我的订单（房客）
            按时间倒序显示订单信息
            订单完成后提供平价功能
            已评价的订单能看到评价信息
            被拒绝的订单能看到拒单信息 
        10.实名认证
            实名认证只能进行一次
            提交信息后再次进入后，只能查看信息,不能修改
            认证信息包含姓名与身份证号 
        11.我的房源
            未实名认证的用户不能发布新房源信息,需 引导到实名认证页面
            按时间倒序显示已经发布的房屋信息
            点击房屋可进入详情页面
            对实名认证的用户提供发布新房屋的功能 
        12.发布新房源
            需要用户填写全部房屋信息
            房屋的文字信息与图片分开操作 
        13.客户订单（房东）
            按时间倒序显示用户下的订单
            对于新订单提供接单与拒单的功能
            拒单必须填写拒单原因
            若客户进行了订单评价，需显示 
        14.退出
            提供退出功能

    项目根目录
        /ihome:项目应用核心目录
        /logs：项目日志目录
        config.py:项目配置文件
        manage.py：项目启动文件
        requrements.txt:项目依赖文件
        areas_facility:房屋设置和区域数据

    项目/ihome 目录
        /api_1_0:项目视图函数–后端接口
        /libs:项目用到的资源库
        /static:项目静态文件夹
        /utils：项目通用工具(自定义状态吗，登录验证装饰器等)
        __init__.py:项目应用初始化文件（应用程序实例，数据库实例，蓝图注册，日志等）
        constants.py:项目常量信息（数据库缓存信息，验证码，房屋信息等）
        models.py:项目模型类
        web_page.py:视图函数（用来处理静态页面的访问）

    项目 /ihome/libs 目录
    -/yuntongxun：第三方扩展（发送短信）

    项目 /ihome/static目录
        /css/：项目css文件
        /html/：项目html文件
        /images/:项目图片文件
        /js/:项目js文件
        /plugins/:项目前端插件（bootstrap, switch,swiper等）
        favicon.ico:项目logo

    项目/ihome/utils目录
        /captcha/图片验证码生成
        commons.py:用设置文件（正则url,登录验证装饰器）
        image_storage.py:云存储设置文件（七牛云）
        respinse_code.py：自定义状态码
        sms.py:发送短信

    使用GIT管理源代码
        使用码云管理
        步骤
            码云上创建项目
            使用pycharm克隆项目
        常用git命令：
            git clone:克隆完整代码
            git pull:拉取某一个分支的代码
            git checkout branch:切换分支
            git add ：将工作区代码保存到暂存区
            git commit:将暂存区代码保存到本地代码库
            git push：将代码推到远端代码仓库 

这里写图片描述

    项目框架搭建
        目标：将特定逻辑代码抽取到指定类中，减小各自之间的耦合性
        结构
            manage:主要管理程序的启动，以及db操作
            ihome/init:管理app的创建，db创建，csrf保护，redis,Session,项目日志
            ihome/api_1_0/init :定义路由
            config:管理配置参数的，比如mysql路径，redis端口等

    日志
        相关概念
            日志是一种可以追踪某些软件运行时所发生事件的方法
            软件开发人员可以向他们的代码中调用日志记录相关的方法来表明发生了某些事情
            一个事件可以用一个可包含可选变量数据的消息来描述
            事件也有重要性的的概念，这个重要性被称为严重性级别
        日志的作用
            通过log的分析，可以方便了解系统，软件，应用的运行情况
            在应用出现故障的时候，快速定位
            程序调试
            用户行为信息分析
        日志的等级
            CRITICAL:重大的，危险的
            ERROR:错误
            WARNING:警告
            INFO:信息
            DEBUG:调试
            NOTSET:没有设置
        logging模块
            python自身提供的用于记录日志的标准库模块

    数据库表分析
        项目中应该有以下几张表
            User:保存用户信息
            House:保存房屋信息
            Order表：保存用户订单信息
            Area表：保存区域信息
            Facility表：保存房屋设施信息
            HouseFacility表：房屋与设施多对多关联表
            HouseImage表：保存房屋信息中的图片数据

    静态文件访问设置
        需要专门处理以下静态文件的访问，采用的方式是专门为静态文件设置访问路径，为静态文件创建一个蓝图

        步骤
            在ihome目录下创建Web_html.py文件，并在该文件下创建蓝图

         # -*- coding:utf-8 -*-

        from flask import Blueprint

        html = Blueprint("html", __name__)
           

            在ihome的init.py文件的create_app方法中注册蓝图

         def create_app(config_name):
        """创建应用实例"""
        ...


        # 注册蓝图，在使用的时候再引入

        from ihome.api_1_0 import api
        app.register_blueprint(api, url_prefix='/api/v1_0')


        # 注册html静态文件的蓝图

        import web_html
        app.register_blueprint(web_html.html)

        return app
            

    静态文件的友好路径访问
        需求：用户访问http://127.0.0.1:5000/直接访问到 http://127.0.0.1:5000/index.html
        用户想要访问其他静态文件直接使用：http://127.0.0.1:5000/<文件名>.html
        代码实现：
            关键代码：current_app.send_static_file(file_name)

    @html.route('/<re(".*"):file_name>')
    def get_html(file_name):
        """提供html静态文件"""
        # 根据用户访问路径中指定的html文件名，找到指定静态文件并返回
        if not file_name:
            # 表示用户访问的是 `/`
            file_name = "index.html"

        # 判断如果不是网站logo
        if file_name != "favicon.ico":
            # 拼接路径
            file_name = "html/" + file_name

        return current_app.send_static_file(file_name)

      

登录注册

    图片验证码
        验证流程
            1.前端传入一个图片id并提交到后台
            2.后台生成图片验证码，并把验证码内容当值，图片id当做key存储到redis中
            3.后台把验证码图片当做响应传给前端
            4.当前端申请发送短信验证码的时候带上图片id和输入的验证码内容
            5.后台取出图片id对应的验证码内容与前端传过来的内容进行比较
            6.如果一样，向指定的手机发送验证码，若不一样，则返回验证码错误 

        后端实现
            1.获取参数
            2.生成验证码
            3.删除之前的验证码并保存当前验证码
            4.错误处理
            5.响应返回

        import logging

        from flask import jsonify, make_response
        from ihome.api_1_0 import api
        from ihome.utils.captcha.captcha import captcha
        from ihome import redis_store, constants
        from ihome.utils.response_code import RET


        # 图形验证码 & 短信验证接口


        # /api/v1_0/image_codes



        # image_codes--> 符合第三四条 : 只需要名词变复数 /  获取单个商品需要/后加id

        @api.route('/image_codes/<image_code_id>')
        def get_image_code(image_code_id):

            # 生成了验证码
            name, text, image_data = captcha.generate_captcha()

            # 保存到redis中 setex: 可以设置数据并设置有效期
            # 需要三个参数: key , expiretime, value

            try:
                redis_store.setex('image_code_' + image_code_id, constants.IMAGE_CODE_REDIS_EXPIRE, text)
            except Exception as e:
                # 需要存储到日志文件中去
                logging.error(e)

                # 需要返回JSON数据, 以键值对返回
                resp = {
                    'errno': RET.DBERR,
                    'errmsg': '保存验证码失败'
                }
                return jsonify(resp)

            # 返回响应数据
            resp = make_response(image_data)
            resp.headers['Content-Type'] = 'image/jpg'

            return resp

           

        前端实现
            1.通过uuid生成验证码编号
            2.拼接验证码地址
            3.设置验证码图片标签src

         // 定义一个成员变量用于记录验证码编号
        var imageCodeId = ""

        // 生成一个图片验证码的编号，并设置页面中图片验证码img标签的src属性
        function generateImageCode() {
            // 1. 生成一个编号
            // 严格一点的使用uuid保证编号唯一， 不是很严谨的情况下，也可以使用时间戳
            imageCodeId = generateUUID();

            // 2. 拼接验证码地址
            var imageCodeUrl = "/api/v1_0/image_codes/" + imageCodeId;

            // 3. 设置页面中图片验证码img标签的src属性
            $(".image-code>img").attr("src", imageCodeUrl)
        }
           

    短信验证码

        核心内容
            1.云通讯SDK自带了一个SendTemplateSMS.py文件，导入SDK并利用里面的示例即可发送短信验证码
            2.修改运通徐的SendTemplateSMS.py 文件，增加单例，以方便调用发短信接口。
            3.在verifycode.py文件中，注册smscode,并实现逻辑代码 

        后端代码实现

    """
    这里使用手机号当做id, 可以通过正则来过滤一些垃圾请求
    GET /api/v1_0/sms_codes/17612345678?image_code=werz&image_code_id=61242
    用户填写的验证码
    用户的手机号
    图像验证码的编码
    """

    @api.route("/sms_codes/<re(r'1[34578]\d{9}'):mobile>")
    def send_sms_code(mobile):

        # 一. 获取参数
        # mobile
        # imaga_code
        # image_code_id
        image_code = request.args.get('image_code')
        image_code_id = request.args.get('image_code_id')

        # 二. 验证参数的完整性及有效性
        if not all([image_code, image_code_id]):
            resp_dict = {
                'errno': RET.PARAMERR,
                'errmsg': '参数不完整'
            }
            return jsonify(resp_dict)

        # 三. 处理业务逻辑

        # 1. try: 从redis中获取真实的图片验证码
        try:
            real_image_code = redis_store.get('image_code_' + image_code_id)
        except Exception as e:
            # 保存错误日志
            logging.error(e)
            # 返回错误信息
            resp_dict = {
                'errno': RET.DBERR,
                'errmsg': '获取图片验证码失败'
            }
            return jsonify(resp_dict)

        # 2. 判断图像验证码是否过期
        # 一般从数据库中获取了一个空值NULL 就是None
        if real_image_code is None:
            # 返回错误信息
            resp_dict = {
                'errno': RET.NODATA,
                'errmsg': '图片验证码过期/失效'
            }
            return jsonify(resp_dict)

        # 3. try:无论验证成功与否, 都执行删除redis中的图形验证码
        try:
            redis_store.delete('image_code_' + image_code_id)
        except Exception as e:
            logging.error(e)
            # 一般来说, 只要是删除数据库出错, 都不应该返回错误信息. 因为这个操作, 不是用户做错了
            # 此时, 只需要记录日志即可


        # 4. 判断用户填写的验证码与真实验证码是否一致, 需要转换小(大)写后在比较
        if real_image_code.lower() != image_code.lower():
            resp_dict = {
                'errno': RET.DATAERR,
                'errmsg': '图片验证码填写有误'
            }
            return jsonify(resp_dict)


        # 5. try:判断用户手机号是否注册过--> 在短信发送之前, 节省资源
        try:
            user = User.query.filter_by(mobile = mobile).first()
        except Exception as e:
            logging.error(e)
            # 理论上应该返回错误信息, 但是注册的时候还需要去验证, 去获取数据库.
            # 因此, 考虑到用户体验, 我们这一次就放过去, 让用户先接受验证码, 知道注册的时候再去判断
        else:
            # 如果查询成功, 再次判断user是否存在
            # 如果数据库没有数据, 返回一个NULL --> None
            if user is not None:
                resp_dict = {
                    'errno': RET.DATAEXIST,
                    'errmsg': '手机号已注册, 直接登录即可'
                }
                return jsonify(resp_dict)


        # 6. 创建/生成6位验证码
        sms_code = '%06d' % random.randint(0, 999999)

        # 7. try:将短信验证码保存redis中
        try:
            # 保存到redis中 setex: 可以设置数据并设置有效期
            # 需要三个参数: key , expiretime, value
            redis_store.setex('sms_code_' + mobile, constants.SMS_CODE_REDIS_EXPIRES, sms_code)
        except Exception as e:
            logging.error(e)
            resp_dict = {
                'errno': RET.DBERR,
                'errmsg': '保存验证码异常'
            }
            return jsonify(resp_dict)


        # 8. try:发送验证码
        try:
            ccp = CCP()
            # 第一个是手机号, 第二个发短信模板需要的参数[验证码, 过期时间], 第三个短信的模板编号
            # result 如果发送短信成功, 就会返回0, 如果失败,就会返回-1
            result = ccp.send_template_sms(mobile, [sms_code, constants.SMS_CODE_REDIS_EXPIRES / 60], 1)
        except Exception as e:
            logging.error(e)
            resp_dict = {
                'errno': RET.THIRDERR,
                'errmsg': '发送短信异常'
            }
            return jsonify(resp_dict)



        # 四. 返回数据
        if result == 0:
            # 0, 表示发送短信成功
            resp_dict = {
                'errno': RET.OK,
                'errmsg': '发送短信成功'
            }
            return jsonify(resp_dict)
        else:
            # -1, 表示发送短信失败
            resp_dict = {
                'errno': RET.THIRDERR,
                'errmsg': '发送短信失败'
            }
            return jsonify(resp_dict)

        

        前端代码实现

         // 使用ajax方式调用后端接口，发送短信
        var req_data = {
            image_code_id: imageCodeId,
            image_code: imageCode
        };
        $.get("/api/v1_0/sms_codes/" + mobile, req_data, function (resp) {
            // 根据返回的返回数据，进行相应的处理
            if (resp.errno == 4004 || resp.errno == 4002) {
                // 图片验证码的错误
                $("#image-code-err span").html(resp.errmsg);
                $("#image-code-err").show();
                //恢复按钮点击
                $(".phonecode-a").attr("onclick", "sendSMSCode();");
            } else if ( resp.errno == 0 ) {
                // 发送短信成功
                var $time = $(".phonecode-a");
                var duration = 60;
                // 设置定时器
                var intervalid = setInterval(function(){
                    $time.html(duration + "秒");
                    if(duration === 1){
                        // 清除定时器
                        clearInterval(intervalid);
                        $time.html('获取验证码');
                        $(".phonecode-a").attr("onclick", "sendSMSCode();");
                    }
                    duration = duration - 1;
                }, 1000, 60);
            } else {
                //理论上应该对各个错误进行针对性处理. 我们这里只是简单的判断了两种错误, 其他错误就直接填出alert提示
                alert(resp.errmsg);
                $(".phonecode-a").attr("onclick", "sendSMSCode();");
            }
        })

        

    注册功能后端代码实现
        在api目录下创建passpot.py文件，用于存放注册/登录/退出功能

     mport logging
    import re
    from flask import request, jsonify, current_app, session
    from ihome import redis_store, db
    from ihome.models import User
    from ihome.utils.response_code import RET
    from . import api


    # POST /avi/v1_0/users/


    # 手机号   mobile


    # 短信验证码 sms_code


    # 密码    password


    @api.route('/users', methods=['POST'])
    def register():

        # 后台返回的是JSON数据, 同时也要求前端返回的是JSON数据
        # key=value&key=value
        # {"key": "value"}

        # 一. 获取参数
        # get request.args.get()
        # form request.form
        # request.get_json()
        # request.form
        # 只要后台发送了JSON数据, 我们就可以通过request.get_json()来获取我们需要的数据

        # 如果前端发送的ContentType不是JSON, 那么request.get_json()就没有办法获取数据

        resp_dict = request.get_json()
        mobile = resp_dict.get('mobile')
        sms_code = resp_dict.get('sms_code')
        password = resp_dict.get('password')

        # 二. 检查数据完整性及有效性
        # 2.1 检查数据完整性
        if not all([mobile, sms_code, password]):
            resp = {
                'errno': RET.PARAMERR,
                'errmsg': '参数不完整'
            }
            return jsonify(resp)

        # 2.2 检查手机号有效性
        # 以前定义的re的正则转换器, 是为了给flask的路由使用的. flask默认的路由规则很简单
        if not re.match(r'1[34578]\d{9}', mobile):
            resp = {
                'errno': RET.DATAERR,
                'errmsg': '手机号格式错误'
            }
            return jsonify(resp)


        # 三. 业务逻辑处理
        # 1. try:从redis中获取短信验证码
        try:
            real_sms_code = redis_store.get('sms_code_' + mobile)
        except Exception as e:
            # 日志模块默认集成到了app中
            # current_app.logger.error(e)
            logging.error(e)
            resp = {
                'errno': RET.DBERR,
                'errmsg': '获取短信验证码失败'
            }
            return jsonify(resp)


        # 2. 判断验证码是否过期
        if real_sms_code is None:
            resp = {
                'errno': RET.NODATA,
                'errmsg': '短信验证码已过期'
            }
            return jsonify(resp)

        # 3. 判断用户是否输出了正确的验证码
        if real_sms_code != sms_code:
            resp = {
                'errno': RET.DATAERR,
                'errmsg': '短信验证码填写错误'
            }
            return jsonify(resp)

        # 4. try:删除短信验证码(如果验证出错重新发送的话, 浪费资源, 浪费用户时间) 跟之前的发送短信验证码3,4步是相反的
        try:
            redis_store.delete('sms_code_' + mobile)
        except Exception as e:
            logging.error(e)
            # 一般来说, 只要是删除数据库出错, 都不应该返回错误信息. 因为这个操作, 不是用户做错了
            # 此时, 只需要记录日志即可

        # 5. 把数据保存到数据库(如果重复注册, 会导致失败)
        # (1. 获取短信验证码的接口, 已经判断过是否注册了 2. 用户模型手机号和用户名已经加入了唯一值, 所以数据不可能重复添加)

        # 创建用户, 保存数据
        user = User(name=mobile, mobile=mobile)
        # 密码的处理, 应该交给模型类去处理.
        user.password = password

        try:
            db.session.add(user)
            db.session.commit()
        except Exception as e:
            # a. 记录日志
            logging.error(e)

            # b. 回滚操作
            db.session.rollback()

            # c. 返回错误数据
            resp = {
                'errno': RET.NODATA,
                'errmsg': '短信验证码已过期'
            }
            return jsonify(resp)

        # 6. 保存将来需要用到的session数据
        # db.session: 处理数据库的
        # Session (大写的, flask_session的) 将session数据从以前默认的cookie, 存放到redis中
        # session: flask自带的session, 这个才是用来设置数据的
        session['user_id'] = user.id
        session['user_name'] = mobile
        session['mobile'] = mobile


        # 四. 返回值, 注册成功返回的页面, 交由前端处理
        resp = {
            'errno': RET.OK,
            'errmsg': '注册成功'
        }
        return  jsonify(resp)
        

    模型中密码的处理
        密码需要做加密处理，相关操作放到模型类中进行

     from werkzeug.security import generate_password_hash, check_password_hash


    # 在User下方增加以下函数


    # 通过property装饰器, 将password函数提升为属性

    @property
    def password(self):
        # 在属性的getter方法中, 禁止访问密码数据
        raise AttributeError('禁止访问用户密码')

    @password.setter
    def password(self, value):
        # 在属性的setter方法中执行加密处理
        # 直接传入value即可, 默认sha256, 并会生成随机的8位盐值
        self.password_hash = generate_password_hash(value)

       

    注册功能前端代码实现

         //定义数据-->JS对象
        var data = {
            mobile: mobile,
            password: passwd2,
            sms_code: phoneCode
        };

        //需要转换成JSON对象
        //X-CSRFToken-->固定的写法. 将来对比的时候, 就会从这个Key中取值
        //getCookie: 自己写的从cookie获取cstf_token的方法
        data_json = JSON.stringify(data);
        $.ajax({
            url: "/api/v1_0/users", //请求路径URL
            type: "post", //请求方式
            data: data_json, //要发送的数据
            contentType: "application/json", //指明给后端发送的是JSON数据
            dataType: "json", //指明后端给前端的是JSON
            headers: {
              "X-CSRFToken": getCookie('csrf_token')
            },
            success: function (resp) {
                if (resp.errno == 0) {
                    //请求成功, 跳转页面
                    location.href = '/login.html'
                } else {
                    //其他错误, 就弹出提示
                    alert(resp.errmsg)
                }
            }
        }); 
       

    登录后端代码实现
        登录实际上是设置session数据，以便服务器和浏览器保持连接状态，因此路由以sessions命名


      POST 用户登录, 其实是在操作session

    # 手机号   mobile


    # 密码    password

    @api.route('/sessions', methods=['POST'])
    def login():

        # 一. 获取参数
        resp_json = request.get_json()
        mobile = resp_json.get('mobile')
        password = resp_json.get('password')

        # 二. 检查完整性及有效性
        if not all([mobile, password]):
            return jsonify(errno = RET.PARAMERR, errmsg = '参数不完整')

        if not re.match(r'1[34578]\d{9}', mobile):
            return jsonify(errno=RET.PARAMERR, errmsg='手机格式错误')

        # 三. 业务逻辑处理
        # 1. try:判断用户的登录错误次数
        # 如果用户在redis中存储的错误次数过多, 不需要在判断了, 直接返回即可
        user_ip = request.remote_addr
        try:
            # 保存错误次数的key, 为access+userIP
            access_counts = redis_store.get('access_' + user_ip)
        except Exception as e:
            logging.error(e)
            return jsonify(errno=RET.DBERR, errmsg='查询数据库失败')

        # 如果有错误记录, 加入已经是6次登录, 而我们设置的最大次数是5. 此时直接返回(登录太频繁, 请稍后再试)即可
        # 判断是否超过了最大的限制次数
        # 错误次数不为空 and 错误次数超过了最大值 --> 直接返回
        if access_counts is not None and int(access_counts) >= 5:
            return jsonify(errno=RET.REQERR, errmsg='请求已超过最大次数')

        # 2. try:查询数据库, 判断用户信息与密码
        try:
            user = User.query.filter_by(mobile=mobile).first()
        except Exception as e:
            logging.error(e)
            return jsonify(errno=RET.DBERR, errmsg='查询用户数据失败')

        # 同时对用户名和密码做判断, 只要有一个错误的, 就告诉用户: 用户名或密码输入错误
        # TODO(huizhubo) 没写密码判断
        if user is None or not user.check_password(password):

            # 累加错误次数, 并设置时间
            try:
                # incr:累加错误次数
                redis_store.incr('access_' + user_ip)
                # expire: 第一个参数 key, 第二个参数 过期时间
                redis_store.expire('access_' + user_ip, 600)
            except Exception as e:
                logging.error(e)

            return jsonify(errno=RET.LOGINERR, errmsg='用户名或密码输入错误')

        # 3. try:如果手机和密码都正确, 说明登录成功, 清除之前保存的错误次数
        try:
            redis_store.delete('access_' + user_ip)
        except Exception as e:
            logging.error(e)

        # 4. 设置session
        session['user_id'] = user.id
        session['mobile'] = user.mobile
        session['user_name'] = user.name

        # 四. 返回值
        return jsonify(errno=RET.OK, errmsg='用户登录成功')
        
        

    注册功能前端代码实现
        在login.js文件的登录方法中，添加以下代码

             //定义数据-->JS对象
            var data = {
                mobile: mobile,
                password: passwd
            };

            //需要转换成JSON对象
            //X-CSRFToken-->固定的写法. 将来对比的时候, 就会从这个Key中取值
            //getCookie: 自己写的从cookie获取cstf_token的方法
            data_json = JSON.stringify(data);
            $.ajax({
                url: "/api/v1_0/sessions", //请求路径URL
                type: "post", //请求方式
                data: data_json, //要发送的数据
                contentType: "application/json", //指明给后端发送的是JSON数据
                dataType: "json", //指明后端给前端的是JSON
                headers: {
                  "X-CSRFToken": getCookie('csrf_token')
                },
                success: function (resp) {
                    if (resp.errno == 0) {
                        //请求成功, 跳转页面
                        location.href = '/'
                    } else {
                        //其他错误, 就弹出提示
                        alert(resp.errmsg)
                    }
                }
            }); 
        
        

    检查登录状态

        后端代码实现
            首页的右上角，未登录会显示注册，登录按钮，如果已经登录了，显示手机号，这时候就需要检查是否登录

         @api.route("/sessions", methods=["GET"])
        def check_login():
        """检查登陆状态"""

        # 尝试从session中获取用户的名字

        name = session.get("user_name")

        # 如果session中数据name名字存在，则表示用户已登录，否则未登录

        if name is not None:
            return jsonify(errno=RET.OK, errmsg="true", data={"name": name})
        else:
            return jsonify(errno=RET.SESSIONERR, errmsg="false")
            

        前端代码实现

         //检查用户的登录状态
        $.get("/api/v1_0/sessions", function(resp) {
        if (resp.errno == 0) {
            // 表示用户是登录
            $(".top-bar>.user-info>.user-name").html(resp.data.name);
            $(".top-bar>.user-info").show();
        } else {
            // 表示用户未登录
            $(".top-bar>.register-login").show();
        }
        }, "json");
            

    退出登录
        后端代码实现

     @api.route("/sessions", methods=["DELETE"])
    @login_required
    def logout():
        """登出"""
        # 清除session数据, csrf_token需要保留.
        csrf_token = session['csrf_token']
        session.clear()
        session['csrf_token'] = csrf_token
        return jsonify(errno=RET.OK, errmsg="OK")
       

        前端代码实现

     function getCookie(name) {
        var r = document.cookie.match("\\b" + name + "=([^;]*)\\b");
        return r ? r[1] : undefined;
    }

    // 点击退出按钮时执行的函数
    function logout() {
        $.ajax({
            url: "/api/v1_0/sessions",
            type: "delete",
            headers: {
                "X-CSRFToken": getCookie("csrf_token")
            },
            dataType: "json",
            success: function (resp) {
                if (resp.errno == 0) {
                    location.href = "/index.html";
                } else {
                    alert(resp.errmsg)
                }
            }
        });
    }
        

    login_required
        很多接口的调用都应该先判断是否登录，所有已在utils/common.py文件中，新增一个公共的函数

     # 目的: 在每一个需要判断是否登录的方法之前, 先调用我们下面的方法, 来判断用户是否登录过

    # view_func --> logout


    def login_required(view_func):
    """检验用户的登录状态"""
    @wraps(view_func)
    def wrapper(*args, **kwargs):
    user_id = session.get("user_id")
    if user_id is not None:

    # 表示用户已经登录


    # 使用g对象保存user_id，在视图函数中可以直接使用


    # 比如后面设置头像的时候, 仍然需要获取session的数据. 为了避免多次访问redis服务器. 可以使用g变量

    g.user_id = user_id
    return view_func(*args, **kwargs)
    else:

    # 用户未登录

    resp = {
    "errno": RET.SESSIONERR,
    "errmsg": "用户未登录"
    }
    return jsonify(resp)
    return wrapper
       
        

用户信息

    七牛云存储
        对于实际项目中的作用
            用于在实际项目中存储媒体（图像，音频，视频）文件
            节省自己服务器的空间，节约宽带，提升媒体文件访问的稳定性
            不需要人力物力对重复数据，冗余数据进行清理及判断

        上传文件到七牛
            在ihome/utils目录下创建images_storge.py文件

              # -*- coding: utf-8 -*-

        from qiniu import Auth, put_file, etag, urlsafe_base64_encode, put_data
        import qiniu.config


        # 需要填写你的 Access Key 和 Secret Key

        access_key = '6HpJXhnT1MS70c7GjT--UrvRn6sMsxwDkIQ1fYQq'
        secret_key = 'rn0V8J7trKklJwTRA8arYoFFCOe6OftoCt_w-s-4'


        def storage(file_data):
            """上传图片到七牛, file_data是文件的二进制数据"""
            # 构建鉴权对象
            q = Auth(access_key, secret_key)

            # 要上传的空间
            bucket_name = 'itheimaihome'

            # 我们不需要这个Key. 七牛会自动生成
            # 上传到七牛后保存的文件名
            # key = 'my-python-logo.png';

            # 生成上传 Token，可以指定过期时间等
            token = q.upload_token(bucket_name, None, 3600)

            # 我们这个是通过form表单提交的, 不需要用到put_file方法
            # 要上传文件的本地路径
            # localfile = './sync/bbb.jpg'
            # ret, info = put_file(token, key, localfile)

            ret, info = put_data(token, None, file_data)

            print 'info: %s' % info
            print 'ret: %s' % ret

            if info.status_code == 200:
                # 表示上传成功， 返回文件名
                # 我们上传成功之后, 需要在别的页面显示图像, 因此需要返回图像名
                return ret.get("key")
            else:
                # 表示上传失败
                raise Exception("上传失败")
                # http://ozcxm6oo6.bkt.clouddn.com/FnTUusE1lgSJoCccE2PtYIt0f7i3


        if __name__ == '__main__':
            # 打开图片数据
            # 需要在同级目录中增加一张1.JPG图片以供测试
            with open("./1.JPG", "rb") as f:
                # 读取图片数据二进制数据
                file_data = f.read()
                # 上传图片书记到七牛云
                result = storage(file_data)
                # result 就存储的是图片名. 将来就可以再程序中调用显示
                print result
            

    上传个人头像信息
        后端代码：
        在/ihome/api_1_0/profile.py文件下添加路由 

        # -*- coding:utf-8 -*-

    import logging
    from . import api
    from ihome.utils.common import login_required
    from flask import request, g, jsonify, current_app, session
    from ihome.utils.response_code import RET
    from ihome.utils.image_storage import storage
    from ihome.models import User
    from ihome import constants, db


    @api.route('/users/avatar', methods=["POST"])
    @login_required
    def set_user_avatar():

        # 图片是以表单提交的

        # 一. 获取数据
        # 1.1 获取用户的ID
        user_id = g.user_id

        # 1.2 获取头像对象
        image_file = request.files.get('avatar')

        # 二. 效验参数
        if image_file is None:
            return jsonify(errno=RET.PARAMERR, errmsg='未上传图像')

        # 三. 业务处理
        # 保存图像 --> 1. 七牛云 2. MySql
        # 3.1 读取图片的二进制数据
        image_data = image_file.read()

        # 3.2 try:保存七牛云
        try:
            # file_name 就存储的是图片名. 将来就可以再程序中调用显示
            file_name = storage(image_data)
        except Exception as e:
            logging.error(e)
            return jsonify(errno=RET.THIRDERR, errmsg='上传图像异常')

        # 3.3 try:保存图像到数据库中
        try:
            # update: 查询之后拼接update, 可以直接进行更新操作
            # update中需要传入字典
            User.query.filter_by(id=user_id).update({"avatar_url": file_name})
            db.session.commit()
        except Exception as e:
            logging.error(e)
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg='数据库保存图像失败')

        # 四. 返回值

        # 此时的文件名, 没有域名. 因此如果直接返回给客户端, 客户端无法直接加载
        # ozcxm6oo6.bkt.clouddn.com
        # 为了避免在数据库存储过多重复的域名前缀, 因此保存的时候, 不加域名. 返回给前端数据时, 我们拼接域名即可

        # 拼接完整的图像URL地址
        avatar_url = constants.QINIU_URL_DOMAIN + file_name

        # 返回的时候, 记得添加图像url信息
        # 如果还需要额外的返回数据, 可以再后方自行拼接数据, 一般会封装成一个字典返回额外数据
        return jsonify(errno=RET.OK, errmsg='保存图像成功', data={"avatar_url": avatar_url})
        

        前端代码实现
        在/ihome/static/js/ihome/profile.js

     $(document).ready(function () {
        // 页面加载好
        $("#form-avatar").submit(function (event) {
            // 阻止表单的默认行为
            event.preventDefault();
            // jquery.form.min.js
            $(this).ajaxSubmit({
                url: "/api/v1_0/users/avatar",
                type: "post",
                dataType: "json",
                headers: {
                    "X-CSRFToken": getCookie("csrf_token")
                },
                success: function (resp) {
                    if (resp.errno == 0) {
                        // 上传头像成功, 设置页面中头像展示的url
                        $("#user-avatar").attr("src", resp.data.avatar_url);
                    } else if (resp.errno == 4101 ){
                        // 表示用户未登录, 跳转到登录页面
                        location.href = "/login.html";
                    } else {
                        alert(resp.errmsg);
                    }
                }
            });
        });
    })
        

    用户名修改
        后端：在/ihome/api_1_0/profile.py中添加路由

        @api.route("/users/name", methods=["PUT"])
    @login_required
    def change_user_name():
        """修改用户名"""
        # 使用了login_required装饰器后，可以从g对象中获取用户user_id
        user_id = g.user_id

        # 获取用户想要设置的用户名
        req_data = request.get_json()
        if not req_data:
            return jsonify(errno=RET.PARAMERR, errmsg="参数不完整")

        name = req_data.get("name")  # 用户想要设置的名字
        if not name:
            return jsonify(errno=RET.PARAMERR, errmsg="名字不能为空")

        # 保存用户昵称name，并同时判断name是否重复（利用数据库的唯一索引)
        try:
            User.query.filter_by(id=user_id).update({"name": name})
            db.session.commit()
        except Exception as e:
            logging.error(e)
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="设置用户错误")

        # 修改session数据中的name字段
        session["user_name"] = name
        return jsonify(errno=RET.OK, errmsg="OK", data={"name": name})
        

        前端：在/ihome/static/js/ihome/profile.js中添加代码

        @api.route("/users/name", methods=["PUT"])
    @login_required
    def change_user_name():
        """修改用户名"""
        # 使用了login_required装饰器后，可以从g对象中获取用户user_id
        user_id = g.user_id

        # 获取用户想要设置的用户名
        req_data = request.get_json()
        if not req_data:
            return jsonify(errno=RET.PARAMERR, errmsg="参数不完整")

        name = req_data.get("name")  # 用户想要设置的名字
        if not name:
            return jsonify(errno=RET.PARAMERR, errmsg="名字不能为空")

        # 保存用户昵称name，并同时判断name是否重复（利用数据库的唯一索引)
        try:
            User.query.filter_by(id=user_id).update({"name": name})
            db.session.commit()
        except Exception as e:
            logging.error(e)
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="设置用户错误")

        # 修改session数据中的name字段
        session["user_name"] = name
        return jsonify(errno=RET.OK, errmsg="OK", data={"name": name})
        

    个人信息获取
        后端：在/ihome/api_1_0/profile.py文件中添加路由

      @api.route("/users", methods=["GET"])
    @login_required
    def get_user_profile():
        """获取个人信息"""
        user_id = g.user_id
        # 查询数据库获取个人信息
        try:
            user = User.query.get(user_id)
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="获取用户信息失败")

        if user is None:
            return jsonify(errno=RET.NODATA, errmsg="无效操作")

        return jsonify(errno=RET.OK, errmsg="OK", data=user.to_dict())
        

        模型增加转字典的方法

      def to_dict(self):
        """将对象转换为字典数据"""
        user_dict = {
            "user_id": self.id,
            "name": self.name,
            "mobile": self.mobile,
            "avatar": constants.QINIU_URL_DOMAIN + self.avatar_url if self.avatar_url else "",
            "create_time": self.create_time.strftime("%Y-%m-%d %H:%M:%S")
        }
        return user_dict
        

        前端：在/ihome/static/js/ihome/my.js 中添加以下代码

      $.get("/api/v1_0/users", function(resp){
        // 用户未登录
        if (resp.errno == 4101) {
            location.href = "/login.html";
        }
        // 查询到了用户的信息
        else if (resp.errno == 0) {
            $("#user-name").html(resp.data.name);
            $("#user-mobile").html(resp.data.mobile);
            if (resp.data.avatar) {
                $("#user-avatar").attr("src", resp.data.avatar);
            }
        }
    }, "json");
       

    用户实名认证
        设置实名认证信息：在/ihome/api_1_0/profile.py文件中添加路由

      @api.route("/users/auth", methods=["POST"])
    @login_required
    def set_user_auth():
        """保存实名认证信息"""
        user_id = g.user_id

        # 获取参数
        req_data = request.get_json()
        if not req_data:
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")

        real_name = req_data.get("real_name")  # 真实姓名
        id_card = req_data.get("id_card")  # 身份证号

        # 参数校验
        if not all([real_name, id_card]):
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")

        # 保存用户的姓名与身份证号
        try:
            User.query.filter_by(id=user_id, real_name=None, id_card=None)\
                .update({"real_name": real_name, "id_card": id_card})
            db.session.commit()
        except Exception as e:
            current_app.logger.error(e)
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="保存用户实名信息失败")

        return jsonify(errno=RET.OK, errmsg="OK")

       

        获取实名认证信息：在/ihome/api_1_0/profile.py 文件中添加路由

      @api.route("/users/auth", methods=["GET"])
    @login_required
    def get_user_auth():
        """获取用户 的实名认证信息"""
        user_id = g.user_id

        # 在数据库中查询信息
        try:
            user = User.query.get(user_id)
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="获取用户实名信息失败")

        if user is None:
            return jsonify(errno=RET.NODATA, errmsg="无效操作")

        return jsonify(errno=RET.OK, errmsg="OK", data=user.auth_to_dict())
        

        模型增加方法实现：在/ihome/models.py

    def auth_to_dict(self):
    """将实名信息转换为字典数据"""
    auth_dict = {
        "user_id": self.id,
        "real_name": self.real_name,
        "id_card": self.id_card
    }
    return auth_dict
        

        前端：在/ihome/static/js/ihome/auth.js 添加代码

      function getCookie(name) {
        var r = document.cookie.match("\\b" + name + "=([^;]*)\\b");
        return r ? r[1] : undefined;
    }

    $(document).ready(function(){
        // 查询用户的实名认证信息
        $.get("/api/v1_0/users/auth", function(resp){
            // 4101代表用户未登录
            if (resp.errno == 4101) {
                location.href = "/login.html";
            }
            else if (resp.errno == 0) {
                // 如果返回的数据中real_name与id_card不为null，表示用户有填写实名信息
                if (resp.data.real_name && resp.data.id_card) {
                    $("#real-name").val(resp.data.real_name);
                    $("#id-card").val(resp.data.id_card);
                    // 给input添加disabled属性，禁止用户修改
                    $("#real-name").prop("disabled", true);
                    $("#id-card").prop("disabled", true);
                    // 隐藏提交保存按钮
                    $("#form-auth>input[type=submit]").hide();
                }
            }
        }, "json");

        // 管理实名信息表单的提交行为
        $("#form-auth").submit(function(e){
            e.preventDefault();
            // 如果用户没有填写完整，展示错误信息
            if ($("#real-name").val()=="" || $("#id-card").val() == "") {
                $(".error-msg").show();
            }

            // 将表单的数据转换为json字符串
            var data = {
                real_name: $("#real-name").val(),
                id_card: $("#id-card").val()
            };
            var jsonData = JSON.stringify(data);

            // 向后端发送请求
            $.ajax({
                url:"/api/v1_0/users/auth",
                type:"post",
                data: jsonData,
                contentType: "application/json",
                dataType: "json",
                headers: {
                    "X-CSRFToken": getCookie("csrf_token")
                },
                success: function (resp) {
                    if (resp.errno == 0) {
                        $(".error-msg").hide();
                        // 显示保存成功的提示信息
                        showSuccessMsg();
                        $("#real-name").prop("disabled", true);
                        $("#id-card").prop("disabled", true);
                        $("#form-auth>input[type=submit]").hide();
                    }
                }
            });
        })
    })
       

        修改我的房源js
            对于发布房源，只有认证后的用户才可以，所以先判断用户的实名认证状态
            在/ihome/static/js/ihome/myhouse.js使用以下代码

              $(document).ready(function(){
            // 对于发布房源，只有认证后的用户才可以，所以先判断用户的实名认证状态
            $.get("/api/v1_0/users/auth", function(resp){
                if (resp.errno == 4101) {
                    // 用户未登录
                    location.href = "/login.html";
                } else if (resp.errno == 0) {
                    // 未认证的用户，在页面中展示 "去认证"的按钮
                    if (!(resp.data.real_name && resp.data.id_card)) {
                        $(".auth-warn").show();
                        return;
                    }
                }
            });
        })
           

房屋信息

    城区信息数据查询
        发布新房源页面中城区信息应该是从后台服务请求
        需要请求城区数据，在/ihome/api_1_0目录下创建house.py文件
        后端代码实现

      mport logging
    from . import api
    from ihome import redis_store
    from ihome.models import Area
    from flask import jsonify, json
    from ihome.utils.response_code import RET
    from ihome import constants

    import sys
    reload(sys)
    sys.setdefaultencoding("utf-8")



    # 这里存放和房屋相关的路由




    # /areas


    # get

    @api.route('/areas/')
    def get_area_info():
        # 一. 逻辑处理

        '''
        1. 读取redis中的缓存数据
        2. 没有缓存, 去查询数据库
        3. 为了将来读取方便, 在存入redis的时候, 将数据转为JSON字典
        4. 将查询的数据, 存储到redis中
        '''
        # 1. 读取redis中的缓存数据
        try:
            areas_json = redis_store.get('area_info')
        except Exception as e:
            logging.error(e)
            # 这里不需要返回错误信息, 因为没有会直接查询数据库
            # 为了避免异常的事情发生, 如果执行失败, 就把数据设置为None
            areas_json = None

        # 2. 没有缓存, 去查询数据库
        if areas_json is None:
            # 查询区域信息
            try:
                areas_list = Area.query.all()
            except Exception as e:
                logging.error(e)
                return jsonify(errno=RET.DBERR, errmsg='数据库异常，请刷新页面重试')

            # 3. 数据转JSON
            # 调用模型的转字典方法, 不断拼接成一个areas
            areas_dict = {'areas': [area.to_dict() for area in areas_list]}
            # 将areas转换成JSON, 方便将来保存redis, 方便返回数据
            areas_json = json.dumps(areas_dict)

            # 4. 保存redis中
            try:
                redis_store.setex('area_info', constants.AREA_INFO_REDIS_EXPIRES, areas_json)
            except Exception as e:
                logging.error(e)
                # 这里如果出错, 可以不用返回错误信息. 因此如果redis没有保存, 那么下一次会直接访问Mysql读取数据, 再次保存

        # 二. 返回数据
        # 前面已经将区域数据转为JSON了. 这里不需要再次调用jsonify来返回, 直接返回字典格式的信息即可
        return '{"errno": 0, "errmsg": "查询城区信息成功", "data": %s}' % areas_json
        

        模型数据处理


    def  to_dictto_dic (self):
        """自定义的方法，将对象转换为字典"""
        area_dict = {
            "aid": self.id,
            "aname": self.name
        }
        return area_dict
       

        请求钩子
            统一设置请求头的Content-Type为JSON

      @api.after_request
    def after_request(response):
        """设置默认的响应报文格式为application/json"""
        # 如果响应报文response的Content-Type是以text开头，则将其改为默认的json类型
        if response.headers.get("Content-Type").startswith("text"):
            response.headers["Content-Type"] = "application/json"
        return response    
        

        前端代码实现：

      // 向后端获取城区的信息
    $.get("/api/v1_0/areas", function (resp) {
        if (resp.errno == 0) {
            // 获取到了城区信息
            var areas = resp.data.areas;
            for (i=0; i < areas.length; i++){
                var area = areas[i];
                $("#area-id").append('<option value="'+ area.aid +'">'+ area.aname +'</option>')
            };
        } else {
            alert(resp.errmsg);
        }
    });
        

    使用JS模板引擎展示城区列表
        Flask:使用jinja2 模板引擎实现python代码和html互通

        前端：使用 art-template,实现js代码和html的互通

        代码实现
            1.在newhouse.html 文件中导入：template.js
            <script src="/static/js/template.js"></script>
            2.在所在城区的选择框标签中，添加以下代码

          <select class="form-control" id="area-id" name="area_id">
        <script id="areas-tmpl" type="text/html">
            {{each areas as area}}
            <option value="{{area.aid}}">{{area.aname}}</option>
            {{/each}}
        </script>                                
        </select>
           

            修改newhouse.js文件中的代码，将获取回来的数据通过template模板传过去

              $(document).ready(function(){
            $.get("/api/v1.0/areas", function (resp) {
                if ("0" == resp.errno) {
                    // 1. 初始化模板
                    rendered_html = template("areas-tmpl", {areas: resp.data});
                    // 2.将模板设置到指定的标签内
                    $("#area-id").html(rendered_html);
                } else {
                    alert(resp.errmsg);
                }
            }, "json");
        });
            

    发布新房源
        后端实现：在/ihome/api_1_0/house.py文件中添加路由

      @api.route("/houses/info", methods=["POST"])
    @login_required
    def save_house_info():
        """保存房屋的基本信息
        前端发送过来的json数据
        {
            "title":"",
            "price":"",
            "area_id":"1",
            "address":"",
            "room_count":"",
            "acreage":"",
            "unit":"",
            "capacity":"",
            "beds":"",
            "deposit":"",
            "min_days":"",
            "max_days":"",
            "area_id":"1",
            "facility":["7","8"]
        }
        """
        # 一. 获取参数
        house_data = request.get_json()
        if house_data is None:
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")

        title = house_data.get("title")  # 房屋名称标题
        price = house_data.get("price")  # 房屋单价
        area_id = house_data.get("area_id")  # 房屋所属城区的编号
        address = house_data.get("address")  # 房屋地址
        room_count = house_data.get("room_count")  # 房屋包含的房间数目
        acreage = house_data.get("acreage")  # 房屋面积
        unit = house_data.get("unit")  # 房屋布局（几室几厅)
        capacity = house_data.get("capacity")  # 房屋容纳人数
        beds = house_data.get("beds")  # 房屋卧床数目
        deposit = house_data.get("deposit")  # 押金
        min_days = house_data.get("min_days")  # 最小入住天数
        max_days = house_data.get("max_days")  # 最大入住天数

        # 二. 校验参数
        if not all([title, price, area_id, address, room_count,acreage, unit, capacity, beds, deposit, min_days, max_days]):
            return jsonify(errno=RET.PARAMERR, errmsg="参数不完整")

        # 判断单价和押金格式是否正确
        # 前端传送过来的金额参数是以元为单位，浮点数，数据库中保存的是以分为单位，整数
        try:
            price = int(float(price) * 100)
            deposit = int(float(deposit) * 100)
        except Exception as e:
            return jsonify(errno=RET.DATAERR, errmsg="参数有误")

        # 三. 保存信息
        # 1. 创建房屋对象
        user_id = g.user_id
        house = House(
            user_id=user_id,
            area_id=area_id,
            title=title,
            price=price,
            address=address,
            room_count=room_count,
            acreage=acreage,
            unit=unit,
            capacity=capacity,
            beds=beds,
            deposit=deposit,
            min_days=min_days,
            max_days=max_days
        )

        # 2. 处理房屋的设施信息
        facility_id_list = house_data.get("facility")
        if facility_id_list:
            # 表示用户勾选了房屋设施
            # 过滤用户传送的不合理的设施id
            # select * from facility where id in (facility_id_list)
            try:
                facility_list = Facility.query.filter(Facility.id.in_(facility_id_list)).all()
            except Exception as e:
                logging.error(e)
                return jsonify(errno=RET.DBERR, errmsg="数据库异常")

            # 为房屋添加设施信息
            if facility_list:
                house.facilities = facility_list

        # 3. 保存数据库
        try:
            db.session.add(house)
            db.session.commit()
        except Exception as e:
            logging.error(e)
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="保存数据失败")

        # 四. 返回
        return jsonify(errno=RET.OK, errmsg="保存成功", data={"house_id": house.id})
       

        前端实现：在/ihome/static/js/ihome/newhouse.js添加以下代码

      $(document).ready(function(){
        ...
        // 处理房屋基本信息的表单数据
        $("#form-house-info").submit(function (e) {
            e.preventDefault();
            // 获取表单数据，转换为json发送到后端
            var houseData = {};
            $("#form-house-info").serializeArray().map(function(x){ houseData[x.name] = x.value});

            var facilities = [];
            $(":checked[name=facility]").each(function(index, x){ facilities[index] = $(x).val()});

            // 这里的房屋设施比较特殊, 所以单独获取. 获取之后,还需要传递给原来的数据中
            // 这里的facility 其实对应的就是房屋信息的facilities属性. 只不过这里只是在拼接数据, 所以可以不一致
            houseData.facility = facilities;

            $.ajax({
                url: "/api/v1_0/houses/info",
                type: "post",
                data: JSON.stringify(houseData),
                contentType: "application/json",
                dataType: "json",
                headers: {
                    "X-CSRFToken": getCookie("csrf_token")
                },
                success: function (resp) {
                    if (resp.errno == 4101) {
                        // 用户未登录
                        location.href = "/login.html";
                    } else if (resp.errno == 0) {
                        // 保存成功
                        // 隐藏基本信息表单
                        $("#form-house-info").hide();
                        // 显示图片表单
                        $("#form-house-image").show();
                        // 设置图片表单中的房屋id
                        $("#house-id").val(resp.data.house_id);
                    } else {
                        alert(resp.errmsg);
                    }
                }
            })

        });
    });
      
       

    上传房源图片
        后端代码实现：在/ihome/api_1_0/house.py文件下添加路由

    @api.route("/houses/image", methods=["POST"])
    @login_required
    def save_house_image():
        """保存房屋的图片"""
        # 获取参数 房屋的图片、房屋编号
        house_id = request.form.get("house_id")
        image_file = request.files.get("house_image")

        # 校验参数
        if not all([house_id, image_file]):
            return jsonify(errno=RET.PARAMERR, errmsg="参数不完整")

        # 1. 判断房屋是否存在
        # 2. 上传房屋图片到七牛中
        # 3. 保存图片信息到数据库中
        # 4. 处理房屋基本信息中的主图片
        # 5. 统一提交数据
        # 1. 判断房屋是否存在
        try:
            house = House.query.get(house_id)
        except Exception as e:
            logging.error(e)
            return jsonify(errno=RET.DBERR, errmsg="数据库异常")

        if house is None:
            return jsonify(errno=RET.NODATA, errmsg="房屋不存在")

        # 2. 上传房屋图片到七牛中
        image_data = image_file.read()
        try:
            file_name = storage(image_data)
        except Exception as e:
            logging.error(e)
            return jsonify(errno=RET.THIRDERR, errmsg="保存房屋图片失败")

        # 3. 保存图片信息到数据库中
        house_image = HouseImage(
            house_id=house_id,
            url=file_name
        )
        db.session.add(house_image)

        # 4. 处理房屋基本信息中的主图片
        if not house.index_image_url:
            house.index_image_url = file_name
            db.session.add(house)

        # 5. 统一提交数据
        try:
            db.session.commit()
        except Exception as e:
            logging.error(e)
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="保存图片信息失败")

        image_url = constants.QINIU_URL_DOMAIN + file_name
        return jsonify(errno=RET.OK, errmsg="保存图片成功", data={"image_url": image_url})
      

        前端代码实现：在/ihome/static/js/newhouse.js中添加代码

      $(document).ready(function(){
        ...
        // 处理图片表单的数据
        $("#form-house-image").submit(function (e) {
            e.preventDefault();
            $("#form-house-image").ajaxSubmit({
                url: "/api/v1_0/houses/image",
                type: "post",
                dataType: "json",
                headers: {
                    "X-CSRFToken": getCookie("csrf_token")
                },
                success: function (resp) {
                    if (resp.errno == 0){
                        // 保存图片成功
                        $(".house-image-cons").append('<img src="'+ resp.data.image_url +'">');
                    } else if (resp.errno == 4101) {
                        location.href = "/login.html";
                    } else {
                        alert(resp.errmsg);
                    }
                }
            })
        });
    });

       
        

    获取房东发布的房源信息
        后端代码实现

      @api.route("/users/houses", methods=["GET"])
    @login_required
    def get_user_houses():
        """获取房东发布的房源信息条目"""
        user_id = g.user_id

        try:
            user = User.query.get(user_id)
            houses = user.houses

            # houses = House.query.filter_by(user_id=user_id)
        except Exception as e:
            logging.error(e)
            return jsonify(errno=RET.DBERR, errmsg="获取数据失败")

        # 将查询到的房屋信息转换为字典存放到列表中
        houses_list = []
        if houses:
            for house in houses:
                houses_list.append(house.to_basic_dict())
        return jsonify(errno=RET.OK, errmsg="OK", data={"houses": houses_list})
        
       

        模型数据处理

       def to_basic_dict(self):
            """将基本信息转换为字典数据"""
            house_dict = {
                "house_id": self.id,
                "title": self.title,
                "price": self.price,
                "area_name": self.area.name,
                "img_url": constants.QINIU_URL_DOMAIN + self.index_image_url if self.index_image_url else "",
                "room_count": self.room_count,
                "order_count": self.order_count,
                "address": self.address,
                "user_avatar": constants.QINIU_URL_DOMAIN + self.user.avatar_url if self.user.avatar_url else "",
                "ctime": self.create_time.strftime("%Y-%m-%d")
            }
            return house_dict
        
      

        前端代码实现

      $(document).ready(function(){
        // 对于发布房源，只有认证后的用户才可以，所以先判断用户的实名认证状态
        $.get("/api/v1_0/users/auth", function(resp){
            if (resp.errno == 4101) {
                // 用户未登录
                location.href = "/login.html";
            } else if (resp.errno == 0) {
                // 未认证的用户，在页面中展示 "去认证"的按钮
                if (!(resp.data.real_name && resp.data.id_card)) {
                    $(".auth-warn").show();
                    return;
                }
                // 已认证的用户，请求其之前发布的房源信息
                $.get("/api/v1_0/users/houses", function(resp){
                    if (resp.errno == 0) {
                        $("#houses-list").html(template("houses-list-tmpl", {houses:resp.data.houses}));
                    } else {
                        $("#houses-list").html(template("houses-list-tmpl", {houses:[]}));
                    }
                });
            }
        });
    })
              

    首页轮播图功能实现
        后端代码实现
            获取成交量最高的前5个订单显示在首页
            数据缓存到redis
            在/ihome/api_1_0/house.py文件中添加路由

      @api.route("/houses/index", methods=["GET"])
    def get_house_index():
        """获取主页幻灯片展示的房屋基本信息"""
        # 从缓存中尝试获取数据
        try:
            ret = redis_store.get("home_page_data")
        except Exception as e:
            logging.error(e)
            ret = None
        if ret:
            logging.info("hit house index info redis")
            # 因为redis中保存的是json字符串，所以直接进行字符串拼接返回
            return '{"errno":0, "errmsg":"OK", "data":%s}' % ret
        else:
            try:
                # 查询数据库，返回房屋订单数目最多的5条数据
                houses = House.query.order_by(House.order_count.desc()).limit(constants.HOME_PAGE_MAX_HOUSES)
            except Exception as e:
                logging.error(e)
                return jsonify(errno=RET.DBERR, errmsg="查询数据失败")

            if not houses:
                return jsonify(errno=RET.NODATA, errmsg="查询无数据")

            houses_list = []
            for house in houses:
                # 如果房屋未设置主图片，则跳过
                if not house.index_image_url:
                    continue
                houses_list.append(house.to_basic_dict())

            # 将数据转换为json，并保存到redis缓存
            json_houses = json.dumps(houses_list)
            try:
                redis_store.setex("home_page_data", constants.HOME_PAGE_DATA_REDIS_EXPIRES, json_houses)
            except Exception as e:
                logging.error(e)

            return '{"errno":0, "errmsg":"OK", "data":%s}' % json_houses
       

        前端代码实现：在/ihome/static/js/ihome/index.js中添加代码

      $(document).ready(function(){
        // 获取幻灯片要展示的房屋基本信息
        $.get("/api/v1_0/houses/index", function(resp){
            if (resp.errno == 0) {
                $(".swiper-wrapper").html(template("swiper-houses-tmpl", {houses:resp.data}));

                // 设置幻灯片对象，开启幻灯片滚动
                var mySwiper = new Swiper ('.swiper-container', {
                    loop: true,
                    autoplay: 2000,
                    autoplayDisableOnInteraction: false,
                    pagination: '.swiper-pagination',
                    paginationClickable: true
                });
            }
        });
    });
        

    首页城区选择
        前端代码：在/ihome/static/js/ihome/index.js添加代码

      $(document).ready(function(){
        // 获取城区信息
        $.get("/api/v1_0/areas", function(resp){
            if (resp.errno == 0) {
                $(".area-list").html(template("area-list-tmpl", {areas:resp.data.areas}));

                $(".area-list a").click(function(e){
                    $("#area-btn").html($(this).html());
                    $(".search-btn").attr("area-id", $(this).attr("area-id"));
                    $(".search-btn").attr("area-name", $(this).html());
                    $("#area-modal").modal("hide");
                });
            }
        });
    });
       

    房屋详情页面
        后端代码实现：在/ihome/api_1_0/house.py 文件中添加路由

    api.route("/houses/<int:house_id>", methods=["GET"])
    def get_house_detail(house_id):
    """获取房屋详情"""

    # 前端在房屋详情页面展示时，如果浏览页面的用户不是该房屋的房东，则展示预定按钮，否则不展示，


    # 所以需要后端返回登录用户的user_id


    # 尝试获取用户登录的信息，若登录，则返回给前端登录用户的user_id，否则返回user_id=-1

    user_id = session.get("user_id", "-1")


    # 校验参数

    if not house_id:
        return jsonify(errno=RET.PARAMERR, errmsg="参数缺失")


    # 先从redis缓存中获取信息

    try:
        ret = redis_store.get("house_info_%s" % house_id)
    except Exception as e:
        logging.error(e)
        ret = None
    if ret:
        logging.info("hit house info redis")
        return '{"errno":"0", "errmsg":"OK", "data":{"user_id":%s, "house":%s}}' % (user_id, ret), 200, {"Content-Type": "application/json"}


    # 查询数据库

    try:
        house = House.query.get(house_id)
    except Exception as e:
        logging.error(e)
        return jsonify(errno=RET.DBERR, errmsg="查询数据失败")

    if not house:
        return jsonify(errno=RET.NODATA, errmsg="房屋不存在")


    # 将房屋对象数据转换为字典

    try:
        house_data = house.to_full_dict()
    except Exception as e:
        logging.error(e)
        return jsonify(errno=RET.DATAERR, errmsg="数据出错")


    # 存入到redis中

    json_house = json.dumps(house_data)
    try:
        redis_store.setex("house_info_%s" % house_id, constants.HOUSE_DETAIL_REDIS_EXPIRE_SECOND, json_house)
    except Exception as e:
        current_app.logger.error(e)

    resp = '{"errno":"0", "errmsg":"OK", "data":{"user_id":%s, "house":%s}}' % (user_id, json_house)
    return resp
       

        模型数据处理


        def to_full_dict(self):
            """将详细信息转换为字典数据"""
            house_dict = {
                "hid": self.id,
                "user_id": self.user_id,
                "user_name": self.user.name,
                "user_avatar": constants.QINIU_URL_DOMAIN + self.user.avatar_url if self.user.avatar_url else "",
                "title": self.title,
                "price": self.price,
                "address": self.address,
                "room_count": self.room_count,
                "acreage": self.acreage,
                "unit": self.unit,
                "capacity": self.capacity,
                "beds": self.beds,
                "deposit": self.deposit,
                "min_days": self.min_days,
                "max_days": self.max_days,
            }

            # 房屋图片
            img_urls = []
            for image in self.images:
                img_urls.append(constants.QINIU_URL_DOMAIN + image.url)
            house_dict["img_urls"] = img_urls

            # 房屋设施
            facilities = []
            for facility in self.facilities:
                facilities.append(facility.id)
            house_dict["facilities"] = facilities

            # 评论信息
            comments = []
            orders = Order.query.filter(Order.house_id == self.id, Order.status == "COMPLETE", Order.comment != None)\
                .order_by(Order.update_time.desc()).limit(constants.HOUSE_DETAIL_COMMENT_DISPLAY_COUNTS)
            for order in orders:
                comment = {
                    "comment": order.comment,  # 评论的内容
                    "user_name": order.user.name if order.user.name != order.user.mobile else "匿名用户",  # 发表评论的用户
                    "ctime": order.update_time.strftime("%Y-%m-%d %H:%M:%S")  # 评价的时间
                }
                comments.append(comment)
            house_dict["comments"] = comments  # [{},{},{}]
            return house_dict
        

        前端代码实现：在/ihome/static/js/detail.js中使用以下代码

      $(document).ready(function(){
        // 获取详情页面要展示的房屋编号
        var queryData = decodeQuery();
        var houseId = queryData["id"];

        // 获取该房屋的详细信息
        $.get("/api/v1_0/houses/" + houseId, function(resp){
            if (resp.errno == 0) {
                $(".swiper-container").html(template("house-image-tmpl", {img_urls:resp.data.house.img_urls, price:resp.data.house.price}));
                $(".detail-con").html(template("house-detail-tmpl", {house:resp.data.house}));

                // resp.user_id为访问页面用户,resp.data.user_id为房东
                if (resp.data.user_id != resp.data.house.user_id) {
                    $(".book-house").attr("href", "/booking.html?hid="+resp.data.house.hid);
                    $(".book-house").show();
                }
                var mySwiper = new Swiper ('.swiper-container', {
                    loop: true,
                    autoplay: 2000,
                    autoplayDisableOnInteraction: false,
                    pagination: '.swiper-pagination',
                    paginationType: 'fraction'
                });
            }
        })
    })

     

    房屋数据搜索
        后端代码实现

    api.route("/houses", methods=["GET"])
    def get_house_list():
    """获取房屋列表信息"""

    # 一. 获取参数

    start_date_str = request.args.get("sd", "")  # 想要查询的起始时间
    end_date_str = request.args.get("ed", "")  # 想要查询的终止时间
    area_id = request.args.get("aid", "")  # 区域id
    sort_key = request.args.get("sk", "new")  # 排序关键字
    page = request.args.get("p", 1)  # 页数


    # 二. 校验参数


    # 2.1判断日期

    try:
        start_date = None
        if start_date_str:
            start_date = datetime.strptime(start_date_str, "%Y-%m-%d")

        end_date = None
        if end_date_str:
            end_date = datetime.strptime(end_date_str, "%Y-%m-%d")

        if start_date and end_date:
            assert start_date <= end_date

    except Exception as e:
        return jsonify(errno=RET.PARAMERR, errmsg="日期参数有误")


    # 2.2判断页数

    try:
        page = int(page)
    except Exception:
        page = 1


    # 三. 业务逻辑处理



    # 3.1 先从redis缓存中获取数据

    try:
        redis_key = "houses_%s_%s_%s_%s" % (start_date_str, end_date_str, area_id, sort_key)
        resp_json = redis_store.hget(redis_key, page)
    except Exception as e:
        logging.error(e)
        resp_json = None

    if resp_json:
        # 表示从缓存中拿到了数据
        return resp_json, 200, {"Content-Type": "application/json"}


    # 3.2 定义查询数据的参数空列表

    filter_params = []


    # 3.3 处理区域信息

    if area_id:
        filter_params.append(House.area_id == area_id)


    # 3.4 处理时间, 获取不冲突的房屋信息

    try:
        conflict_orders_li = []
        if start_date and end_date:
            # 从订单表中查询冲突的订单，进而获取冲突的房屋id
            conflict_orders_li = Order.query.filter(Order.begin_date <= end_date, Order.end_date >= start_date).all()
        elif start_date:
            # 从订单表中查询冲突的订单，进而获取冲突的房屋id
            conflict_orders_li = Order.query.filter(Order.end_date >= start_date).all()
        elif end_date:
            # 从订单表中查询冲突的订单，进而获取冲突的房屋id
            conflict_orders_li = Order.query.filter(Order.begin_date <= end_date).all()
    except Exception as e:
        logging.error(e)
        return jsonify(errno=RET.DBERR, errmsg="数据库异常")

    if conflict_orders_li:
        conflict_house_id_li = [order.house_id for order in conflict_orders_li]
        # 添加条件，查询不冲突的房屋
        filter_params.append(House.id.notin_(conflict_house_id_li))


    # 3.5 排序

    if sort_key == "booking":
        house_query = House.query.filter(*filter_params).order_by(House.order_count.desc())
    elif sort_key == "price-inc":
        house_query = House.query.filter(*filter_params).order_by(House.price.asc())
    elif sort_key == "price-des":
        house_query = House.query.filter(*filter_params).order_by(House.price.desc())
    else:
        house_query = House.query.filter(*filter_params).order_by(House.create_time.desc())


    # 3.6 分页  sqlalchemy的分页

    try:
        #                    页数     每页数量                          错误输出
        house_page = house_query.paginate(page, constants.HOUSE_LIST_PAGE_CAPACITY, False)
    except Exception as e:
        logging.error(e)
        return jsonify(errno=RET.DBERR, errmsg="数据库异常")


    # 3.7 将数据转为JSON

    house_li = house_page.items   # 当前页中的数据结果
    total_page = house_page.pages   # 总页数

    houses = []
    for house in house_li:
        houses.append(house.to_basic_dict())


    # 将结果转换json字符串

    resp = dict(errno=RET.OK, errmsg="查询成功", data={"houses": houses, "total_page": total_page, "current_page":page})
    resp_json = json.dumps(resp)


    # 3.8 将结果缓存到redis中

    if page <= total_page:
        # 用redis的哈希类型保存分页数据
        redis_key = "houses_%s_%s_%s_%s" % (start_date_str, end_date_str, area_id, sort_key)
        try:
            # 使用redis中的事务
            pipeline = redis_store.pipeline()
            # 开启事务
            pipeline.multi()
            pipeline.hset(redis_key, page, resp_json)
            pipeline.expire(redis_key, constants.HOUSE_LIST_PAGE_REDIS_EXPIRES)
            # 执行事务
            pipeline.execute()
        except Exception as e:
            logging.error(e)


    # 四. 数据返回

    return resp_json
        

订单模块

    保存订单
        后端代码实现：在/ihome/api_1_0/下新建order.py，并添加路由

      @api.route("/orders", methods=["POST"])
    @login_required
    def save_order():
        """保存订单"""
        # 一. 获取数据
        # 获取用户id
        user_id = g.user_id
        # 获取参数,校验参数
        order_data = request.get_json()
        if not order_data:
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")
        # 进一步获取详细参数信息,house_id/start_date/end_date
        house_id = order_data.get("house_id")
        start_date_str = order_data.get("start_date")
        end_date_str = order_data.get("end_date")

        # 二. 校验参数完整性
        # 2.1 完整性校验
        if not all([house_id, start_date_str, end_date_str]):
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")

        # 2.2 对日期格式化,datetime
        try:
            start_date = datetime.datetime.strptime(start_date_str, "%Y-%m-%d")
            end_date = datetime.datetime.strptime(end_date_str, "%Y-%m-%d")
            # 断言订单天数至少1天
            assert start_date <= end_date
            # 计算预订的天数
            days = (end_date - start_date).days + 1
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.PARAMERR, errmsg="日期格式错误")

        # 三. 业务逻辑处理
        # 3.1 查询房屋是否存在
        try:
            # House.query.filter_by(id=house_id).first()
            house = House.query.get(house_id)
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="获取房屋信息失败")
        # 校验查询结果
        if not house:
            return jsonify(errno=RET.NODATA, errmsg="房屋不存在")

        # 3.2 判断用户是否为房东
        if user_id == house.user_id:
            return jsonify(errno=RET.ROLEERR, errmsg="不能预订自己的房屋")

        # 3.3 查询是否被别人预定
        try:
            # 查询时间冲突的订单数
            count = Order.query.filter(Order.house_id == house_id, Order.begin_date <= end_date,
                                       Order.end_date >= start_date).count()
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="检查出错，请稍候重试")
        # 校验查询结果
        if count > 0:
            return jsonify(errno=RET.DATAERR, errmsg="房屋已被预订")

        # 3.4 计算房屋总价
        amount = days * house.price
        # 生成模型类对象,保存订单基本信息:房屋/用户/订单的开始日期/订单的结束日期/天数/价格/总价
        order = Order()
        order.house_id = house_id
        order.user_id = user_id
        order.begin_date = start_date
        order.end_date = end_date
        order.days = days
        order.house_price = house.price
        order.amount = amount
        #　3.5 保存订单数据到数据库
        try:
            db.session.add(order)
            db.session.commit()
        except Exception as e:
            current_app.logger.error(e)
            # 提交数据如果发生异常,需要进行回滚操作
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="保存订单失败")

        # 四. 返回数据
        # 前端对应服务器的操作如果是更新资源或新建资源,可以返回对应的信息,
        return jsonify(errno=RET.OK, errmsg="OK", data={"order_id": order.id})
     

    获取用户订单列表
        一个接口实现两个功能
            以房东的身份查询订单：查询属于自己房子的订单
            以房客的身份查询订单：查询自己预定的订单
            使用一个参数区分当前要查询的是什么订单：custom(房客)，landlord(房东)

      api.route("/users/orders", methods=["GET"])
    @login_required
    def get_user_orders():
        """查询用户的订单信息"""
        # 一. 获取数据
        user_id = g.user_id

        # 用户的身份，用户想要查询作为房客预订别人房子的订单，还是想要作为房东查询别人预订自己房子的订单
        role = request.args.get("role", "")

        # 二. 业务逻辑处理
        # 2.1 查询订单数据
        try:
            if "landlord" == role:
                # 以房东的身份查询订单
                # 先查询属于自己的房子有哪些
                houses = House.query.filter(House.user_id == user_id).all()
                houses_ids = [house.id for house in houses]
                # 再查询预订了自己房子的订单,默认按照房屋订单发布时间进行倒叙排序
                orders = Order.query.filter(Order.house_id.in_(houses_ids)).order_by(Order.create_time.desc()).all()
            else:
                # 以房客的身份查询订单， 查询自己预订的订单
                orders = Order.query.filter(Order.user_id == user_id).order_by(Order.create_time.desc()).all()
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="查询订单信息失败")

        # 2.2 将订单对象转换为字典数据
        orders_dict_list = []
        # 校验查询结果
        if orders:
            for order in orders:
                orders_dict_list.append(order.to_dict())

        # 三. 返回数据
        return jsonify(errno=RET.OK, errmsg="OK", data={"orders": orders_dict_list})
     

        模型替换处理

      def to_dict(self):
        """将订单信息转换为字典数据"""
        order_dict = {
            "order_id": self.id,
            "title": self.house.title,
            "img_url": constants.QINIU_URL_DOMAIN + self.house.index_image_url if self.house.index_image_url else "",
            "start_date": self.begin_date.strftime("%Y-%m-%d"),
            "end_date": self.end_date.strftime("%Y-%m-%d"),
            "ctime": self.create_time.strftime("%Y-%m-%d %H:%M:%S"),
            "days": self.days,
            "amount": self.amount,
            "status": self.status,
            "comment": self.comment if self.comment else ""
        }
        return order_dict
     

    接单个拒单
        后端代码实现：在/ihome/api_1_0/order.py文件中添加路由
            接单和拒单同一个接口，不同的action实现
            action:accept（接单），reject(拒单)

       @api.route("/orders/<int:order_id>/status", methods=["PUT"])
    @login_required
    def accept_reject_order(order_id):
        """接单、拒单"""
        # 一. 获取数据
        # 获取用户信息
        user_id = g.user_id
        # 获取参数,校验参数存在
        req_data = request.get_json()
        if not req_data:
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")
        # action参数表明客户端请求的是接单还是拒单的行为
        action = req_data.get("action")

        # 二. 校验完整性
        if action not in ("accept", "reject"):
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")

        # 三. 业务逻辑处理
        # 3.1 获取订单的状态信息
        try:
            # 根据订单号查询订单，并且要求订单处于等待接单状态
            order = Order.query.filter(Order.id == order_id, Order.status == "WAIT_ACCEPT").first()
            # 查询所属房屋
            house = order.house
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="无法获取订单数据")

        # 3.2 确保房东只能修改属于自己房子的订单
        if not order or house.user_id != user_id:
            return jsonify(errno=RET.REQERR, errmsg="操作无效")

        # 3.3 对接单或拒单分别做处理
        # 如果房东选择接单操作
        if action == "accept":
            # 接单，将订单状态设置为等待评论
            order.status = "WAIT_COMMENT"
        # 如果房东选择拒单操作，需要填写拒单原因
        elif action == "reject":
            # 拒单，要求用户传递拒单原因
            reason = req_data.get("reason")
            # 判断房东是否填写拒单原因
            if not reason:
                return jsonify(errno=RET.PARAMERR, errmsg="参数错误")
            # 如果房东选择拒单,把拒单原因存如数据库,
            order.status = "REJECTED"
            # comment字段保存拒单原因
            order.comment = reason

        # 3.4 把接单或拒单操作存储数据库
        try:
            db.session.add(order)
            db.session.commit()
        except Exception as e:
            current_app.logger.error(e)
            # 写入数据如果发生异常,进行回滚
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="操作失败")

        #四. 返回数据
        return jsonify(errno=RET.OK, errmsg="OK")
 

        前端实现
            在加载完订单列表后，给相关按钮添加点击事件
            在点击列表页的接单（拒单）的时候，将订单的id保存到弹出的框【确定】标签的属性中
            点击弹出框的确定键的时候，去获取到【确定】标签的订单号，进行请求

    评论订单功能实现
        后台接口实现：在/ihome/api_1_0/order.py中添加路由

      @api.route("/orders/<int:order_id>/comment", methods=["PUT"])
    @login_required
    def save_order_comment(order_id):
        """保存订单评论信息"""
        # 一. 获取数据
        user_id = g.user_id
        # 获取参数
        req_data = request.get_json()
        # 尝试获取评价内容
        comment = req_data.get("comment")

        # 二. 校验参数
        # 要求用户必须填写评论内容
        if not comment:
            return jsonify(errno=RET.PARAMERR, errmsg="参数错误")

        # 三. 业务逻辑处理
        # 3.1 查询订单状态为待评价
        try:
            # 根据订单id/订单所属用户/订单状态为待评价状态
            order = Order.query.filter(Order.id == order_id, Order.user_id == user_id,
                                       Order.status == "WAIT_COMMENT").first()
            # 查询订单所属房屋
            house = order.house
        except Exception as e:
            current_app.logger.error(e)
            return jsonify(errno=RET.DBERR, errmsg="无法获取订单数据")
        # 校验查询结果
        if not order:
            return jsonify(errno=RET.REQERR, errmsg="操作无效")

        # 3.2 保存评价信息
        try:
            # 将订单的状态设置为已完成
            order.status = "COMPLETE"
            # 保存订单的评价信息
            order.comment = comment
            # 将房屋的完成订单数增加1,如果订单已评价,让房屋成交量加1
            house.order_count += 1
            # add_all可以一次提交多条数据db.session.add_all([order,house])
            db.session.add(order)
            db.session.add(house)
            db.session.commit()
        except Exception as e:
            current_app.logger.error(e)
            # 提交数据,如果发生异常,进行回滚
            db.session.rollback()
            return jsonify(errno=RET.DBERR, errmsg="操作失败")

        # 3.3 缓存中存储的房屋信息,因为订单成交,导致缓存中的数据已经过期,所以,需要删除过期数据
        try:
            redis_store.delete("house_info_%s" % order.house.id)
        except Exception as e:
            current_app.logger.error(e)

        # 四. 返回数据
        return jsonify(errno=RET.OK, errmsg="OK")


项目部署

    1.利用scp命令将整个项目上传到远程服务器
        不需要迁移文件夹，在服务器重新生成即可
        scp -r /home/python/Desktop/iHome root@http://139.196.88.158:/home
    2.在虚拟环境中安装项目所需要的依赖
        pip install -r requirements.txt

    3.在服务器创建数据库

    mysql -uroot -pmysql
    create database ihome charset-utf8;
    use ihome


    4.退出数据库，进行数据可以迁移

    python manage.py init
    python manage.py migarate -m 'init db'
    python manage.py upgrate


    5.进入数据库，添加‘城区’数据和‘房屋设置数据’
    6.退出数据库运行uwsgi服务器
        uwisgi --initconfig.ini
    7.运行nginx服务器
        /etc/init.d/nginx start 
