# IOS_IPA
一、打包ipa和生成.plist文件具体步骤：
1、在苹果开发者后台生成签名文件，使用developer profile或者adhoc distribution profile这边注意不能使用distribution profile，因为这不是发布到Appstore。 
2、生成archive，点击菜单栏product中的archive选项进行打包 
3、在organizer中点击archive进行distribute，发布的过程中注意选择save for enterprise distribution，不然会失败，完成保存会生成俩文件 .ipa文件和 .plist文件。其中.ipa文件就是应用程序文件， .plist文件是苹果需要通过itms-services协议访问的文件。

下面是.plist文件的格式
<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">  
<plist version="1.0">  
<dict>  
    <key>items</key>  
    <array>  
        <dict>  
            <key>assets</key>  
            <array>  
                <dict>  
                    <key>kind</key>  
                    <string>software-package</string>  
                    <key>url</key>  
                    <string>http://113.200.5.104:8996/wJob/job.ipa</string>  
                </dict>  
            </array>  
            <key>metadata</key>  
            <dict>  
                <key>bundle-identifier</key>  
                <string>com.qgbes.pjob</string>  
                <key>bundle-version</key>  
                <string>1.0.0</string>  
                <key>kind</key>  
                <string>software</string>  
                <key>title</key>  
                <string>测试APP免Appstore安装项目</string>  
            </dict>  
        </dict>  
    </array>  
</dict>  
</plist>
-----------------------------------------------------------
<key>url</key>  
<string>http://113.200.5.104:8996/wJob/job.ipa</string>
===========================================================
这边是我们生成的ipa文件存放的位置。

二、现在万事俱备只欠东风啦，只需要客户端能够成功访问到我们生成的.plist文件即可。
本来觉得和ipa文件一样，放在服务器上是，访问一下就OK啦，结果发现，最新版本是不行的，之前确实可以通过http的方式进行访问plist文件进行安装，不过现在苹果规定必须以https的方式进行访问。

以https方式访问plist文件的解决方案
1、配置tomat支持https方式访问 
2、利用dropbox分享外链进行访问原始文件 
3、利用开源中国的git&osc分享外链进行访问原始文件

说说三种方式，
第一种方式：对于只使用http方式访问来配置的tomcat，本身来改配置代价高，而且没必要。 
第二种方式：dropbox是国外的，而且是要翻墙的，也就是存在不稳定情况，不通用。 
第三种方式：国内网站，简单，稳定

这边我们也就只是需要访问个文件，简单点就在git&osc上放个文件，提供个文件链接就OK啦。

三、打开客户端safari浏览器，输入
itms-services://?action=download-manifest&url=‘plist文件地址’
这样就结束啦，反正我这边是安装成功啦~~~

总结下注意点 
1、签名要使用developer profile或者adhoc distribution profile,不能使用distribution profile 
2、个人开发者证书只能在100个设备中实现无线安装 
3、最新版ios设备支持https方式访问plist文件（ipa文件是可以通过http方式访问的）
