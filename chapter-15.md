# Chapter 15

Q: message queue里存的是整个视频的copy还是meta？为什么说中间加queue的方式费storage?

A: 保存一个文件的地址就行



Q: do all chunks have same resolution of the video? if so, why chunk table needs resolution?

A: 一个视频分成多个块。一个视频下的所有块的分辨率一样，但是视频可以有不同分辨率



Q: 如果一个视频会被100个人在看，一些人才开始看，一些人都快看完了，视频是要做成100个copy呢，还是有什么处理方式

A: 这个是几个人看没有一点关系。看到哪里读取对应进度的数据就行。文件系统支持 fseek操作



Q: 带宽会影响什么？会影响rpc通信的效率？

A: 带宽 有速度和延迟两个概念。不满足就会影响



Q: 请问如何判断是重复视频呢？

AL: md5码





