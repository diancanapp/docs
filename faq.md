# FAQ

Q: IsPromote是否活动中，如何计算值？
A: IsPromote表示商品是否活动中，只有为true时，才会去检查活动起止时间，为false时，表示没有活动。

Q：有些接口是管理后台用的，有些是小程序用的，管理后台适用JWT鉴权，小程序适用Token(基于SessionKey)鉴权，管理后台和小程序都要使用的接口，如何处理比较好？
A：