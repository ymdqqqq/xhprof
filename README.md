# xhprof for PHP7

Please do not use this in an production env.

生产环境勿用。


## Install（for lkk_dev_web）

### Download code
```
$ git clone https://github.com/ymdqqqq/xhprof.git
$ git checkout php7
$ cd xhprof/extension
```
### Compile in Linux
```
$ /home/php-7.0.9/bin/phpize
$ ./configure --with-php-config=/home/php-7.0.9/bin/php-config
$ make && make install
```
### edit php.ini, add a new line:
```
$ vi /home/php-7.0.9/etc/php.ini
/extensions（找到编辑extension的位置）
extension=xhprof.so
```
### make sure it works:
```
$ /home/php-7.0.9/bin/php -m | grep xhprof
显示“xhprof”说明安装成功。
```
### install graphviz
```
$ yum install graphviz
```
### copy code to OOP
```
$ cd ..
$ cp -r xhprof_html /home/{yourname}/lkk/public/pages/
$ cp -r xhprof_lib /home/{yourname}/lkk/public/pages/
```
### reload nginx
```
$ vi /home/tengine/conf/nginx.conf
复制nginx.conf的内容进去。
$ nginx -s reload
```
### test && get profling data
```
在需要测试的地方加以下代码：
xhprof_enable();

{your testing code}

$data = xhprof_disable();
require "/data/{yourname}/lkk/public/pages/xhprof_lib/utils/xhprof_lib.php";
require "/data/{yourname}/lkk/public/pages/xhprof_lib/utils/xhprof_runs.php";

$xhprofRuns = new \XHProfRuns_Default();
$runId = $xhprofRuns->save_run($data, 'test');

echo 'http://dev.lekongkong.site/xhprof_html/index.php?run=' . $runId . '&source=test';
exit;
```
### show profling graph
```
在网页上打开你要测试的页面。
copy网页上出现的url并访问之。
点击“View Full callgraph”即可看到性能图像了。
```
