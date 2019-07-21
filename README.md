# hello-world
firstDemo
public static void mainp
					kafka

由于Kafka采用解耦的设计思想，并非原始的发布订阅,即生产者负责产生消息，直接推送给消费者。而是在中间加入持久化层——broker,生产者把数据存放在broker中，消费者从broker中取数据。这样就带来了几个好处:

1 生产者的负载与消费者的负载解耦
2 消费者按照自己的能力fetch数据
3 消费者可以自定义消费的数量
另外，由于broker采用了主题topic-->分区的思想，使得某个分区内部的顺序可以保证有序性，但是分区间的数据不保证有序性。这样，消费者可以以分区为单位，自定义读取的位置——offset。

Kafka采用zookeeper作为管理，记录了producer到broker的信息，以及consumer与broker中partition的对应关系。因此，生产者可以直接把数据传递给broker，broker通过zookeeper进行leader-->followers的选举管理；消费者通过zookeeper保存读取的位置offset以及读取的topic的partition分区信息。


1.发起请求的常用工具是 HttpClient 
- HttpClient 是早期 Apache 开源的 Http 客户端
- HttpClient 是一个 Java 客户端库
- HttpClient 调用方式比较繁琐, 性能也相对较差, 且在多线程下有安全问题
可以用OkHttp来替换:
用法:
object OkHttpTest {
  def main(args: Array[String]): Unit = {
    val url = "https://restapi.amap.com/v3/geocode/regeo?" +
      "location=116.310003,39.991957" +
      "&key=ef752cf28705a5f3f1e95f4b1158a7a1"
    //1.client
    val client = new OkHttpClient()
	
    //2.get
    val request: Request = new Request.Builder()
      .url(url)
      .get()
      .build()
	  
    //3.excute
    val response: Response = client.newCall(request).execute()

    //print response
    if (response.isSuccessful) {
      println(response.body().string())
    }

  }
}
