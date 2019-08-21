# Sorting-files-with-size
### Python - This python code is written to sort the files based on size and print 5 number of files which is larger in size. 
### I have used module argparse and created switches like "-l" for location and "-f" for file format. 
### By default this code will print the files larger in size from the current working directory. 
### I have configured the switches so that you can specify the location and also the file format. 

```python
import argparse
import os


parser = argparse.ArgumentParser()

parser.add_argument('-l',
                    dest='location',
                    help='Path to check the size',
                    default = os.getcwd())

parser.add_argument('-f',
                    dest='format',
                    help='Type of file you want to check',
                    default = 'null')


arguments = parser.parse_args()

result = {}

location = arguments.location
fileformat = arguments.format


for item in os.walk(location):
   
    curDir,subDirs,subFiles = item
    
    if fileformat == 'null':
        
        try:
    
            for subFile in subFiles:
      
                absPath = os.path.join(curDir,subFile)
      
                size = os.path.getsize(absPath)
      
                result[absPath] = size
        except:
            
                result[absPath] = 0
        
    else:
        
        for subFile in subFiles:
            
            if subFile.endswith(fileformat):
                
                try:
      
                  absPath = os.path.join(curDir,subFile)
      
                  size = os.path.getsize(absPath)
      
                  result[absPath] = size
        
                except:
                
                    result[absPath] = 0
        
def getfilesize(item):
  return item[1]

for x in sorted(result.items(),key=getfilesize,reverse=True)[:5]:
    print(x)
```

## The output of the code wll looks like as follows


- arjunm@ubuntu:~$ python3 finalcode.py -l /home/arjunm/Downloads/ -f txt
-('/home/arjunm/Downloads/serverload.txt', 11812)
-('/home/arjunm/Downloads/Downloads/Non ho potuto resistere e passare!.txt', 11619)
-('/home/arjunm/Downloads/Downloads/cooperazione con una compagnia internazionale.txt', 5195)
-('/home/arjunm/Downloads/Downloads/Volevano manichini di denaro.txt', 4410)
-('/home/arjunm/Downloads/Downloads/Interview task list.txt', 1555)
