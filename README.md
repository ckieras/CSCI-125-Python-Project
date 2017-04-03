
#Team ACED: Emily Frances Leiter Olson, Alexandra Rae Rosatti, Corinne Kieras, Daisy Richmond
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
#scrapes the text on the table from the website and puts it into a workable format
soup = BeautifulSoup(open('ecfr.txt','r'))
tbl = (soup.find_all('table')[6])
for word in tbl:
    newtext=(word.get_text()).encode('utf-8')
print newtext
newtext1=str(newtext)
newtext3 = newtext1.split(' ')
newtext4 = ''.join(newtext3)
#this function counts the number of endangered species and threatened ones and returns the total
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


###This makes the dictionary
newtext5 = newtext1.split('.')
newtext6 = ' '.join(newtext5)
newtext7 = newtext6.split(' ')
d=dict()
for a in range(len(newtext7)):
    if newtext7[a]=='FR':
        key=newtext7[a+1]        key=key.split(",")[0]
        key=key.split(";")[0]
        value=newtext7[a+2]
        value=value.split(";")[0] #Kicks out extra characters at end of date
        d[key]=value
    else:
        continue   
#scrapes the information at the bottom and puts it into a consistent date format
extratable=soup.find_all('p')[-2]
extratable1=(extratable.get_text()).encode('utf-8')
newextra=extratable1.replace('Aug. 4, 2016','8/4/2016')
newextra1=newextra.replace(', as amended at ','; ')
newextra2=newextra1.replace('Aug. 12, 2016','8/12/2016')
newextra3=newextra2.replace('Aug. 26, 2016','8/26/2016')
newextra4=newextra3.replace('Sept. 12, 2016','9/12/2016')
newextra5=newextra4.replace('Sept. 22, 2016','9/22/2016')
newextra6=newextra5.replace('Sept. 30, 2016','9/30/2016')
newextra7=newextra6.replace('Oct. 5, 2016','10/5/2016')
newextra8=newextra7.replace('Oct. 6, 2016','10/6/2016')newextra9=newextra8.replace('Nov. 2, 2016','11/2/2016')
newextra10=newextra9.replace('Dec. 21, 2016','12/21/2016')
extra=newextra10.replace('Jan 11, 2017]','1/11/2017')
extra1=extra.replace('67214, 67856, 9/30/2016','67214, 9/30/2016; 81 FR 67856, 9/30/2016')
finalextra=extra1.replace('68984, 69002, 10/5/2016','68984, 10/5/2016; 81 FR 69002, 10/5/2016')
extratable2=finalextra.split('; ')
#this adds the information at the bottom of the table to the dictionary
for item in extratable2:
    for b in range(len(item)):
        if item[b]=='F' and item[b+1]=='R':
            thing=item[b+3:]
            
            for w in range(len(thing)):
             
               if thing[w]==',' and thing[w+3]=='/':
                    
                  key1=thing[0:w-1]
                  value1=thing[w+2:]
                  d[key1]=value1
               elif thing[w]==',' and thing[w+2]=='1' and thing[w+3]=='0':
                   key2=thing[0:w]
                    
                   value2=thing[w+2:]
                   d[key2]=value2
               elif thing[w]==',' and thing[w+2]=='1' and thing[w+3]=='1':
                   key3=thing[0:w]
                    
                   value3=thing[w+2:]
                    
                   d[key3]=value3
               elif thing[w]==',' and thing[w+2]=='1' and thing[w+3]=='2':
                   key4=thing[0:w]
                    
                   value4=thing[w+2:]
                   d[key4]=value4
               else:
                   continue 
print d


#exemplary status
#We decided that in order to fully utilize the dictionary we would create a code
#that allows one to search for the FR number and then recieve the corresponding date
#If the FR number the user enters is not in the dictionary the user will
#be able to search for another one or exit the program if they do not wish to 
#continue searching by typing in 'done'.
searchkey = raw_input("What FR value do you want to search the dictionary for? ")
for key in d:
    if searchkey in d:
        print d[searchkey]
        break
    if searchkey!=key:
        newsearchkey = raw_input('Sorry the key '+searchkey+' does not exist. Try a different one or enter done to quit:')
        if newsearchkey in d:
            print d[newsearchkey]
            break
        elif newsearchkey == 'done':
            break
        else:
            continue


#Question 7
i=0
lennewtext10=len(newtext10)
while i<lennewtext10:
    #print i, newtext10[i]
    if newtext10[i]=='FR':
        newtext10.remove(newtext10[i+1])
        newtext10.remove(newtext10[i])
        lennewtext10=lennewtext10-2
        #i=i+1
    else:
        i=i+1
        continue
print newtext10

###Question 8:
#This part is finding the most recent year
yearlist=d.values()
mashedup='/'.join(yearlist)
splityears=mashedup.split("/")
#print splityears
year=2018
while True:
    if str(year) in splityears:
        trueyear=year
        print "A species was most recently added to the list in: "+str(year)
        break
    else: 
        year=year-1
        #print "Subtracting one"
        continue
#Now grabbing the exact dictionary value
for item in d.values():
    if str(trueyear) in item:
        truedate=item
        print "The date this species was added is: "+str(item)
        break
    else:
        continue
emptylist=[]
indexofdate=newtext4.find(str(truedate))
#print indexofdate
for i in range(37,60):
    emptylist.extend(newtext4[indexofdate-i])
emptylist.reverse()
animalstring=''.join(emptylist)

print "The most recently added species is :"+ str(animalstring)



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
#imports the new information from the new website and puts it into a workable format
from bs4 import BeautifulSoup
soup = BeautifulSoup(open('mwl.txt','r'))
tbl = (soup.find_all('table')[0])
newtext = tbl.get_text()
newtext1= newtext.encode('utf-8')
newtext2=str(newtext1)
newtext5 = newtext2.replace('\n',' ')
newtext3 = newtext5.split(' ')
newtext4 = ''.join(newtext3)
#this function adds up the endangered and threatened species from the Minnesota website and prints the totals
def endthr():
    endangered = 0
    threatened = 0

    for letter in newtext4:
       for i in range(len(newtext4)):
           if newtext4[i] == 'E'and newtext4[i+1] == 'n'and newtext4[i+2] == 'd'and newtext4[i+3] == 'a' and newtext4[i+4] == 'n' and newtext4[i+5] == 'g' and newtext4[i+6] == 'e' and newtext4[i+7] == 'r' :
                endangered = endangered + 1
           elif newtext4[i] == 'T' and newtext4[i+1] == 'h'and newtext4[i+2] == 'r' and newtext4[i+3] == 'e'and newtext4[i+4] == 'a'and newtext4[i+5] == 't':
                threatened = threatened + 1
       return str(endangered-6)+'\t'+'\t' + '\t'+str(threatened-1)

endangeredthreatened = endthr()
print 'Endangered ' + 'Threatened'
print endangeredthreatened

