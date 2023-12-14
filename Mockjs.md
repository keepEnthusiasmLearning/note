# Mockjs

Description: 生成随机数据，拦截 Ajax 请求

**Start**

    $ npm install mockjs

    var Mock = require('mockjs')
    var data = Mock.mock({
        // 属性 list 的值是一个数组，其中含有 1 到 10 个元素
        'list|1-10': [{
            // 属性 id 是一个自增数，起始值为 1，每次增 1
            'id|+1': 1
        }]
    })
    // 输出结果
    console.log(JSON.stringify(data, null, 4))




    'name|rule': value

- 属性名
- 生成规则 rule
    + min-max
    + count - 重复次数
    + min-max.dmin-dmax
    + min-max.dcount
    + count.dmin-dmax
    + count.dcount
    + +step - 属性值自动 +n
- 属性值
    + @ 占位符


