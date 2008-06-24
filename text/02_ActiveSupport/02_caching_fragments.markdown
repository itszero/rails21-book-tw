## Fragment\_exist?

在 **cache\_store** 中新增加了兩個方法： **fragment\_exist?** 和 **exist?** 。

**fragment\_exist?** 顧名思義，它將檢查一個由 key 指定的緩衝區片段存不存在。這個方法將可以用來替代常用的：
  
    read_fragment(path).nil?

**exist?** 方法被實際的加入到 **cache\_store**，而 **fragement\_exist?** 則是一個您能夠在 Controller 中使用的 helper。
