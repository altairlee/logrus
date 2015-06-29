## logrus
----


### example

```
package main

import (
	log "github.com/gogap/logrus"
	"github.com/gogap/logrus/hooks/file"
	"github.com/gogap/logrus/hooks/graylog"
)

func main() {
	log.SetFormatter(&log.JSONFormatter{})

	//输出到graylog
	glog, err := graylog.NewHook("boot2docker:9001", "yijifu", nil)
	if err != nil {
		log.Error(err)
		return
	}
	log.AddHook(glog)

	//输出到文件
	log.AddHook(file.NewHook("logs/ss.log"))
	
	//yijifu组件中的member模块的日志
	log.WithField("biz", "member").Errorf("member not login,member is %s", "1001")
}


```

## log in file example

```
2015/06/29 15:24:52 [ERROR] member not login,member is 1001
git.rd.rijin.com/yanglong/test_case/logrus.go:23[biz:membe]

```

## log on gray log example
![picture](https://cloud.githubusercontent.com/assets/2741940/8403073/ede3e688-1e73-11e5-864c-ac901d86263a.png)