书中142页：

> “在 Android 和 iOS 上，Flutter Engine 会为 UI Task Runner、GPU Task Runner 和 I/O Task Runner 各自创建一个独立的线程，而所有 Engine 实例会共享同一个 Platform Task Runner 线程，对于平台而言，Platform Task Runner 就是平台的主线程，Fuchsia 和 Web 不一样”  

而在139页：

> Flutter Engine 自己并不创建和管理线程，线程的创建和管理是由 Embedder 层负责。

这里同样是主体对象没区分开导致，其实大多数时候我们讨论 Engine 都会默认把 Engine 和 Embedder 作为一个底层整体：

- 139页开篇时是把整个 Flutter Framework 拆分为多层解释，单独把 Skia 所在的 C++ 层作为 Engine 来理解，是为了更好的介绍 Flutter 内的分层结构；
- 142页其实是已经把整个 Engine(C++) 和 Embedder 作为一个整体 Engine 对待，所以这里产生了歧义。


考虑到这个歧义，在 142 页这里应该可以把 Engine 去掉，并且把创建改为分配更恰当：

 > “在 Android 和 iOS 上，Flutter 会为 UI Task Runner、GPU Task Runner 和 I/O Task Runner 各自分配一个独立的线程，而所有 Engine 实例会共享同一个 Platform Task Runner，对于平台而言，Platform Task Runner 就是平台的主线程，Fuchsia 和 Web 不一样”  

是的，在 Flutter 中可以创建多个 Engine。

另外文章的后面也介绍了，Runner 和线程没有绝对关系，只是 Android 和 iOS 平台上的默认行为是为这四个默认 Runner 各自分配了一个独立线程，所以结合起来理解应该不会有太大问题。

> ps: 1.17 版本开始，底层绘制上 Android 可能会用到 Vulkan，而 iOS 可能会是 Metal，这主要和硬件还有系统版本有关系。
