# testgit
#使用www.xssed.com网站的数据集黑样本作为正样例，有4万多条；
#另外提供约20万条正常的http get请求记录作为负样例，为了保证数据安全，去除了url中的host、path等信息，仅保留了payload的部分。
#分步骤将数据集进行“解码(输出可读代码文本)”--->“范化(将数字、url链接精简化)”--->“分词”三个过程。实现代码及输出结果都在文件中。
#分词后的结果如下所示：
#正样例：
#topic=http://gmwgroup.harvard.edu/techniques/index.php?topic=<script>alert(document.cookie)</script>
#siteID=';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
#js='"--></style></script><script>alert(/meehinfected/)</script></title><marquee><h1>XSS:)</h1><marquee><strong><blink>XSSTEST</blink></strong></marquee><h1  >XSS :) </h1></marquee>

#负样例：
#_=1498584888937/&list=FU1804,FU0,FU1707,FU1708,FU1709,FU1710,FU1711,FU1712
#hid=sgpy-windows-generic-device-id&v=8.4.0.1062&brand=1&platform=6&ifbak=0&ifmobile=0&ifauto=1&type=1&filename=sgim_privilege.zip
#iid=11491672248&device_id=34942737887&ac=wifi&channel=huawei&aid=13&app_name=news_article&version_code=621&version_name=6.2.1&device_platform=android&ssmix=a&device_type=FDR-A03L&device_brand=HUAWEI&language=zh&os_api=22&os_version=5.1.1&uuid=860947033207318&openudid=fc19d05187ebeb0&manifest_version_code=621&resolution=1200*1848&dpi=240&update_version_code=6214&_rticket=1498580286466

#分词后的正样例：
#['topic=', 'http://u', '<script>', 'alert(','document.cookie', ')', '</script>']
#['siteid=', 'alert(', 'string.fromcharcode(', '0','0', '0', ')', ')', 'alert(', 'string.fromcharcode(', '0', '0', '0', ')', ')','alert(', 'string.fromcharcode(', '0', '0', '0', ')', ')', 'alert(','string.fromcharcode(', '0', '0', '0', ')', ')', '>', '</script>','>', '>', '<script>', 'alert(', 'string.fromcharcode(', '0', '0','0', ')', ')', '</script>']
#['js=', '>', '</style>', '</script>','<script>', 'alert(', 'meeh', 'infected', ')', '</script>','</title>', '<marquee>', '<h0>', 'xss', ')', '</h0>','<marquee>', '<strong>', '<blink>', 'xss', 'test','</blink>', '</strong>', '</marquee>', '<h0', '>','xss', ')', '</h0>', '</marquee>']

#分词后的负样例：
#['_=', '0', 'list=', 'fu0', 'fu0', 'fu0', 'fu0','fu0', 'fu0', 'fu0', 'fu0']
#['hid=', 'sgpy', 'windows', 'generic', 'device', 'id','v=', '0.0.0.0', 'brand=', '0', 'platform=', '0', 'ifbak=', '0', 'ifmobile=','0', 'ifauto=', '0', 'type=', '0', 'filename=', 'sgim_privilege.zip']
#['iid=', '0', 'device_id=', '0', 'ac=', 'wifi','channel=', 'huawei', 'aid=', '0', 'app_name=', 'news_article','version_code=', '0', 'version_name=', '0.0.0', 'device_platform=', 'android','ssmix=', 'a', 'device_type=', 'fdr', 'a0l', 'device_brand=', 'huawei','language=', 'zh', 'os_api=', '0', 'os_version=', '0.0.0', 'uuid=', '0','openudid=', 'fc0d0ebeb0', 'manifest_version_code=', '0', 'resolution=', '0','0', 'dpi=', '0', 'update_version_code=', '0', '_rticket=', '0']


参考资料：https://www.freebuf.com/news/142069.html
