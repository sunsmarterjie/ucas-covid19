# ucas-covid19(魔改版)

国科大疫情防控每日填报助手: 用于解决忘记填写企业微信中身体状况每日打卡的问题。


# 注意
本人不对因为滥用此程序造成的后果负责，**请在合理且合法的范围内使用本程序**。

**本程序仅用于解决忘记打卡这一问题，如果填报表中任意情况发生变化，比如地点发生变化，处在居家隔离阶段等情况，请务必在程序运行之前手动打卡。由于各种已知的或未知的原因可能造成打卡信息不一定总是准确的，请经常人工查看企业微信里面的填报表信息是否正确**


打卡网站可能会经常更新，因此代码会做更改。如果在使用过程中遇到问题或者发现 bug，可以提 issue 或者加入 [Telegram](https://t.me/ucas_covid19) 交流，代码更新也会在此处通知。
如果想要即时得知代码的更新请 watch 本仓库。

有特殊需求的同学可以修改本代码，但请遵守`CC BY-NC-SA 3.0` 许可协议。




# 方法二： 使用 GitHub Actions（推荐使用）
没有服务器的同学可以使用 GitHub Action 来进行运行此程序。

**请勿**直接修改`sub.py`内的登录账号和密码，Github的公开仓库的内容可以被所有人查看。

Github提供了一个secret功能，用于存储密钥等敏感信息，请按照以下步骤操作。

使用步骤:
- 点击右上角 `star` :)
- 克隆这个仓库到你名下
- fork的仓库默认禁用了`workflow`，需要手动打开：点击 `actions`选项卡，点击`I understand my workflows, go ahead and run them`。
- 在仓库设置里面, 设置 secrets 如下
  - `SEP_USER_NAME`: 你的 SEP 用户名(邮箱)
  - `SEP_PASSWD`: 你的 SEP 密码
  
- 测试actions是否可以正常工作：编辑本项目内任意文件，推荐修改`README.md`，比如添加一个空行，并提交以触发action运行，提交后的一分钟左右可以在action选项卡中看到运行记录


参考截图设定以上三个secrets，`API_KEY`可选。
![](setting.png)


完成之后, 每天 UTC 0:10 (北京时间 8:10) 自动触发 github actions 进行填报 。

如果 fork 之后想更新至本仓库最新代码，请参考[此教程](https://blog.csdn.net/qq_35246620/article/details/98039346) 。


只接受PR，不接受需求。

# changelog
- 2020年4月15日 添加了随机等待`10-600`秒之后再进行填报
- 2020年4月15日 添加了`user-agent`
- 2020年4月15日 更新了README，添加了设定secrets页面的截图
- 2020年6月12日 更新了README，提醒同学请勿直接在代码中填写密码
- 2020年6月14日 更新了README，添加有关触发action运行的说明
- 2020年6月24日 适配了网站的字段的更新；添加了 debug模式隐藏打卡信息；github action直接输出打卡结果；移除了 serverless 方式的支持
- 2020年9月16日 适配了网站的字段的更新
- 2020年9月26日 更新了README，添加了使用windows计划任务的操作步骤
- 2020年11月3日 更新了README，添加了 MacOS系统中 crontab 的配置方法
- 2020年11月6日 添加了 Telegram Group
- 2020年11月7日 使用环境变量传递口令，解决密码中存在特殊字符导致 sed 截断的问题
- 2020年11月9日 bugfix: 修复环境变量传递口令中存在的 bug， 经过测试已经 work 了，面壁思过中 :( 
- 2020年12月2日 网站证书配置有误导致打卡失败，修改代码为不验证证书
- 2020年12月22日 添加邮件通知
- 2021年1月21日 判断所在地点是不是国内，如果不是国内，则提示手动打卡
- 2021年1月25日 添加 `去往何处`等字段
- 2021年1月25日 缓存了 cookies 到文件中，避免登录失败导致无法打卡
- 2021年1月25日 重构了检查提交信息的代码
- 2021年1月25日 重构了发送通知的代码
- 2021年1月25日 添加了 github actions 缓存 cookies 的配置
- 2021年1月27日 优化了取 github 环境变量的方式，减少未设置变量导致出错的概率；兼容 python 3.5 的 pathlib
- 2021年1月29日 解决接触时间 1970-01-01的问题， 见 [issue 36](https://github.com/IanSmith123/ucas-covid19/issues/36)


# 致谢
- 感谢 [karuboniru](https://github.com/IanSmith123/ucas-covid19/pull/1) 提供的github actions 支持
- 感谢 [tyfulcrum](https://github.com/IanSmith123/ucas-covid19/pull/2) 对文档的完善工作
- 感谢 [HsimWong](https://github.com/IanSmith123/ucas-covid19/pull/3) 对文档的完善工作
- 感谢 [spwpun](https://github.com/IanSmith123/ucas-covid19/pull/6) 添加了使用 windows 计划任务的操作步骤
- 感谢 [PrimeMHD ](https://github.com/IanSmith123/ucas-covid19/pull/7) 添加了使用 MacOS 的 crontab 的配置步骤
- 感谢 [T-winkle](https://github.com/IanSmith123/ucas-covid19/pull/24) 添加了邮件通知打卡结果的功能
- 感谢 [lizard1998myx](https://github.com/IanSmith123/ucas-covid19/pull/28) 修复了提交信息缺少`去往何处`等字段的问题

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png" /></a><br />本作品采用<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/">知识共享署名-非商业性使用-相同方式共享 3.0 未本地化版本许可协议</a>进行许可。


Les1ie

2020-4-5 23:56:52
