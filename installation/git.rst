=========================== 
Git获得版本
=========================== 


windows下git的安装
------------------
	下载地址：
	.. code-block:: shell

		https://git-scm.com/downloads

	安装完成后进行后续的操作

本地获得远程仓库码
-------------------
* 在本地创建一个文件夹名为 如为：zhubaotujian，工程路径不能有中文
* 进入该文件夹，右键在弹框中点击 Git Bash Here
* 在弹出的页面中中出入下面的命令，后续需要输入密码的地方为git仓库用户的密码:Br@git

.. code-block:: shell

	git init 
	git remote add origin  ssh://git@192.168.21.141/home/git/zhubao.git
	git remote update
	git checkout -b master origin/master

* 代码更新
	* 拉取代码:

	.. code-block:: shell

		git pull origin master

	* 推送代码:
	
	.. code-block:: shell

		git add #需要更新的文件(git add  test_case/promotion_category/promotion_category.py)
		git commit -m "备注信息" #(git commit -m "产品管理用例完善")
		git pull origin master #(拉取代码，在commit之后，push之前拉取)
		git push origin master

* ps:每次推送代码前先执行代码拉取操作






