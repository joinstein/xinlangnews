# xinlangnews
python
import requests as re
from bs4 import BeautifulSoup
res = re.get('http://news.sina.com.cn/china/')
res.encoding = 'utf-8'
# print(res.text)
soup = BeautifulSoup(res.text,'html.parser')
# print(soup)
for news in soup.select('.news-item'):
    if len(news.select('h2')) > 0:
        h2 = news.select('h2')[0].text
        time = news.select('.time')[0].text
        a = news.select('a')[0]['href']
        print(time,h2,a)
import requests as req
from bs4 import BeautifulSoup
import json,re

res = req.get('http://news.sina.com.cn/c/2017-05-03/doc-ifyexxhw2088205.shtml')
res.encoding = 'utf-8'
# print(res.text)
soup = BeautifulSoup(res.text,'html.parser')
# print(soup)
tite = soup.select('#artibodyTitle')[0].text
time = soup.select('#navtimeSource')[0].contents[0].strip()
newsfrom = soup.select('#navtimeSource span a ')[0].text
news = ''.join([p.text.strip() for p in soup.select('#artibody p')[:-1]])
writer = soup.select('.article-editor')[0].text.strip('责任编辑：')

res_number = req.get('http://comment5.news.sina.com.cn/page/info?version=1&format=js&channel=gn&newsid=comos-fyetwsm1937707&group=&compress=0&ie=utf-8&oe=utf-8&page=1&page_size=20')
jd = json.loads(res_number.text.strip('var data ='))

print('评论数:',jd['result']['count']['total'])
print(tite,time,newsfrom)
print(news)
print('作者:',writer)
