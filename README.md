# qqconnect - ThinkPHP 5 QQ登录
## 安装方法

composer安装:
``` bash
composer require kuange/qqconnect
```

添加公共配置:
``` php
// QQ 互联配置
'qqconnect' => [
    'appid' => '',
    'appkey' => '',
    'callback' => '',
    'scope' => 'get_user_info,add_share,list_album,add_album,upload_pic,add_topic,add_one_blog,add_weibo,check_page_fans,add_t,add_pic_t,del_t,get_repost_list,get_info,get_other_info,get_fanslist,get_idolist,add_idol,del_idol,get_tenpay_addr',
    'errorReport' => true
]
```

控制器编写:

登录
``` php
use kuange\qqconnect\QC;
class OauthController extends Controller
{
    public function qqAction()
    {
        $qc = new QC();
        return redirect($qc->qq_login());
    }
}
```

回调
``` php
use kuange\qqconnect\QC;
class CallbackController extends Controller
{
    public function qqAction()
    {
        $qc = new QC();
        echo $qc->qq_callback();    // access_token
        echo $qc->get_openid();     // openid
        // 待处理用户逻辑
        $this->success('登录成功', url('/'));
    }
}
```
