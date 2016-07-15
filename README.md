# HTML5 Based File Uploader
# Dropup

## 使用方法

##### 引入Dropup文件

CommonJS 方式引用
```js
var Dropup = require('dropup');
```

AMD 方式引用
```js
define(['dropup'], function(Dropup) {
    // ...
});
```

全局方式，在HTML页面中引入:
```html
<script src="dropup.min.js"></script>
```


### HTML代码
__提示:__</br>
1、上传多个文件时，file input要添加multiple属性</br>
2、android系统选择文件，file input要添加capture="camera"属性，才能打开相机</br>
3、未添加file控件html代码，且未指定fileInput参数，插件会自动生成一个图片选择控件</br>
__注意:__</br>
1、添加了file控件html代码，必须指定fileInput参数，否则会触发两次 `click` 事件，出现2次文件选择器。</br>
2、若使用了 `FastClick` 插件，__必须__在file控件父元素添加class `needsclick` ，否则container内部分甚至全部区域点击无效。
```html
<div class="container" style="width: 200px; height:200px; border: 1px solid black;">
    <input class="du-fileinput" type="file" accept="image/*" capture="camera" style="display:none;" />
</div>
```
__建议:__</br>
HTML中不添加file控制代码，由插件自动生成


### Javascript代码

```js
new Dropup(container, params);
```

Example：
```js
new Dropup(".container", {
    url: "http://localhost/upload",
    fileInput: '.du-fileinput',
    maxFilesize: 500,
    onUploaded: function(du, file, response) {
        // your code to parse response
        // ...
        return false;// 不处理
        return true;// 会调用onSuccess()
        return "error";// 会调用onError()
    },
    onSuccess: function(du, file, response) {
        console.log(file);
    },
    onError: function(du, file, message) {
        alert(message);
    }
});
```

### 服务器端
数据返回格式没有要求，不过通常我们为了方便前端处理，都返回JSON格式。


## 参数
### 
<table>
<thead>

<tr>
  <th>参数</th>
  <th>类型</th>
  <th>默认值</th>
  <th>说明</th>
</tr>
</thead>
<tbody>
<tr><th colspan="4">构造参数</th></tr>
<tr>
  <td>container</td>
  <td>string or HTMLElement</td>
  <td></td>
  <td>拖拽敏感区域</td>
</tr>
<tr>
  <td>params</td>
  <td>object</td>
  <td>{}</td>
  <td>可选参数</td>
</tr>
<tr>
  <th colspan="4">params参数</th>
</tr>
<tr>
  <td>url</td>
  <td>string</td>
  <td>null</td>
  <td>ajax上传地址</td>
</tr>
<tr>
  <td>method</td>
  <td>string</td>
  <td>POST</td>
  <td>提交方式</td>
</tr>
<tr>
  <td>withCredentials</td>
  <td>boolean</td>
  <td>false</td>
  <td>支持跨域发送cookies</td>
</tr>
<tr>
  <td>requestHeaders</td>
  <td>object</td>
  <td>{}</td>
  <td>请求头部信息</td>
</tr>
<tr>
  <td>formParams</td>
  <td>object</td>
  <td>{}</td>
  <td>参数表，和上传请求同时发送</td>
</tr>
<tr>
  <td>fileDataName</td>
  <td>string</td>
  <td>file</td>
  <td>文件上传域的name</td>
</tr>
<tr>
  <td>allowExts</td>
  <td>string</td>
  <td>null</td>
  <td>允许的文件类型, 格式: 扩展名[,扩展名], 如: <code>jpeg,jpg,png,gif</code>,多个类型使用逗号<code>,</code>隔开</td>
