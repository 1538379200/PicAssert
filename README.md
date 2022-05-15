# PicAssert图片断言工具：
anchor： 测码范晔
联系邮箱： 1538379200@qq.com
当前版本：v 1.3.1
通过图片拓展断言方式
> assert_exist会将图片在全局做一次模板匹配行为，当查找的图片大于或者等于设置的阈值的时候，程序将返回True，
当全局匹配的图片匹配度低于所设置的阈值时，程序将启动特征匹配模式，对前面相似度较近的区域进行截图，再次进行特征分析，
如果特征分析的结果判断为图片相似，程序将返回True，否则返回False
assert_click图片点击返回一个分辨率的坐标点

## 参数
1、Assert类参数
    driver:                 传入的selenium.webdriver.Chrome的实例
    lock_conf:              是否锁定配置文件输入，设置为True则从配置文件读取配置，在其他设备运行增加兼容性
2、Assert().assert_exist()方法参数
    pic_path(str):          需要进行断言的图片路径，有传入driver则默认作用浏览器
    threshold(float|int):   整数或者浮点数，断言的判断阈值，0~1之间，默认0.7
3、Assert().assert_click()方法参数
    pic_path(str):          需要点击的目标图片，传入图片的路径，有传入driver默认作用浏览器
    hwnd(str):              字符串形式，应用于GUI界面，填写当前窗口的句柄，填写可以默认使用后台鼠标点击，不移动当前鼠标指针(传入driver的浏览器默认不用传入)

## 使用示例
```pycon
from PicAssert.Assert import Assert
from SafeDriver.drivers import driver, option


dr = driver()
ps = Assert(driver=dr, lock_conf=True)
res1 = ps.assert_exist(r'D:\test.png')
if res1 is True:
    print("找到图片")
else:
    print("未找到")
res2 = ps.assert_click(r'D:\test2.png')
print("当前点击坐标点：", res2)
```
## 如何提升兼容性
1、因为不同设备的分辨率尺寸，很难做到完全的兼容使用，目前建议在本机进行操作
2、浏览器运行，现在暂时不增加无头模式的运行兼容，因为其截图和设备尺寸的兼容现在没有很好的方法解决
