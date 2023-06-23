# tasks

可中断和恢复的任务序列，任务序列应该为 promise 数组，依次顺序执行一系列任务，所有任务全部完成后可得到执行结果

## 安装
### npm

下载扩展库
``` bash
npm i @aardiolib/tasks
```

复制扩展库到用户库
``` bash
robocopy .\node_modules\@aardiolib\ .\lib\ /E
```

## 示例

简单示例
```js
import console;
import win.ui;
import promise;
import tasks;
/*DSG{{*/
var winform = win.form(text="tasks";right=300;bottom=124)
winform.add(
button={cls="button";text="开始";left=16;top=30;right=125;bottom=87;z=1};
button2={cls="button";text="暂停";left=167;top=30;right=276;bottom=87;z=2}
)
/*}}*/

var taskList = {};

for(i=1;5;1){
	table.push(taskList,function(){
		return ..promise(function(resolve,reject){
			..console.log(i,"执行中")
		    winform.setTimeout(function(){
		        ..console.log(i,"执行完成")
		    	resolve(i)
		    },2000)
		})
		
	})
}

var processor = tasks(taskList);

winform.button.oncommand = function(id,event){
	console.log("点击开始")
	winform.button.disabled = true;
	
	processor.start().then(function(results){
		console.log("执行结果:");
		console.dumpJson(results);
		winform.button.disabled = false;
	},function(err){
		console.log("执行被中断");
		console.log(err);
	})
}

winform.button2.oncommand = function(id,event){
	console.log("点击暂停")
	winform.button2.disabled = true;
	processor.pause().then(function(){
		console.log("已暂停")
		winform.button.disabled = false;
		winform.button2.disabled = false;
	});
}

winform.show();

win.loopMessage();
```