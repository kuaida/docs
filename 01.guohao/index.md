### 5月22日工作内容

1. 主持小组完成项目页面设计草图
1. 主持小组完成数据库设计草图
1. 完成数据库设计

[数据库设计文档](./数据库设计.md)


### 5月25日 数据库修改内容:

1. 修改 answerSchema 中 点在数量 likeNumber String ,更改为: 点赞者  likers []
1. 更新集合间引用关系:
* userSchema
  * myCollections:[{type:'ObjectId',ref:'question'}]
  * myQuestions:[{type:'ObjectId',ref:'question'}]
  * myAnswers:[{type:'ObjectId',ref:'question'}]
* questionSchema
  * author:{type:'ObjectId',ref:'user'}
  * answerList:[{type:'ObjectId',ref:'question'}]
* answerSchema
  * question:{type:'ObjectId',ref:'question'}
  * author:{type:'ObjectId',ref:'user'}
* typeSchema
  * questionIdList:[{type:'ObjectId',ref:'question'}]
  
  ### 5月26日工作内容
  
 1. 给数据库增添默认值
 1. 用户数据集合增加新字段：
  * 获得奖金总数   totalReward   {type：Number,default:0}
