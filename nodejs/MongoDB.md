`MongoDB` 是一种灵活且强大的 `NoSQL` 数据库，适用于需要处理非结构化或半结构化数据、快速开发和高扩展性的应用。与传统关系型数据库相比，`MongoDB` 提供了更大的灵活性和可扩展性

`MongoDB`的另一大特性是它是一款云数据库，无需安装客户端就能使用，这对于快速开发一些小型应用来说具有非常大的优势
# 在node中使用mongoDB
## 安装mongoose依赖
`mongoose`是用于在`node`项目中连接`mongodb`的工具，使用`npm`安装
```
npm install mongoose
```
## 设置mongoDB数据库
通过在线设置或本地设置`mongoDB`数据库，复制数据库的连接字符串，并通过`dotenv`将其添加到环境中以便后续使用
```js
MONGODB_URI = mongodb+srv://<username>:<password>@cluster0.8gafz.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0
```
## 创建数据库连接
在`lib`文件夹中创建`db.js`文件用作连接文件，导入`mongoose`依赖，使用数据库`URI`连接
```js
import mongoose from "mongoose";

export const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGODB_URI);
    console.log("MongoDB connected:" + conn.connection.host);
  } catch (error) {
    console.log(error);
  }
}
```
在入口文件`index.js`中在服务器开启时调用连接函数
```js
import { connectDB } from "./lib/db.js";

app.listen(PORT, () => {
  console.log("listening on port:", PORT)
  connectDB();
});
```
## 定义Schema视图以及模型
在`models`文件夹中定义数据库的视图模型
>`Schema`相当于一个模型结构，并不携带真实的数据，真实数据由`model`携带，`model`相当于数据库中的数据表，可以执行数据表响应增删改查操作
```js
import mongoose from "mongoose";

const userSchema = new mongoose.Schema(
  {
    email: {
      type: String,
      required: true,
      unique: true,
    },
    fullName: {
      type: String,
      required: true,
    },
    password: {
      type: String,
      required: true,
      minlength: 6,
    },
    profileImage: {
      type: String,
      default: "",
    },
  },
  { timestamps: true }
);
const User = mongoose.model("User", userSchema);

export default User;
```
建立数据模型视图便于在模型中定义静态方法和实例方法，提供数据操作的便携接口

上述案例中就创建了一个`User`的数据视图`Schema`以及建立了一个`User`数据模型并导出

### 参数配置
`mongoose.Schema()`是一个创建视图的方法，其中包括了模型需要的参数，上述样例中包含了两个花括号，其实两者是一个意思，即是可以合并的，`timestamps`值自动添加`createdAt`和`updatedAt`两个字段

>`type`类型可以沿用常见的类型，除此之外还有类似`mongoose.Schema.Types.ObjectId`的特殊类型，表示`mongodb`的`_id`字段

### 外键匹配
当我们在建立模型的时候，可能需要建立某些模型之间的联系，看下列案例
```js
const messageSchema = new mongoose.Schema(
  {
    senderID: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
      required: true,
    },
    receiverID: {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
      required: true,
    },
    text: {
      type: String,
    },
    image: {
      type: String,
    },
  },
  {
    timestamps: true,
  }
);
```
在上述案例中，存在`User`和`Message`两个模型，已知`Message`必须有发送者和接收者两个实体，这个实体又是`User`模型，即字段内容为别的模型
#### ref连接
通过`ref:'OtherModel'`我们可以指定字段连接别的模型，同时需要指定`type：mongoose.Schema.Types.ObjectId`使字段类型为`_id`，这样就建立了字段与模型的外键
#### populate填充
在查询时，使用`populate`来填充字段为指定模型，根据两者的`_id`为匹配依据对其进行填充，如
```js
Massage.find().populate('senderId').populate('receiverId','email fullname')
```
`mongodb`就会自动查找`_id`并填充对应数据
第二个参数可以指定需要填充的字段

## 创建模型实例Document
在上述例子中，我们首先创建了数据库视图`Schema`，然后根据视图创建了模型`Model`，模型相当于`MongoDB`数据集合的抽象，下一步就是创建具体的数据实例`Document`，也就是数据表视图中的记录
我们有三种方法创建`Document`记录：
1. 使用`new <Model>()`构造函数创建实例，然后通过`save()`方法将其保存到数据库记录中
2. 使用`<Model>.create()`方法直接创建一条记录
3. 使用`<Model>.insertMany()`创建大批量文档记录
>使用`await`方法创建异步请求保证记录顺序创建
```js
const Tank = mongoose.model('Tank', yourSchema);

const small = new Tank({ size: 'small' });
await small.save();

// or

await Tank.create({ size: 'small' });

// or, for inserting large batches of documents
await Tank.insertMany([{ size: 'small' }]);
```
>在与数据库的连接开启前，数据并不会被插入到数据库中
## 操作数据库
创建完数据记录，就可以对数据库执行增删改查操作了
包括：
1. 记录操作：增删改查等
2. 查询操作：各种条件查询
3. 特殊操作：比如使用`ref`进行连表

详见`mongoose`官方文档[Mongoose v8.9.4: Model (mongoosejs.com)](https://mongoosejs.com/docs/api/model.html)