</tr>
<tr>
  <td>allowMimeTypes</td>
  <td>string</td>
  <td>null</td>
  <td>允许的Mime类型, 格式: mime[,mime], 如: <code>image/*</code>,多个类型使用逗号<code>,</code>隔开</td>
</tr>
<tr>
  <td>maxFilesize</td>
  <td>int</td>
  <td>256</td>
  <td>单个文件限制，单位: KB</td>
</tr>
<tr>
  <td>maxFiles</td>
  <td>int</td>
  <td>null</td>
  <td>最大上传数</td>
</tr>
<tr>
  <td>parallelUploads</td>
  <td>int</td>
  <td>2</td>
  <td>并行上传量，在进行多文件同时上传时的并发量</td>
</tr>
<tr>
  <td>auto</td>
  <td>boolean</td>
  <td>true</td>
  <td>自动上传，选择文件后自动执行上次文件动作</td>
</tr>
<tr>
  <td>multi</td>
  <td>boolean</td>
  <td>true</td>
  <td>允许多文件上传，头像修改建议设为false，或者将file input的multiple去掉</td>
</tr>
<tr>
  <td>init</td>
  <td>boolean</td>
  <td>true</td>
  <td>默认初始化</td>
</tr>
<tr>
  <td>fileInput</td>
  <td>string or HTMLElement</td>
  <td>null</td>
  <td>file控件, 若container里存在file控件，则必填。反之可不填，会自动生成一个图片控件</td>
</tr>
<tr>
  <td>clickable</td>
  <td>boolean</td>
  <td>true</td>
  <td>拖拽敏感区域是否可点击</td>
</tr>
<tr>
  <th colspan="4">提示文字(Tips Text)</th>
</tr>
<tr>
  <td>txtFileTooBig</td>
  <td>string</td>
  <td>文件上传限制最大为{{maxFilesize}}.</td>
  <td>文件大小超过限制</td>
</tr>
<tr>
  <td>txtInvalidFileType</td>
  <td>string</td>
  <td>不允许的文件类型</td>
  <td>文件类型不允许</td>
</tr>
<tr>
  <td>txtMaxFilesExceeded</td>
  <td>string</td>
  <td>最多能上传{{maxFiles}}个文件</td>
  <td></td>
</tr>
<tr>
  <td>txtCancelUploadTips</td>
  <td>string</td>
  <td>“您确定要取消上传吗？</td>
  <td></td>
</tr>
<tr>
  <th colspan="4">回调函数（Callback)</th>
</tr>
<tr>
  <td>onDragHover</td>
  <td>function()</td>
  <td></td>
  <td>文件拖放。<br/>【注意】dragover事件一定要清除默认事件，不然会无法触发后面的drop事件</td>
</tr>
<tr>
  <td>onDragOver</td>
  <td>function()</td>
  <td></td>
  <td>拖拽到敏感区域</td>
</tr>
<tr>
  <td>onDragLeave</td>
  <td>function()</td>
  <td></td>
  <td>离开敏感区域</td>
</tr>
<tr>
  <td>onDrop</td>
  <td>function(du, file)</td>
  <td></td>
  <td>文件选择后</td>
</tr>
<tr>
  <td>onBefore</td>
  <td>function(du, file)</td>
  <td></td>
  <td>上传之前</td>
</tr>
<tr>
  <td>onProgress</td>
  <td>function(du, file)</td>
  <td></td>
  <td>上传进度</td>
</tr>
<tr>
  <td>onUploaded</td>
  <td>function(du, file, response)</td>
  <td></td>
  <td>上传完毕。<br/>【注意】不同返回值会回调不同函数:<br/>
    <code>return false;// 不处理</code><br/>
    <code>return true;// 会调用onSuccess()</code><br/>
    <code>return "error";// 会调用onError()</code>
  </td>
</tr>
<tr>
  <td>onSuccess</td>
  <td>function(du, file, response)</td>
  <td></td>
  <td>上传成功</td>
</tr>
<tr>
  <td>onError</td>
  <td>function(du, file, response)</td>
  <td></td>
  <td>上传失败</td>
</tr>
<tr>
  <td>onCancel</td>
  <td>function(du, file)</td>
  <td></td>
  <td>上传取消</td>
</tr>
<tr>
  <td>onDelete</td>
  <td>function(du, file)</td>
  <td></td>
  <td>文件删除</td>
</tr>
<tr>
  <td>onComplete</td>
  <td>function(du)</td>
  <td></td>
  <td>文件全部上传完毕</td>
</tr>
<tr>
  <th colspan="4">file对象数据结构</th>
</tr>
<tr>
  <td>file</td>
  <td>object</td>
  <td></td>
  <td>文件对象数据结构，例如: <code>{id: "kQtmYe2Mi07w0Z-T67cTzMmHixHB3Chx", name: "example.jpg", percent: "100.00", size: 8172, src: "", status: "success", type: "image/jpeg"}</code></td>
</tr>
<tr>
  <th colspan="4">外部方法</th>
</tr>
<tr>
  <td>start</td>
  <td>function()</td>
  <td></td>
  <td>上传开始，如果参数<code>auto</code>为<code>false</code>时，需要手动调用此方法</td>
</tr>
<tr>
  <td>delete</td>
  <td>function(id)</td>
  <td></td>
  <td>删除文件，参数<code>id</code>是<code>file.id</code></td>
</tr>
<tr>
  <td>setOption</td>
  <td>function(option, value)</td>
  <td></td>
  <td>参数设置，支持3种形式：<br/>
    <code>setOption('name', 'value')</code><br/>
    <code>setOption('name', {key: value})</code><br/>
    <code>setOption({key: value, key2: {}})</code>
  </td>
</tr>
</tbody></table>

### 更新日志
### 1.5.2 - 2016/07/15

1. 修复 `delete()` 方法，在 `files` 中找不到等于id的文件，会删除最后一个文件的BUG。
2. 修改 `uploadFile(), setOption(), formatSize(), getSuffix(), guid()` 5个方法。
3. 修改 `init()` 方法，自动生成的文件选择器会依赖 `multi`, `allowMimeTypes` 参数。
4. 替换 `multipart_params` 参数为 `formParams`。
5. 新增 `requestHeaders`, `allowMimeTypes` 2个可选参数。

### 1.5.1 - 2016/05/29
1. 移除兼容旧版FastClick单击无效果的代码。

### 1.5.0 - 2016/05/25
1. 插件不再处理上传结果，直接调用onUploaded()由用户处理。

### 1.4.0 - 2016/04/08
1. 调整大量代码结构。
2. 上传完成后，如果是JSON会自动处理结果，否则直接调用onSuccess()函数由用户处理。
3. 新增onBefore()回调函数，便于上传之前修改参数。
4. 新增setOption()方法。

