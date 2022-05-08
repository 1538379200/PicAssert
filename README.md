# PicAssert-- 图像断言

## 介绍
PicAsssert会将图片在全局做一次模板匹配行为，当查找的图片大于或者等于设置的阈值的时候，程序将返回True，
当全局匹配的图片匹配度低于所设置的阈值时，程序将启动特征匹配模式，对前面相似度较近的区域进行截图，再次进行特征分析，
如果特征分析的结果判断为图片相似，程序将返回True，否则返回False
程序依赖 opencv、pillow 进行图片的处理

## 使用特点说明
1、Assert类中最好设置一下 InitDPI ，以元祖或者列表的形式，写上当前编写代码设备的分辨率，提升兼容性
2、PicAssert的Assert类，如果添加了driver，则识别为selenium操作，将使用selenium进行截图，代码可以无头模式运行，但为了提升稳定性，
  请将窗口设置为当前编写代码的设备的分辨率大小，设置selenium浏览器窗口大小代码为：
  ```pycon
  dr.set_window_size(1920, 1080)
```
  Assert类如果没有添加任何参数，则默认截取设备的全屏，可以在其他gui代码中运行，注意不能关闭当前显示的屏幕
3、使用图片断言会返回一个布尔值，True为找到当前图片，False为未找到图片

## 调用方式
实例化Assert类：
```pycon
ps = Assert()  # ps = Assert(driver=driver)
ps.assert_exist("./test.png", 0.7)
```
assert_exist有两个形参
第一个参数：pic_path  需要判断的图片保存路径
第二个参数：threshold  断言阈值，当前默认 0.7，可调制0到1的区间，1为100%，请尽量控制在0.6到0.9之间

## 使用流程
1、正常编写代码，将需要断言的地方，使用工具进行截图，截图尽量不会包含其他可变的干扰，将其保存在一个路径中
2、导入PicAssert包，实例化Assert类，使用assert_exist，传入前面截图路径
3、获取返回值
4、运行完成，将在项目目录下，新建一个.assert_cache文件夹，下面有success和fail文件夹，成功断言放在success中，失败在fail中，程序每次运行会清空缓存文件

## selenium代码使用示例
```pycon
from SafeDriver.drivers import driver, option
import time
from PicAssert.Assert import Assert
dr = driver()
option.headless = True
dr.set_window_size(1920, 1080)
ps = Assert(dr)
ps.InitDPI = (1920, 1080)
dr.get("https://www.baidu.com")
time.sleep(2)
p1_res = ps.assert_exist(r"D:\test.png")     # ps.assert_exist(r"D:\test.png", 0.8)
if p1_res is True:
    print("图片存在")
else
    print("图片不存在")
```
