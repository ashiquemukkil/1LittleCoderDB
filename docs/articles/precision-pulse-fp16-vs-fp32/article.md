#Precision Pulse FP16 vs FP32 

###Introduction:

When its come to Large language models(LLMs) like GPT4,LLaMA,..), choice of data type can significantly impact on memory usage and training speed,
Utilise standard FP32(32 bit floating point) on LLM model like 7 Billion parameter LLaMA will be memory-intensive consume as much as 28 gigabytes of RAM. Furthermore the gradient and optimiser will take almost 3 time of model size memory which will posing challenges for hardware and out of memory error.
In low precision data type, specifically Float16 and bFloat16 ,these are alternative data type which need half of memory(16 bits) and offer memory bottleneck associate which FP32,However right selection of data type will be a trade-off between memory usage and model training effectiveness

##What is FP32

