# getListenPorts
## Installation
Clone this repository
```
git clone https://github.com/seevenup83/getRemoteListenPorts
```

## Configuration
### serverList
Copy a csv based list with servernames to the cloned directory and name it: **serverList**
you can have a look at the existent serverList

**IMPORTANT** if the server is not the first field in the list, you have to change this in the script **getRemoteListenPorts** like this:

Example1: Server is in field 1
```
serverList=$(cat ./serverList | cut -d ';' -f1)
```
Example2: Server is in field 5
```
serverList=$(cat ./serverList | cut -d ';' -f5)
```

### password
To prevent user input on scp and ssh user the file: **password**


### getListenPorts
If you want to change the command to find out what ports are LISTEN or filter out more or less, change this line in the script: **getListenPorts**
```
netstat -tulpn 2>/dev/null | grep LISTEN | grep -v "::" | grep -v "127.0." | cut -d : -f2 | cut -d ' ' -f1
```

## Usage
To get all the LISTEN ports based on **serverList** just run the fallowing command on a server that has access to all servers
```
./getRemoteListenPorts
```

to print the findings in a csv-list, you can add >> 
```
./getRemoteListenPorts >> exportListenPorts.csv
```