# Firebase Firestore 配置说明

## 1. 创建 Firebase 项目

1. 访问 [Firebase Console](https://console.firebase.google.com/)
2. 点击"创建项目"
3. 输入项目名称，例如："yeyuruoying-website"
4. 按照向导完成项目创建

## 2. 启用 Firestore 数据库

1. 在 Firebase 控制台中，点击左侧菜单的"Firestore Database"
2. 点击"创建数据库"
3. 选择"以测试模式启动"（稍后可以修改安全规则）
4. 选择数据库位置（建议选择亚洲地区）

## 3. 获取配置信息

1. 在 Firebase 控制台中，点击左侧菜单的"项目设置"（齿轮图标）
2. 在"常规"标签下，滚动到"您的应用"部分
3. 点击"添加应用" → 选择"Web"应用
4. 输入应用昵称，例如："留言板"
5. 复制生成的配置对象

## 4. 更新网站配置

将 `messages.html` 文件中的以下部分替换为您的实际配置：

```javascript
const firebaseConfig = {
    apiKey: "your-api-key",
    authDomain: "your-project.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789",
    appId: "your-app-id"
};
```

## 5. 设置 Firestore 安全规则

在 Firestore 控制台中，点击"规则"标签，将规则修改为：

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /messages/{document} {
      allow read: if true;
      allow write: if true;
    }
  }
}
```

## 6. 测试功能

1. 打开留言板页面
2. 填写姓名和留言内容
3. 点击"发表留言"
4. 检查 Firestore 控制台是否有新数据

## 注意事项

- 测试模式的安全规则允许任何人读写数据，请在生产环境中设置更严格的规则
- 留言内容会进行HTML转义以防止XSS攻击
- 姓名限制20个字符，留言内容限制500个字符 