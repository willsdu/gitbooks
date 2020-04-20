# mongo查询介绍

mongo查询现在没有工单系统接入，生产的查询还是需要给DBA提供语句，由DBA帮助执行

生产的环境是`offline.haproxy.gaodunwangxiao.com:3717/gaodun_tag` 。

## 查询大一大二等标签人数

查询某个时间范围内大一和大二标签人数，可以使用mongo查询语句

```js
db.getCollection('user_tag').aggregate([
    { $match: { "tags": { "$elemMatch": { "_id": ObjectId("5d7f349844defe8f7fb87f21") } } } },
    { $match: { "tags": { "$elemMatch": { "create_time": { "$lte": new Date(2019, 01, 01) } } } } },
    { $unwind: "$tags" },
    { $match: { "tags._id": ObjectId("5d7f349844defe8f7fb87f21") } },
    { $match: { "tags.create_time": { "$lte": new Date(2020, 01, 01) } } },
    { $unwind: "$tags.tag_val" },
    { $project: { "_id": 1, "user_id": 1, "tag_val": "$tags.tag_val" } },
    { $group: { _id: "$tag_val", "total": { $sum: 1 } } }
])
```

也可以使用js语句

```js
var url = "t.mongo.gaodunwangxiao.com:27017/gaodun_tag";
var db = connect(url);

var tagsMap = new Map();
tagsMap["5d830fe2c03ff53339c48098"] = "大一"
tagsMap["5d830fe2c03ff53339c48099"] = "大二"
tagsMap["5d830fe2c03ff53339c4809a"] = "大三"
tagsMap["5d830fe2c03ff53339c4809b"] = "大四"
tagsMap["5a3b113d5ab29c1b04e36cac"] = "在校生"

db.getCollection('user_tag').find({})

var curse = db.getCollection('user_tag').find({
    "tags": { "$elemMatch": { "_id": ObjectId("5d7f349844defe8f7fb87f21") } }
});
while (curse.hasNext()) {
    var data = curse.next()
    var str = data.user_id;
    var tags = data.tags
    for (var i = 0; i < tags.length; i++) {
        var tag = tags[i]
        var sid = tag._id.valueOf()
        if (sid == "5d7f349844defe8f7fb87f21") {
            for (var j = 0; j < tag.tag_val.length; j++) {
                if(tag.create_time)
                var tid = tag.tag_val[j].valueOf()
                    str = str + "," + tid
            }
        }
    }
    print(str)
}
```



## 查询三种职业的人数





