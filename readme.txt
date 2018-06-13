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









# -*- coding: utf-8 -*-
import re,os,xlwt,time,xlrd
from xlwt import Workbook

def listFiles(path, setFiles):
    if os.path.isfile(path):
        file_path = os.path.split(path)#分割出目录和文件名
        filename = file_path[1]#得到文件名
        file_ext = filename.split('.')[-1]#得到文件类型
        if re.search('mapper',filename,re.I) and re.match('xml',file_ext,re.I): #找出mybatis文件
            setFiles['mybatis'].append(path)
            #print(path)
        elif re.match('py',file_ext,re.I): #找出python文件
            setFiles['python'].append(path)
            #print(path)
    elif os.path.isdir(path):
            for x in os.listdir(path):
                listFiles(os.path.join(path, x), setFiles)
    #return setFiles

def readMybatsFile(filename, listResult):
    f = open(filename,'r')#,encoding='utf-8'
    line = f.readline()
    i = 0
    flag = True
    isInComment = True
    servicename = getServiceName(filename)
    while line:
        i = i + 1
        start = line.count('<!--');#统计注释开头符号
        end = 0 - line.count('-->');#统计结束开头符号
        if start > 0 or end < 0:#存在注释符号
            if start + end > 0:#<!--进入注释
                isInComment = False
            elif start + end < 0:#-->结束注释
                isInComment = True
        if not isInComment:#处于注释之间的内容不处理
            line = f.readline()
            continue
        if line.find('$')>=0:
            #记录相应结果
            result = {}
            result['ServiceName'] = servicename
            result['LineNum'] = i
            result['ErrorKeyWord'] = line
            result['FileName'] = filename
            result['Type'] = 'mybatis'
            result['Result'] = 'fail'
            listResult.append(result)
            flag = False
        line = f.readline()
    if flag:#没有检测问题
        result = {}
        result['ServiceName'] = servicename
        result['LineNum'] = 0
        result['ErrorKeyWord'] = 'NA'
        result['FileName'] = filename
        result['Type'] = 'mybatis'
        result['Result'] = 'success'
        listResult.append(result)
    f.close()
    return listResult

def readPythonFile(filename, listResult):
    f = open(filename,'r')#,encoding='utf-8'
    line = f.readline()
    i = 0
    flag = True
    servicename = getServiceName(filename)
    while line:
        i = i + 1
        if re.search('MySQLdb\.connect|Oracle\.connect|pymssql\.connect|sqlite3\.connect|pymysql\.connect|pymongo\.connect|redis\.connect|redis\.Redis|pyredis\.Client|memcache\.Client',line,re.I):#检测sql关键字
            #记录相应结果
            result = {}
            result['ServiceName'] = servicename
            result['LineNum'] = 0
            result['ErrorKeyWord'] = ''
            result['FileName'] = filename
            result['Type'] = 'python'
            result['Result'] = 'fail'
            listResult.append(result)
            flag = False
            break
        line = f.readline()
    if flag: #没有检测问题
        result = {}
        result['ServiceName'] = servicename
        result['LineNum'] = 0
        result['ErrorKeyWord'] = ''
        result['FileName'] = filename
        result['Type'] = 'python'
        result['Result'] = 'success'
        listResult.append(result)
    f.close()
    return listResult

#保存xls文件
def listToExcel(listResult, keys, file):
    book = Workbook(encoding='utf-8')
    sheet1 = book.add_sheet('sheet1')
    #先添加第一列表头
    i = 0
    for title in keys:
        sheet1.write(0,i,title)
        i = i+1
    #添加数据
    i = 1
    for result in listResult:
        for j in range(len(keys)):
            sheet1.write(i,j,result[keys[j]])
        i = i+1
    #保存文件
    book.save(filename)

#读取xls文件
def readXlsFile(filename, conFile):
    try:
        data = xlrd.open_workbook(filename)
        table = data.sheets()[0]#通过索引顺序获取
        nrows = table.nrows
        for i in range(nrows ):
            conFile.append(table.row_values(i))
        return conFile
    except(Exception, e):
        print(Exception,e)
        return conFile

#得到服务名
def getServiceName(filename):
    filename = filename.replace('\\','/')
    g = re.match('.*(/.+Service.*?/)',filename)
    if g:
        return g.group(1).replace('/','').split("Service")[0] + "Service"
    else:
        return ''

#读取Txt文件
def readTxtFile(filename, conFile):
    try:
        for line in open(filename,'r'):#,encoding='utf-8'
            line = line.replace("\n","").replace("\r","").strip()
            if line:
                conFile.append(line);
        return conFile
    except:
        return conFile
#比较结果
def compareResult(xlsResult, dataResult):
    #'ServiceName','Type','FileName','Result','LineNum','ErrorKeyWord'
    servicename = str(dataResult['ServiceName'])
    fileType = str(dataResult['Type'])
    fileName = str(dataResult['FileName'])
    result = str(dataResult['Result'])
    lineNum = (dataResult['LineNum'])
    errorKeyWord = str(dataResult['ErrorKeyWord'])
    #print("data:",servicename,fileType,fileName,result,lineNum,errorKeyWord)
    #print(" xls:",str(xlsResult[0]),str(xlsResult[1]),str(xlsResult[2]),str(xlsResult[3]),(xlsResult[4]),str(xlsResult[5]))
    try:
        if str(xlsResult[0])==servicename and str(xlsResult[1])==fileType and str(xlsResult[2].encode('utf-8'))==fileName and str(xlsResult[3])==result and int(xlsResult[4])==lineNum and str(xlsResult[5].encode('utf-8'))==errorKeyWord:
            return True
        else:
            return False
    except(Exception, e):
        print(Exception,e)
        return False

if __name__ == '__main__':
    setFiles = {'mybatis':[],'python':[]}
    #获取读取文件，没有默认从当前目前开始读取
    sacnFile = [];
    sacnFile = readTxtFile('scan.txt',sacnFile)
    if sacnFile:
        for filename in sacnFile:
            listFiles(filename, setFiles)
    else:
        listFiles(os.getcwd(), setFiles)
    #获取过滤文件
    filterFile = [];
    filterFile = readTxtFile('filter.txt',filterFile)
    filterFile.append(os.getcwd()+'\\sqlcheck.py')#过滤本身文件
    for ffile in filterFile:
        for i in range(len(setFiles['mybatis'])-1,-1,-1):
            if setFiles['mybatis'][i].startswith(ffile):
                setFiles['mybatis'].pop(i)
        for i in range(len(setFiles['python'])-1,-1,-1):
            if setFiles['python'][i].startswith(ffile):
                setFiles['python'].pop(i)
    #print(setFiles)
    #检测文件
    listResult = []
    for filename in setFiles['mybatis']:
        listResult = readMybatsFile(filename,listResult)
    for filename in setFiles['python']:
        listResult = readPythonFile(filename,listResult)
    #过滤结果
    resultFilterFile = [];
    resultFilterFile = readXlsFile('resultFilter.xls',resultFilterFile)
    for result in resultFilterFile:
        for i in range(len(listResult)-1,-1,-1):
            if compareResult(result,listResult[i]):
                listResult.pop(i)
                break

    keys = ['ServiceName','Type','FileName','Result','LineNum','ErrorKeyWord']
    filename = 'sqlcheck_'+time.strftime('%Y%m%d%H%M%S',time.localtime(time.time())) + '.xls'
    listToExcel(listResult, keys, filename)
    print('检测结果成功')
