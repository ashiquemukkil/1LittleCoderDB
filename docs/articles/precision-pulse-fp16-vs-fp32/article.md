#Precision Pulse FP16 vs FP32 

###Introduction:

When its come to Large language models(LLMs) like GPT4,LLaMA,..), choice of data type can significantly impact on memory usage and training speed,
Utilise standard FP32(32 bit floating point) on LLM model like 7 Billion parameter LLaMA will be memory-intensive consume as much as 28 gigabytes of RAM. Furthermore the gradient and optimiser will take almost 3 time of model size memory which will posing challenges for hardware and out of memory error.
In low precision data type, specifically Float16 and bFloat16 ,these are alternative data type which need half of memory(16 bits) and offer memory bottleneck associate which FP32,However right selection of data type will be a trade-off between memory usage and model training effectiveness

## FP32

![fp32](https://raw.githubusercontent.com/ashiquemukkil/1LittleCoderDB/bb1f424ddb17565e22d30e27f1759ff07fedf11a/docs/imges/precision-pulse-fp16-vs-fp32/fp32.png){:height="70%" width="70%"}

FP32 is a widely supported and standard data format in most of the computing environments and hardwares, It is the default data type for representing real numbers in many programming languages, libraries, and frameworks. traditionally model weights are represented by FP32.

* 32 bits (4 byte) of memory representation  
* All most all modern CPUs and GPUs are support natively 
* It have enough range to represent numbers of magnitude from 10<sup>-45</sup> to 10<sup>38</sup>
* High precision, allowing to represent and perform calculations with a wide range of real numbers accurately

LLaMA 7B model weight FP32 representation take 28 gigabytes of memory _7B*4bytes_ (32 bits = 4bytes)

## FP16 and bFP16

![fp16](https://raw.githubusercontent.com/ashiquemukkil/1LittleCoderDB/bb1f424ddb17565e22d30e27f1759ff07fedf11a/docs/imges/precision-pulse-fp16-vs-fp32/fp16.png){:height="70%" width="70%"}


