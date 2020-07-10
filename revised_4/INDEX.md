2.4.6 懒加载部分代码

`getNetworkData` 方法增加 `Future<String>` 的声明，`Text`使用 `data.data` 。



```
class SampleFutureBuilder extends StatelessWidget {
  Future<String> getNetworkData() async {
    await Future.delayed(Duration(seconds: 10));
    return "result";
  }

  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
        future: getNetworkData(),
        initialData: "init",
        builder: (BuildContext context, AsyncSnapshot<String> data) {
          return Container(
            child: new Text(data.data ?? "loading"),
          );
        });
  }
}

```


