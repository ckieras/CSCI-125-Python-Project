# CSCI-125-Python-Project
For Python Project
import urllib
txt = urllib.urlopen('http://www.ecfr.gov/cgi-bin/text-idx?rgn=div8&node=50:2.0.1.1.1.2.1.1').read()


from bs4 import BeautifulSoup

soup = BeautifulSoup(txt)
tbl = soup.find_all('table')[6]
for word in tbl:
  print (tbl.get_text())
