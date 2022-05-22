# SONNY_project
손흥민의 득점왕 기원을 위하여 제작한 토이 프로젝트
=============
(손흥민 스탯 분석, 시각화)<jupyter notebook, tableau>
'''
This is a code for cralwing
=============
'''
'''
from bs4 import BeautifulSoup
from selenium import webdriver
import pandas as pd 
import selenium
import requests
import csv
import time
import pandas as pd
'''
'''
driver = webdriver.Chrome()
driver.get('https://understat.com/player/453')
'''
'''
html = driver.page_source
soup = BeautifulSoup(html, 'html.parser')
data = soup.select("#stats_standard_dom_lg > tbody")
soccer_list = []

rows = data[0].findAll('tr')
for row in rows:
            th = row.findAll('th')
            tds = row.findAll('td')
            col0 = th[0].text
            col1 = tds[1].text
            col2 = tds[2].text
            col3 = tds[3].text
            col4 = tds[4].text   
            col5 = tds[11].text
            col6 = tds[10].text
          
            soccer_list.append([col0, col1, col2, col3, col4, col5, col6])
'''
df = pd.DataFrame(soccer_list, columns=['position','appearances','minutes','goals'])
df.to_csv('position_history.csv', index=False)
