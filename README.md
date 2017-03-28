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
            if newtext4[i] == 'E'and newtext4[i+1].isdigit():
                ecount = ecount+1
            
            elif newtext4[i] == 'T' and newtext4[i+1].isdigit():
                tcount = tcount+1
        return str(ecount)+'\t'+'\t'+str(tcount)


endthr=et()
print 'Endangered'+'\t'+'Threatened'
print endthr

#ABOVE IS CORRECT DON'T DELETE


#This makes the dictionary not including the stuff at the bottom
newtext5 = newtext1.split('.')
newtext6 = ' '.join(newtext5)
newtext7 = newtext6.split(' ')
#print newtext7
d=dict()
for a in range(len(newtext7)):
    if newtext7[a]=='FR':
        key=newtext7[a+1]
        key=key.split(",")[0]
        key=key.split(";")[0]
        #print key
        value=newtext7[a+2]
        value=value.split(";")[0] #Kicks out extra characters at end of date
        #print value
        d[key]=value
    else:
        continue
print d
        
