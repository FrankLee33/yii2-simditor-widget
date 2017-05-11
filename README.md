Yii2 Simditor
===========
### 安装

```
$ php composer.phar require felix33/simditor "*"
```

or add

```
"felix33/simditor": "*"
```

to the ```require``` section of your `composer.json` file.

### 应用

controller:  

```
public function actions()
{
    return [
        'upload' => [
            'class' => 'felix33\simditor\SimditorAction',
        ]
    ];
}
```

view:  

```
echo \felix33\simditor\Simditor::widget(['name' => 'xxxx']);
```

或者：

```
echo $form->field($model,'colum')->widget('felix33\simditor\Simditor',[]);
```

### 配置相关

##### 编辑器相关配置，请在`view` 中配置，参数为`clientOptions`，比如定制菜单，编辑器大小等等，具体参数请查看[simditor官网文档](http://simditor.tower.im/docs/doc-usage.html)。

简单实例:  
```php
use \felix33\simditor\Simditor;
echo Simditor::widget([
    'value'=> '初始化内容..',
    'clientOptions' => [
      'placeHolder' => '这里输入内容...',
      'toolbarFloat' => false,
       // 工具栏
      'toolbar' => [ 'title', '|', 'bold', 'italic',
          'underline', 'strikethrough', 'color',
          'fontScale', 'clearhtml', '|', 'ol', 'ul',
          'blockquote', 'code', 'table', '|', 'link',
          'image', 'hr', '|', 'indent', 'outdent',
          'alignment', 'html', 'fullscreen', 'devices'
       ],
        // 编辑器插入图片时使用的默认图片
       'defaultImage' => '/images/image.png',
       'upload' => [
          // 文件上传的接口地址
          'url' => 'ImgUpload.action',
          // 键值对,指定文件上传接口的额外参数,上传的时候随文件一起提交
          'params' => null,
          // 服务器端获取文件数据的参数名
          'fileKey' => 'fileDataFileName',
          'connectionCount' => 3,
          'leaveConfirm' => '正在上传文件'
        ],
        'devices' => [
          ['text' => '电脑预览', 'css' => 'simditor-devices-pc.css'],
          ['text' => '手机预览', 'css' => 'simditor-devices-mobile.css']
        ]
    ]);
```

##### 文件上传相关配置，请在`controller`中配置

简单实例:  
```php
public function actions()
{
    return [
        'upload' => [
            'class' => 'felix33\simditor\SimditorAction',
            'config' => [
                "imageUrlPrefix"  => "http://www.baidu.com",//图片访问路径前缀
                "imagePathFormat" => "/upload/image/{yyyy}{mm}{dd}/{time}{rand:6}" //上传保存路径
                "imageRoot" => Yii::getAlias("@webroot"),
            ],
        ]
    ];
}
```
