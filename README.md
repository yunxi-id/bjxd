function 提示(内容)
Toast.makeText(this, 内容,Toast.LENGTH_SHORT).show()
end
 
function 检测更新(Github地址)
local dl=ProgressDialog.show(activity,nil,'更新检测中…')
dl.show()
local tt=Ticker()
tt.start()
packinfo=this.getPackageManager().getPackageInfo(this.getPackageName(),((1552294270/8/2-8392)/32/1250-25.25)/8-236)
version=tostring(packinfo.versionName)
versioncode=tostring(packinfo.versionCode)
 
url=Github地址;
function 过滤(content)
版本名=content:match("【版本名】(.-)【版本名】")
版本=content:match("【版本】(.-)【版本】")
内容=content:match("【内容】(.-)【内容】")
链接=content:match("【链接】(.-)【链接】")
if(版本名==nil) then
版本名="获取失败"
end
if(版本==nil) then
版本="0"
end
if(内容==nil) then
内容="获取失败"
end
if(链接==nil) then
提示("服务器参数配置错误，请过段时间再次尝试")
end
 
if(版本 > versioncode) then
dl.dismiss()
tt.stop()
对话框()
.设置标题("检测到更新")
.设置消息("版本："..version.."→"..版本名.."\n更新内容："..内容)
.设置积极按钮("下载更新",function()
下载文件(链接)
提示("下载更新中…")
end)
.设置消极按钮("取消更新")
.显示()
else
dl.dismiss()
tt.stop()
提示("当前已是最新版本！")
end
end
Http.get(url,nil,"UTF-8",nil,function(code,content,cookie,header)
if(code==200 and content)then
过滤(content)
else
dl.dismiss()
tt.stop()
提示("本地网络或服务器异常 "..code)
end
end)
end
