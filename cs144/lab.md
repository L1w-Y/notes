## LAB 1

### 实验要求
lab0 实现的Bytestream双向字节流，作为传输通道
lab1主要是让我们实现一个streamReassemler类，也就是流重组器。

对于**TCP发送端**来说，在数据发送过程中，下层网络层对单个数据包有一个最大尺寸限制，叫做 MTU（最大传输单元）。
* 对于大多数以太网网络，MTU 大约是 1500 字节
* 但在 IP 层中，TCP 头占 20 字节，IP 头也占 20 字节
* 所以留给 TCP 有效负载（也就是实际要传的数据） 的空间最多是：1500 - 20 (IP) - 20 (TCP) = 1460 字节

所以在数据来到接收端的时候，会出现乱序、重复或部分丢失的问题，对于**TCP接收方**来说，就需要将这些 TCP 段重新组装成一个完整、有序的字节流，供上层应用读取。
这个streamReassemler用来实现这样的功能。

课程给的实验文档相当谜语人:
>>**What should the Reassembler store internally?**
>> The insert method informs the Reassembler about a new excerpt of the ByteStream, and where it fits in the overall stream (the index of the beginning of the substring)
>>
>> In principle, then, the Reassembler will have to handle three categories of knowledge:
>>1. Bytes that are the next bytes in the stream. The Reassembler should push these to the stream (output.writer()) as soon as they are known.
>>2. Bytes that fit within the stream’s available capacity but can’t yet be written, because earlier bytes remain unknown. These should be stored internally in the Reassembler.
>>3. Bytes that lie beyond the stream’s available capacity. These should be discarded. The Reassembler’s will not store any bytes that can’t be pushed to the ByteStream either immediately, or as soon as earlier bytes become known.
>>
>> The goal of this behavior is to limit the amount of memory used by the Reassembler and ByteStream, no matter how the incoming substrings arrive. We’ve illustrated this in the picture below. The “capacity” is an upper bound on both:
 >>1. The number of bytes buffered in the reassembled ByteStream (shown in green)
 >>2. The number of bytes that can be used by “unassembled” substrings (shown in red)

其实想表达的就是StreamReassembler需要处理三类数据
1. **可立即写入的字节**  
   这些是当前期望的下一个字节（ `_next_index`）。一旦收到，应立即通过 `ByteStream` 的 `writer()` 写入。

2. **尚未可写的字节**  
   这些字节的索引高于 `_next_index`，但低于 `_next_index + capacity`。由于前面的字节尚未到达，这些字节暂时无法写入，应在内部缓冲区中存储，待前面的字节到达后再写入。

3. **超出容量的字节**  
   这些字节的索引高于 `_next_index + capacity`。由于超出 `ByteStream` 的容量限制，应立即丢弃，不予存储。

看下面的图片：
![alt text](image.png)
紫色区域：ByteStream中整流完毕的数据，并且已经pop(上层应用读取)
绿色区域：存储在ByteStream已经整流但未被读取的数据，占用Bytestream容量
红色区域：存储在StreamReassembler中未整流的数据，占用StreamReassembler容量
### FAQs
* **ByteStream** 和 **StreamReassembler** 的总容量有固定的限制
* 
* 接收数据的每个字节都有自己唯一的索引，代表他在原始数据流中的位置
* Reassembler 类中，持有一个 ByteStream 实例，但只负责往里面 write() 字节，不需要（也不能）用它的读取接口，真正要读的是外部调用者（例如用户程序或 TCP 协议栈上层）
* 其实就是StreamReassembler接收数据流，比如已经收到了 [10-20],[25-30]，而ByteStream已经写入了排序好的[0-5]，这时候[5-15]的数据到来，那么应该排序[5-20]，之后应该立刻写ByteStream，给StreamReassembler释放空间，中间还涉及到重复数据和丢失数据的处理
