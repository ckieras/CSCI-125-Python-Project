## CSCI-125-Python-Project
For Python Project
# urllib helps us save from URLs
import urllib 
#The following reads from a URL
txt = urllib.urlopen('http://www.ecfr.gov/cgi-bin/text-idx?rgn=div8&node=50:2.0.1.1.1.2.1.1').read()
#The following creates a new local file in your notebook
outf = open('ecfr.txt', 'w')
#The following writes to a file in your notebook
outf.write(txt)
#The following closes a file in your notebook
outf.close()

raw= str(txt)
from bs4 import BeautifulSoup

soup = BeautifulSoup(open('ecfr.txt','r'))
tbl = (soup.find_all('table')[6])
for word in tbl:
    newtext=(word.get_text()).encode('utf-8')
    newtext1=str(newtext)
    ' '.join(newtext1)
    for word in newtext1:
        #i=0
        ecount=0
        a=0
        #tcount=0
        for i in word:
            #print i
            if i[a]=="E" and i[a+1].isdigit():
                print "yes"
            else:
                continue
             #   ecount=ecount+1
        #print ecount
              #  i=i+1
               # continue
            #elif word[i]=="T" and word[i+1].isdigit():
             #   tcount=tcount+1
              #  i=i+1
               # continue
           # else:
            #    i=i+1
             #   continue
        #print ecount
        #print tcount




