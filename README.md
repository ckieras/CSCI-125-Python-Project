# CSCI-125-Python-Project
For Python Project
import urllib
txt = urllib.urlopen('http://www.ecfr.gov/cgi-bin/text-idx?rgn=div8&node=50:2.0.1.1.1.2.1.1').read()


from bs4 import BeautifulSoup

soup = BeautifulSoup(txt)
tbl = soup.find_all('table')[6]
for word in tbl:
  print (tbl.get_text())

ecount=0
tcount=0

for tr in tbl.find_all('tr')[2:]:
    #print tr
    for td in tr:
        tds = tr.find_all('td')
        print (tds[0].text, tds[1].text, tds[2].text, tds[3].text, tds[4].text)
        print tds[3].text
        if tds[3].text=="E":
            ecount=ecount+1
        elif tds[3].text=="T":
            tcount=tcount+1
    print ecount, tcount
