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
t#The following closes a file in your notebook
outf.close()

raw= str(txt)

from bs4 import BeautifulSoup

soup = BeautifulSoup(open('ecfr.txt','r'))
tbl = (soup.find_all('table')[6])
for word in tbl:
     newtext=word.get_text()


ecount=0
tcount=0

for tr in tbl.find_all('tr')[2:]:
    #print tr
    for td in tr:
        tds = tr.find_all('td')
t        (tds[0].text).encode('utf-8') 
        (tds[1].text).encode('utf-8') 
        (tds[2].text).encode('utf-8') 
        (tds[3].text).encode('utf-8')
        (tds[4].text).encode('utf-8')
        if tds[3].text=="E":
            ecount=ecount+1
        elif tds[3].text=="T":
            tcount=tcount+1
    print ecount, tcount
u    
#The below is still very buggy

def ecounts():
    ecount=0
    for tr in tbl.find_all('tr')[2:]:
        #print tr
        for td in tr:
            tds = tr.find_all('td')
            (tds[0].text).encode('utf-8') 
b            (tds[1].text).encode('utf-8') 
            (tds[2].text).encode('utf-8') 
            (tds[3].text).encode('utf-8')
            (tds[4].text).encode('utf-8')
            try:
                if tds[3].text=="E":
                    ecount=ecount+1
                elif tds[3].text=="T":
                    pass
                else:
                     continue
            except:
                continue
        #print ecount
        return ecount
def tcounts():
    tcount=0
    for tr in tbl.find_all('tr')[2:]:

#tcount=0
,        #print tr
        for td in tr:
            tds = tr.find_all('td')
            (tds[0].text).encode('utf-8') 
            (tds[1].text).encode('utf-8') 
            (tds[2].text).encode('utf-8') 
            (tds[3].text).encode('utf-8')
            (tds[4].text).encode('utf-8')
            try:
                if tds[3].text=="T":
                    tcount=tcount+1
                    print tcount
                elif tds[3].text=="E":
                    pass
                else:
                    continue
            except:
                continue
        #print tcount
        return tcount
e=ecounts()
t=tcounts()
print e
print t


#Have also tried this and we want the return to be tabbed one less time but the error is that list index is out of range but I think we have the best chance with this one

def ecounttcount():
    ecount=0
    tcount=0
    for tr in tbl.find_all('tr')[2:]:
    #print tr
        for td in tr:
            tds = tr.find_all('td')
            (tds[0].text).encode('utf-8') 
            (tds[1].text).encode('utf-8') 
            (tds[2].text).encode('utf-8') 
            (tds[3].text).encode('utf-8')
            (tds[4].text).encode('utf-8')
            if tds[3].text=="E":
                ecount=ecount+1
            elif tds[3].text=="T":
                tcount=tcount+1
            else:
                continue
    return ecount, tcount

endthr=ecounttcount()
print endthr
