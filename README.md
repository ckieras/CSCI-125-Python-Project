# CSCI-125-Python-Project
For Python Project
import urllib
txt = urllib.urlopen('http://www.stolaf.edu/people/olaf/cs125/43rd.txt').read()
outf = open('43rd-congress.html', 'w')
outf.write(txt)
outf.close()

txt2 = urllib.urlopen('http://www.stolaf.edu/people/olaf/cs125/43rd.full.txt').read()
outf2 = open('43rd-congress.full.html', 'w')
outf2.write(txt)
outf2.close()

from bs4 import BeautifulSoup

soup = BeautifulSoup (open("43rd-congress.html"))

final_link = soup.p.a
final_link.decompose()

print soup.find_all('tr')[2].find_all('td')[5].get_text()[2:]
