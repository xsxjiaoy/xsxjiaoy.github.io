# EmailJS 配置指南

本指南将帮助您配置 EmailJS 服务，实现网站表单提交功能，将用户信息发送到您的邮箱 1953419050@qq.com。

## 步骤 1：注册 EmailJS 账号

1. 访问 EmailJS 官网：https://www.emailjs.com/
2. 点击右上角的 "Sign Up" 按钮注册账号
3. 您可以使用 Google 账号、GitHub 账号或邮箱地址注册

## 步骤 2：添加邮件服务

1. 登录后，进入 Dashboard 页面
2. 点击左侧菜单中的 "Email Services"
3. 点击 "Add New Service" 按钮
4. 选择您的邮件提供商（例如 Gmail、QQ 邮箱、Outlook 等）
5. 按照提示授权您的邮箱账号
   - 对于 QQ 邮箱，您需要获取授权码（不是邮箱密码）
   - 如何获取 QQ 邮箱授权码：https://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=1001256

6. 授权成功后，您将看到新创建的服务，记录下 **Service ID**（格式：service_xxxxxxxx）

## 步骤 3：创建邮件模板

1. 点击左侧菜单中的 "Email Templates"
2. 点击 "Create New Template" 按钮
3. 设置模板名称（例如："Contact Form Submission"）
4. 在模板编辑器中设计您的邮件内容
   - 您可以使用以下变量：
     - `{{to_email}}` - 收件人邮箱（您的邮箱：1953419050@qq.com）
     - `{{from_name}}` - 家长姓名
     - `{{phone}}` - 联系电话
     - `{{child_grade}}` - 孩子年级
     - `{{subject}}` - 辅导科目
     - `{{message}}` - 留言内容

5. 示例模板内容：
   ```html
   <h2>新的家教咨询</h2>
   <p><strong>家长姓名：</strong>{{from_name}}</p>
   <p><strong>联系电话：</strong>{{phone}}</p>
   <p><strong>孩子年级：</strong>{{child_grade}}</p>
   <p><strong>辅导科目：</strong>{{subject}}</p>
   <p><strong>留言内容：</strong></p>
   <p>{{message}}</p>
   ```

6. 在 "To Email" 字段中输入您的邮箱：1953419050@qq.com
7. 设置邮件主题（例如："新的家教咨询 - {{from_name}}"）
8. 点击 "Save" 按钮保存模板，记录下 **Template ID**（格式：template_xxxxxxxx）

## 步骤 4：获取 API 密钥

1. 点击左侧菜单中的 "Account"
2. 在 "API Keys" 部分找到 **Public Key**
3. 记录下您的 Public Key（格式：user_xxxxxxxx）

## 步骤 5：更新网站代码

1. 打开网站项目中的 `index.html` 文件
2. 找到以下代码部分：
   ```javascript
   // 初始化EmailJS
   // 请按照以下步骤获取您的EmailJS配置信息：
   // 1. 访问https://www.emailjs.com/注册账号
   // 2. 添加邮件服务（如Gmail、QQ邮箱等）
   // 3. 创建邮件模板
   // 4. 在Account > API Keys中获取您的Public Key（用户ID）
   emailjs.init('user_your_user_id'); // 替换为您的EmailJS用户ID（Public Key）
   ```

3. 将 `user_your_user_id` 替换为您的 Public Key

4. 找到以下代码部分：
   ```javascript
   // 发送邮件
   // 请替换以下参数：
   // 1. 'service_your_service_id' - 您的EmailJS服务ID
   // 2. 'template_your_template_id' - 您的EmailJS模板ID
   // 3. 确保模板中的变量名与formData中的键名一致
   emailjs.send('service_your_service_id', 'template_your_template_id', {
       to_email: '1953419050@qq.com', // 接收邮件的邮箱地址
       from_name: formData.name,
       phone: formData.phone,
       child_grade: formData.child_grade,
       subject: formData.subject,
       message: formData.message
   })
   ```

5. 将 `service_your_service_id` 替换为您的 Service ID
6. 将 `template_your_template_id` 替换为您的 Template ID

## 步骤 6：测试表单提交功能

1. 保存修改后的 `index.html` 文件
2. 打开网站，填写表单并提交
3. 检查您的邮箱（1953419050@qq.com）是否收到测试邮件
4. 如果邮件发送失败，请检查浏览器控制台中的错误信息，确保所有配置信息正确

## 常见问题解决

### 1. 邮件发送失败，显示 "Invalid service ID"

- 检查您的 Service ID 是否正确复制
- 确保您的邮件服务已正确配置并授权

### 2. 邮件发送失败，显示 "Invalid template ID"

- 检查您的 Template ID 是否正确复制
- 确保模板中的变量名与代码中的键名一致

### 3. QQ 邮箱授权问题

- 确保您使用的是授权码而不是邮箱密码
- 检查您的 QQ 邮箱安全设置，确保允许第三方应用访问

### 4. 邮件发送成功但未收到邮件

- 检查您的垃圾邮件文件夹
- 确保您的邮箱没有将 EmailJS 的邮件标记为垃圾邮件

## 注意事项

- EmailJS 免费账户每月有 200 封邮件的发送限制
- 不要在客户端代码中暴露您的 Private Key，只使用 Public Key
- 定期检查您的 EmailJS Dashboard，查看邮件发送状态和历史记录

完成以上步骤后，您的网站表单提交功能将正常工作，用户填写的信息将自动发送到您的邮箱 1953419050@qq.com。
