#!/usr/bin/env python
# coding=utf-8



from time import sleep
from selenium import webdriver

#定义一个upload　类，用于通过cookick　免密登录，避免使用密码登录
class upLoad():
    url = ""
    #定义一个构造函数,传入网址和cooick
    def __init__(self, url, cooick):
        self.url = url
        self.driver = webdriver.Chrome()#通过webdriver启动chrome浏览器
        self.driver.get(url)#打开某一网址，获取浏览器的cooick
        #打开本地文件cooick 每次取出一行
        with open(cooick, "r") as f:
            for line in f:
                name, value, domain = line.strip().split('\t')#划分每行的三个值
                cookie = {"name":name, "value" : value, "domain" : domain}
                self.driver.add_cookie(cookie)#把去到的值添加到浏览器中
        #正式启动浏览器
        self.driver.get(self.url)

#定义一个downLoad类，用于下载文件
class downLoad(upLoad):
    #get_link方法 :用于获取每个课程的程序设计地址
    def get_link(self):
        names = []
        timus = [] 
        #首先通过八种查找方式中的ｃｓｓ查找到每个单元,把对象存放于lessons列表
        lessons = self.driver.find_elements_by_css_selector("[class = 'jsk-list jsk-list-striped lessons']")
        for x in lessons:
            #通过标签名的查找方式找到每个<li>标签,存放在status列表中
            status = x.find_elements_by_tag_name("li")
            for y in status:
                #通过查看<span>标签里的属性值判断该程序设计是否已经完成,把完成的titlie 和 href 的值分别存在列表里，用字典存储其实更好
                spans =  y.find_elements_by_tag_name("span")
                if spans[0].get_attribute('title') == "已完成":
                    if spans[0].get_attribute('class') == "lesson-icon-challenge":
                        #print(y.find_element_by_tag_name('a').get_attribute('href'))
                        timu = spans[1].get_attribute('title')
                        timus.append(timu)
                        name = y.find_element_by_tag_name('a').get_attribute('href')
                        names.append(name)
        return names,timus
    
    # get_text方法用于获取课程里的代码
    def get_text(self, cd_name, names, timus):
        #通过便利get_link获取到的链接地址获取所有代码
        for i in range(len(timus)):
            self.driver.get(names[i])
            sleep(1)
            #模拟点击操作,sleep()的作用是防止页面没有加载完成，无法找打元素
            self.driver.find_element_by_link_text("稍后继续").click()
            sleep(2)
            #通过xpath进行查找要注意绝对路径和相对路径的区别，xpath有少许的浪费资源,xpath 可以自己写亦可以网页生成
            self.driver.find_element_by_xpath("//div//a[@id = 'submit-history-trigger']").click()
            sleep(2)
            self.driver.find_element_by_xpath('//*[@id="submit-history"]/div/div[2]/table/tbody/tr[1]/td[5]/a').click()
            sleep(2)
            #由于历史按键点击之后会打开新的窗口，要使用switch_to.window(driver.window_handles[1])表示第二个窗口
            self.driver.switch_to.window(self.driver.window_handles[1])
            pre = self.driver.find_elements_by_tag_name('pre')
            #print(pre[0].text)
            #进行文件的简单存储
            filename = cd_name +str(timus[i])+ ".text"
            f = open(filename, 'w')
            f.write(pre[0].text)
            f.close()
            sleep(1)
            #为了防止窗口不断打开新的要记得爬取完代码关闭窗口,并切换会第一个窗口
            self.driver.close()
            self.driver.switch_to.window(self.driver.window_handles[0])

if __name__ == "__main__":
    course = ["./1.python/", "./2.c++/", "./3.c/", "./4.data_structure/"]
    url = ['https://www.jisuanke.com/course/788','https://www.jisuanke.com/course/787','https://www.jisuanke.com/course/786','https://www.jisuanke.com/course/792']
    cooick = "./cooick"
    for i in range(len(course)):
    #driver = upLoad(url, cooick)
        print(url[i])
        #在实例化download对象时系统会默认先调用父类的初始化方法，所以不用单独实例化一个父类对象
        downLoad_text = downLoad(url[i], cooick)
        names, timus = downLoad_text.get_link()
        downLoad_text.get_text(course[i], names, timus)
        
    
