清纯校花真空去上学的小说晓雪是a市某中学的英语老师

cudaError_t cudaStreamCreate(cudaStream_t*);
cudaError_t cudaStreamDestroy(cudaStream_t);


cudaStream_t stream_1;
cudaStreamCreate(&stream_1); // 注意要传流的地址
cudaStreamDestroy(stream_1);

为了检查一个 CUDA 流中的所有操作是否都在设备中执行完毕，CUDA 运行时 API 提
供了如下两个函数：

cudaError_t cudaStreamSynchronize(cudaStream_t stream);
cudaError_t cudaStreamQuery(cudaStream_t stream);

函数 cudaStreamSynchronize 会强制阻塞主机，直到 CUDA 流 stream 中的所有操作都执行完毕。函数 cudaStreamQuery 不会阻塞主机，只是检查 CUDA 流 stream 中的所有操作是否都执行完毕。若是，返回 cudaSuccess，否则返回 cudaErrorNotReady。
2 在默认流中重叠主机和设备计算

虽然同一个 CUDA 流中的所有 CUDA 操作都是顺序执行的，但依然可以在默认流中
重叠主机和设备的计算。下面让我们通过数组相加的例子进行讨论。在数组相加的 CUDA 程序中与 CUDA 操作有关的语句如下：
