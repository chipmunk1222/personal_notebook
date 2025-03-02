`cloudinary`是一个基于云的媒体管理平台（图床），专门用于图像和视频的上传、存储、管理、优化和分发。
`cloudinary`自带全球`CDN`加速服务，确保资源引用的速度
# 使用cloudinary图床
`cloudinary`图床的使用场景就是简单的图片上传——托管——调用三个环节
具体使用方法如下：
1. 配置环境：`cloudinary`有不同的环境用来隔离不同开发需求（免费版只有一个环境，但一般也能应对大部分的需求）
2. 设置`api key`和`secret`：每个环境都有一个环境名，在环境中创建`api key`和`secret`，共同使用三者来使用`cloudinary`的`api`服务
3. 上传资源：在`app`或命令行中上传资源`assets`，当然，在命令行中上传资源就要使用上面提到的三者，可以创建文件夹进行资源分类
4. 调用图片资源：复制图片连接即可使用`http`直接调用图片资源

## cloudinary图床工作流
总之，`cloudinary`图床的工作方式无非两种：上传图片以及调用图片
- 上传图片：`boardcast`添加或`api`添加，`api`添加需要密钥
- 访问图片：图片的`secure_url`字段就是通过`http`访问图片的字段

# cloudinary api的使用
区别于在图形界面中直接从本地或网络中载入图片，使用`api`时需要一些额外步骤
## 安装依赖
```js
npm install cloudinary
```
## 配置身份验证
身份验证需要传入`cloudinary`的环境参数，具体格式如下`CLOUDINARY_URL=cloudinary://my_key:my_secret@my_cloud_name`

一般在环境变量中注入`CLOUDINARY_CLOUD_NAME`、`CLOUDINARY_API_KEY`与`CLOUDINARY_API_SECRET`
创建`lib/cloudinary.js`通过下列方法配置：
```js
// const cloudinary = require('cloudinary').v2;
import { v2 as cloudinary } from 'cloudinary'

cloudinary.config({ 
	cloud_name: 'my_cloud_name',
	api_key: 'my_key', 
	api_secret: 'my_secret'
});

export default cloudinary
```
## 设置上传信息
使用`cloudinary.uploader.upload()`指定上传路径，第一个参数是图资源本地路径，后面可添加配置项对象，如`{folder:xxx}`指定上传文件夹

例如：
```js
import cloudinary from '../lib/cloudinary.js'

export const updateProfile = async (req, res) => {
  try {
    const {profileImage} = req.body;
    if(!profileImage){
      return res.status(400).json({ message: "Profile image is required" });
    }
    
    const userId = req.user._id;
    const uploadResponse = await cloudinary.uploader.upload(profileImage);
    const updatedUser = await User.findByIdAndUpdate(userId, {profileImage:uploadResponse.secure_url}, {new: true});
    res.status(200).json(updatedUser);
    
  } catch (error) {
    console.log("error in update profile", error);
    res.status(500).json({ message: "Server error" });
  }
}
```
其中返回的`uploadResponse`是一个`json`对象，包含以下属性
```json
{  
    "asset_id": "bf98540caf22ed65775ee0951f4746c9",  
    "public_id": "cld-sample",  
    "format": "jpg",  
    "version": 1719304891,  
    "resource_type": "image",  
    "type": "upload",  
    "created_at": "2024-06-25T08:41:31Z",  
    "bytes": 476846,  
    "width": 1870,  
    "height": 1250,  
    "backup": true,  
    "asset_folder": "",  
    "display_name": "cld-sample",  
    "url": "[http://res.cloudinary.com/cld-docs/image/upload/v1719304891/cld-sample.jpg](http://res.cloudinary.com/cld-docs/image/upload/v1719304891/cld-sample.jpg)",  
    "secure_url": "[https://res.cloudinary.com/cld-docs/image/upload/v1719304891/cld-sample.jpg](https://res.cloudinary.com/cld-docs/image/upload/v1719304891/cld-sample.jpg)",  
    "next_cursor": "497b323dcb9883a15a5e6a7cfb75d439e4de1ca882f5cbe8de6a8b322c37bdad",  
    "derived": [  
        {  
            "transformation": "c_scale,w_500",  
            "format": "jpg",  
            "bytes": 22871,  
            "id": "ce3d7bf3068809656dc5aa76572535da",  
            "url": "[http://res.cloudinary.com/cld-docs/image/upload/c_scale,w_500/v1719304891/cld-sample.jpg](http://res.cloudinary.com/cld-docs/image/upload/c_scale,w_500/v1719304891/cld-sample.jpg)",  
            "secure_url": "[https://res.cloudinary.com/cld-docs/image/upload/c_scale,w_500/v1719304891/cld-sample.jpg](https://res.cloudinary.com/cld-docs/image/upload/c_scale,w_500/v1719304891/cld-sample.jpg)"  
        }  
    ]  
}
```