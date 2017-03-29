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

extratable=soup.find_all('p')[-2]
extratable1=(extratable.get_text()).encode('utf-8')
print extratable1
#print extratable1
extratable2=extratable1.split('; ')
#print extratable2
for item in extratable2:
    for b in range(len(item)):
        if item[b]=='F' and item[b+1]=='R':
            thing=item[b+3:]
            print thing

#Question 7
for word in newtext:
    newtext8=newtext.replace("FR", " ")
    print newtext8
#not done yet but this gets rid of FR in the table

####FOR QUESTION #9
   import urllib
#The following reads from a URL
txt = urllib.urlopen('https://www.fws.gov/midwest/endangered/lists/minnesot-spp.html').read()
#The following creates a new local file in your notebook
outf = open('mwl.txt', 'w')
#The following writes to a file in your notebook
outf.write(txt)
#The following closes a file in your notebook
outf.close()

from bs4 import BeautifulSoup
soup = BeautifulSoup(open('mwl.txt','r'))
tbl = (soup.find_all('table')[0])
newtext = tbl.get_text()
newtext1= newtext.encode('utf-8')
newtext2=str(newtext1)
newtext5 = newtext2.replace('\n',' ')
newtext3 = newtext5.split(' ')
newtext4 = ''.join(newtext3)

def endthr():
    endangered = 0
    threatened = 0

    for letter in newtext4:
       for i in range(len(newtext4)):
           if newtext4[i] == 'E'and newtext4[i+1] == 'n'and newtext4[i+2] == 'd'and newtext4[i+3] == 'a' and newtext4[i+4] == 'n' and newtext4[i+5] == 'g' and newtext4[i+6] == 'e' and newtext4[i+7] == 'r' :
                endangered = endangered + 1
           elif newtext4[i] == 'T' and newtext4[i+1] == 'h'and newtext4[i+2] == 'r' and newtext4[i+3] == 'e'and newtext4[i+4] == 'a'and newtext4[i+5] == 't':
                threatened = threatened + 1
       return str(endangered-6)+'\t'+'\t'+str(threatened-1)

endangeredthreatened = endthr()
print 'Endangered' + '\t' + 'Threatened'
print endangeredthreatened

