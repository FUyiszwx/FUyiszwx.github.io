# Attention
Query, Key, Value的概念出自信息检索系统，例如，在搜索引擎上输入的内容为Q，引擎根据Q匹配的内容为K，根据两者相似度得到匹配的内容为V。
查询对象Q， 被查询对象V

计算Q和V中事物的重要性

重要性计算就是相似度计算

Q, $K= k_1, k_2,\cdots, k_n$ (k是将Values拆分成键值对)

利用点乘计算Q和K中每一个事物的相似度，就可以拿到Q和$k_i$的相似度$a_i$

做一层softmax($a_1, a_2,\cdots, a_n$)
![alt text](https://imgmd.oss-cn-shanghai.aliyuncs.com/BERT_IMG/attention-%E8%AE%A1%E7%AE%97%E5%9B%BE.png)