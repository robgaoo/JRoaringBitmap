* [roaring](src%2Fmain%2Fjava%2Fcom%2Fliveramp%2Fts%2Froaring)目录下的代码是参考go源码实现的32位bitmap.
* 应为serialCookie的代码还没有写,所以当一个容器满了之后会报错。 64的部分和这里的代码完全没有关系, 因为后来发现32是兼容的，所以直接在32上套容器实现64位


* [roaring64](src%2Fmain%2Fjava%2Fcom%2Fliveramp%2Fts%2Froaring64) 则是在java32位类库上实现的64位bitmap. 
* Java的官方版本中, 也不完全兼容Go的版本,
  java在返回集合时用的是数组, 而数组的长度最多是 INT_MAX = 2^31 - 1,
  而go中bitmap的容量可以达到 2^32
* 官方版本在返回value是用的是int, 这样就会导致go中可以存下 value: 1<<32-1, 但是在java里读出来是-1,
  不过应该不影响比较操作(包含/Not/And/Or)
