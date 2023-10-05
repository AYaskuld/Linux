## Process monitoring

### Task list

**top** - view a dynamically updating list of running processes

Example:
```bash
$ top
```
<img src="https://elearn.epam.com/assets/courseware/v1/de6d3c209e851b49fd7581c8650487bb/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/top.png">

### View processes

**ps** - view a list of running processes

Example:
```bash
$ ps aux
```
<img src ="https://elearn.epam.com/assets/courseware/v1/77362c759f26b390bca34869e4122276/asset-v1:RD_CIS+DOBCLinux+0422+type@asset+block/ps.png">

### Kill processes

**kill** - allow to stop or terminate running process

Example:
```bash
$ kill 156
$ kill -9 156 

#killall – kill processes by name
#Example
$ killall top
$ killall -9 top 
$ killall –KILL top
```
