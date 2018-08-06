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








