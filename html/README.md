### new FormData对象console输出为空
网络上查询获取到的资料，结果如下，
---
> 想要从一个formData里取数据，直接
  console.log(form);
  是看不到的因为formData里的数据是一类似于私有属性的方式储存，必要要通过
  console.log(form.get(key));
  get方法传递key，才能返回value，formData
  
 个人认为FormData对象为懒加载，只有使用get或getAll方法获取某个name的值时，才真正的去解析FormHtmlElement对象。以上有待进一步验证！
