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
        
        
        
  #what I have is really close it just needs to count up everytime properly but it is pulling the correct E's and T's

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
#newtext2 = newtext1.spilt('T')
newtext3 = newtext1.split(' ')
newtext4 = ''.join(newtext3)
#newtext5 = list(newtext4)
def et():
    ecount = 0
    tcount = 0
    for letter in newtext4:
        for i in range(len(newtext4)):
            if newtext[i] == 'E'and newtext[i+1].isdigit():
                ecount = ecount+1
            print ecount
            elif newtext[i] == 'T' and newtext[i+1].isdigit():
                tcount = tcount+1
            print tcount








