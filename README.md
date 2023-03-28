<p align="right"><img src="https://github.com/isc-at/CPIPE/blob/master/archived.jpg"/></p>

## The Idea  
The similarity between JSON objects + arrays and Globals in IRIS or Caché is evident.    
With small and medium size JSON objects navigation across %Dynamic Objects is comfortable.  
But with **large** and/or deep cascaded objects it becomes a challenge.   

The presented tool offers 3 variants   
- loading an already existing %Dynamic Object or Array into a global of your choice   
- loading a %Stream containing a JSON object into a global of your choice   
- loading an external File containing a JSON object into a global of your choice   

### How to use it
```
UESR>read str
{"id":306904,"last_star_ts":0,"completion_day_level":{},"global_score":0,"local_score":0,"stars":0,"name":"name_1"}
USER>set jsn={}.%FromJSON(str)
USER>write ##class(rcc.jstog).toglobal(jsn,"^jsn")
1
USER>zwrite ^jsn
^jsn("global_score")=0
^jsn("id")=306904
^jsn("last_star_ts")=0
^jsn("local_score")=0
^jsn("name")="name_1"
^jsn("stars")=0

USER>zzjson jsn
{
  "id":306904,
  "last_star_ts":0,
  "completion_day_level":{
  },
  "global_score":0,
  "local_score":0,
  "stars":0,
  "name":"name_1"
}
USER>
```
   from an already existing Stream it's like this    
```
USER>write ##class(rcc.jstog).stream(jsonstream,"^jsstr")
1
```
  and from file it is this method:
```
USER>set filename="/opt/irisbuild/src/data/big6.json"
USER>write ##class(rcc.jstog).file(filename)  ; using default global ^json
1
USER>
```
## How to Test it
log in to command line or use a terminal session     

2 test files are available   
- /opt/irisbuild/src/data/demo.json  ~1kB     
![](https://community.intersystems.com/sites/default/files/inline/images/demo.jpg)  
- /opt/irisbuild/src/data/big6.json  ~6GB 
![](https://community.intersystems.com/sites/default/files/inline/images/big6.jpg)  
this file is composed from the anonymized results of AOC2022 contest  

```
USER>......< your choice  > ....."
USER>kill ^json ; using default global ^json  
USER>write ##class(rcc.jstog).file(filename)
1
USER ZWRITE ^json
```

[Article in DC](https://community.intersystems.com/post/jsonfile-global-1)   

[Video](https://youtu.be/rJ4hY7-5CRk)    
