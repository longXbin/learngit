# selenium
http://www.cnblogs.com/jinxiao-pu/p/6677782.html

2018-05-07
1、 安智网某站SQL注入到GetShell：http://10.71.146.169/static/bugs/wooyun-2016-0217072.html
2、 中行云平台SQL注入涉及北京地区数十万用户身份信息：http://10.71.146.169/static/bugs/wooyun-2016-0185574.html
3、 名鞋库某站SQL报错注入：http://10.71.146.169/static/bugs/wooyun-2016-0175545.html
4、 凤凰网某分站存在SQL注射漏洞：http://10.71.146.169/static/bugs/wooyun-2016-0182189.html

https://blog.csdn.net/spring292713/article/details/39667835
http://www.jb51.net/article/49573.htm


https://github.com/thinkgem/jeesite

https://pan.baidu.com/s/1pN-i9L3R-7dNAFVJfE_4vw   4I00

https://www.cnblogs.com/bananaplan/p/remove-listitem-while-iterating.html

https://blog.csdn.net/liyuanbhu/article/details/7882789









package com.picture;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

import sun.misc.BASE64Decoder;
import sun.misc.BASE64Encoder;

public class Base64Image {
    public static void main(String[] args) {
        //测试从Base64编码转换为图片文件
        String imgStr = "";
        base64ToImage(imgStr, "D:/wangyc.jpg");
        
        //测试从图片文件转换为Base64编码
        String imageToBase64 = imageToBase64("D:/wangyc.jpg");
        System.out.println(imageToBase64);
    }
    
    /**
     * 对字节数组字符串进行Base64解码并生成图片
     */
    public static boolean base64ToImage(String imgStr, String filePath) {
        if(imgStr == null) // 图像数据为空
            return false;
        BASE64Decoder decoder = new BASE64Decoder();
        try {
            // Base64解码
            byte[] bytes = decoder.decodeBuffer(imgStr);
            for (int i = 0; i < bytes.length; ++i) {
                if (bytes[i] < 0) {// 调整异常数据
                    bytes[i] += 256;
                }
            }
            
            // 生成图片
            OutputStream out = new FileOutputStream(filePath);
            out.write(bytes);
            out.flush();
            out.close();
            return true;
        } catch (Exception e) {
            return false;
        }
    }
    
    /**
     * 将图片文件转化为字节数组字符串，并对其进行Base64编码处理
     */
    public static String imageToBase64(String filePath) {
        byte[] data = null;
        //读取图片字节数组
        try {
            InputStream in = new FileInputStream(filePath);
            data = new byte[in.available()];
            in.read(data);
            in.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // 对字节数组Base64编码
        BASE64Encoder encoder = new BASE64Encoder();
        return encoder.encode(data);
    }
}

https://blog.csdn.net/poorcoder_/article/details/71374002

https://blog.csdn.net/gnail_oug/article/details/80705718
http://blog.51cto.com/wyait/2107423

http://jinnianshilongnian.iteye.com/blog/2029217

https://blog.csdn.net/LHacker/article/details/19340757

步骤：

1、在自定义的Realm增加方法：

public void clearAuthz(){
this.clearCachedAuthorizationInfo(SecurityUtils.getSubject().getPrincipals());
}
2、在自己的service调用这个方法：

RealmSecurityManager rsm = (RealmSecurityManager)SecurityUtils.getSecurityManager();
AuthRealm authRealm = (AuthRealm)rsm.getRealms().iterator().next();
authRealm.clearAuthz();


http://www.cnblogs.com/EasonJim/p/7481825.html

http://pangguoming.com/2018/02/07/springboot-shiro-401/

https://blog.csdn.net/towtotow/article/details/79244817

https://blog.csdn.net/yingxiake/article/details/51224569
https://blog.csdn.net/zhangdehua678/article/details/78913839


https://blog.csdn.net/neweastsun/article/details/78775371

https://blog.csdn.net/qq_31489805/article/details/80267916 shiro整合springboot前后端分离
https://blog.csdn.net/palerock/article/details/73457415
https://blog.csdn.net/haoyuyang/article/details/80036989
https://blog.csdn.net/poorCoder_/article/details/71374002
https://blog.csdn.net/cckevincyh/article/details/79633661
https://ask.csdn.net/questions/652023
https://blog.csdn.net/shadowTime/article/details/80483377

https://blog.csdn.net/zxssoft/article/details/79651889 mysql 模糊匹配优化

https://blog.csdn.net/u013939884/article/details/72860358 彻底找到 Tomcat 启动速度慢的元凶

https://blog.csdn.net/jancislo/article/details/80847104 sql注入
https://blog.csdn.net/qq_23184291/article/details/79651093

https://www.cnblogs.com/sunshineatnoon/p/4064632.html cas登录

https://blog.csdn.net/Bupt_Lili/article/details/80424894 通知
http://www.cnblogs.com/tinyj/archive/2018/10/16/9797807.html

http://icollege.isoftstone.com/pages/learner/course_chapter.jsp?courseId=563&courseUserId=1555 软通考试

https://blog.csdn.net/qq_19729969/article/details/80902577 小程序日期时间控件
https://blog.csdn.net/lizhipeng123321/article/details/82775575

https://bbs.csdn.net/topics/392299866

十大纲领 CCCDB DCBCD

会议管理 BCBBD DDDDC

考勤管理 DABCB BDAAB 

日清邮件 DBACD CDBAB

工作方法 DACDA D\D\BC\BD\AD

企业微信 BDCCD DBBDD 

总结汇报 BAABC DACBD

费用管理 CCADB ABDDB

客户服务 BBADB D/A/AC/CD/BC

廉政自律 DBDCC DDDAB

信息安全 ABDDB CDBBA ACBBA CACCC
以上是企业文化的考试答案
晚上回去考下试

https://blog.csdn.net/kai46385076/article/details/39122313

https://www.cnblogs.com/demodashi/p/9436573.html//小程序登录前后台流程


https://blog.csdn.net/Charles_Tian/article/details/81980409?utm_source=copy

https://www.cnblogs.com/mfrbuaa/p/4588057.html//apk反编译


https://time.geekbang.org/column/article/14577 测试52讲
