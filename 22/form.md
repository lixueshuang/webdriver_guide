form的操作
===================

场景
-----
表单对象的操作比较简单，只需要记住下面几点

* 使用send_keys方法往多行文本框和单行文本框赋值；
* 使用click方法选择checkbox
* 使用click方法选择radio
* 使用click方法点击button
* 使用click方法选择option，从而达到选中select下拉框中某个具体菜单项的效果

代码
----

### form.html
```
	<html>
		<head>
			<meta http-equiv="content-type" content="text/html;charset=utf-8" />
			<title>form</title>		
			<script type="text/javascript" async="" src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
			<link href="http://netdna.bootstrapcdn.com/twitter-bootstrap/2.3.2/css/bootstrap-combined.min.css" rel="stylesheet" />		
			<script type="text/javascript">
				$(document).ready(function(){
						$('input[type=submit]').click(function(){
							alert('watir-webdriver is better than selenium webdriver');
						});
				});
			</script>
		</head>
			
		<body>
			<h3>form</h3>
			<div class="row-fluid">
				<div class="span6 well">		
					<form>
						<fieldset>
							<legend>Legend</legend>						
							<label class="checkbox">
								<input type="checkbox"> Check me out
							</label>
							
							<label class="radio">
								<input type="radio"> select me 
							</label>
							
							<label class="select">
								<select>
									<option>0</option>
									<option>1</option>
									<option>2</option>
								</select> select one item
							</label>
							
							<input type="submit" class="btn" value="submit" />
						</fieldset>
					</form>
				</div>
			</div>
		</body>
		<script src="http://netdna.bootstrapcdn.com/twitter-bootstrap/2.3.2/js/bootstrap.min.js"></script>
	</html>
```

### form.rb
```
	#encoding: utf-8
	require 'selenium-webdriver'

	dr = Selenium::WebDriver.for :chrome
	file_path = 'file:///' + File.expand_path(File.join('.', 'form.html'))
	dr.get file_path

	# 选中checkbox
	dr.find_element(:css, 'input[type=checkbox]').click()
	sleep(1)

	# 选中radio
	dr.find_element(:css, 'input[type=radio]').click()
	sleep(1)

	# 选择下拉菜单中的最后一项
	dr.find_element(:tag_name, 'select').find_elements(:tag_name, 'option').last.click()
	sleep(1)

	# 点击提交按钮
	dr.find_element(:css, 'input[type=submit]').click()
	sleep(1)

	alert = dr.switch_to.alert
	puts alert.text
	alert.accept()

	dr.quit()
```

