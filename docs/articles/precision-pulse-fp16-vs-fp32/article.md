#Precision Pulse FP16 vs FP32 

###Introduction:

When its come to Large language models(LLMs) like GPT4,LLaMA,..), choice of data type can significantly impact on memory usage and training speed,
Utilise standard FP32(32 bit floating point) on LLM model like 7 Billion parameter LLaMA will be memory-intensive consume as much as 28 gigabytes of RAM. Furthermore the gradient and optimiser will take almost 3 time of model size memory which will posing challenges for hardware and out of memory error.
In low precision data type, specifically Float16 and bFloat16 ,these are alternative data type which need half of memory(16 bits) and offer memory bottleneck associate which FP32,However right selection of data type will be a trade-off between memory usage and model training effectiveness

## FP32

| ![fp32](https://raw.githubusercontent.com/ashiquemukkil/1LittleCoderDB/bb1f424ddb17565e22d30e27f1759ff07fedf11a/docs/imges/precision-pulse-fp16-vs-fp32/fp32.png){:height="70%" width="70%"} |
|:--:| 
| *FP32* |

FP32 is a widely supported and standard data format in most of the computing environments and hardwares, It is the default data type for representing real numbers in many programming languages, libraries, and frameworks. traditionally model weights are represented by FP32.

* 32 bits (4 byte) of memory representation  
* All most all modern CPUs and GPUs are support natively 
* It have enough range to represent numbers of magnitude from 10<sup>-45</sup> to 10<sup>38</sup>
* High precision, allowing to represent and perform calculations with a wide range of real numbers accurately

LLaMA 7B model weight FP32 representation take 28 gigabytes of memory _7B*4bytes_ (32 bits = 4bytes)

## FP16 and bFP16

| ![fp16](https://raw.githubusercontent.com/ashiquemukkil/1LittleCoderDB/bb1f424ddb17565e22d30e27f1759ff07fedf11a/docs/imges/precision-pulse-fp16-vs-fp32/fp16.png){:height="70%" width="70%"} |
|:--:| 
| *FP16* |

FP16 is a 16 bits representation also know as half-precision floating point format which used in computing particularly deep-learning network

* 15<sup>nth</sup>bit represent sign (0 for positive and 1 for negative)
* 10 to 14 bit for exponent and 0 to 9 for fraction

| ![bfp16](https://raw.githubusercontent.com/ashiquemukkil/1LittleCoderDB/bb1f424ddb17565e22d30e27f1759ff07fedf11a/docs/imges/precision-pulse-fp16-vs-fp32/bfp16.png){:height="70%" width="70%"} |
|:--:| 
| *BFP16* |

Even-though bFP16 also a 16bits representation, it offer greater precision 

* bFP16 includes a sign bit, 8-bit exponent, and 7-bit fraction

###Use cases:

The value proposition by using half precision data types in deep neural network can cut-down training time significantly and memory conception into almost half also without much loss in performance, but narrow exponent and fraction FP16 is less precise than BF16.It is more susceptible to issues like numerical instability, vanishing gradients, and accumulation errors, especially in deep neural networks,
BF16 offers improved numerical precision compared to FP16, making it more suitable for training deep learning models

FP16 is primarily used for inference and certain deep learning tasks where memory and speed are prioritised over precision like 
computer vision tasks where the focus is on inference speed. For example, when running pre-trained CNN models for image classification on a GPU, using FP16 can significantly speed up inference while maintaining reasonable accuracy. Real-time image processing, object detection, and facial recognition..

BF16 is well-suited for training deep neural networks and scientific computing applications where maintaining numerical stability is crucial, Particularly useful in training deep neural networks. Training deep learning models involves both forward and backward passes through the network, as well as gradient updates,The increased numerical precision of BF16 compared to FP16 helps mitigate issues like vanishing gradients and accumulation errors during training. This can lead to faster convergence and more stable training for large and complex models.

##Mixed precision 

Method of using both FP16 and FP32 in a model during training to make run faster and use less memory, by keeping certain part of model on FP32 to avoid risk numerical precision

* Forward Pass: During the forward pass of a deep neural network, which involves computing predictions, mixed precision often uses FP16. This speeds up computation and reduces memory consumption.
* Backward Pass: During the backward pass (gradient computation) and weight updates, mixed precision switches to higher precision, typically FP32. This helps prevent gradient underflow and accumulation errors that can occur when using lower-precision representations.

Using PyTorch, we can implement mixed-precision training with help of  ```torch.cuda.amp(Automatic Mixed Precision) ``` 

>
**Import all dependencies and define model**

```python
import torch
import torch.nn as nn
import torch.optim as optim
from torch.cuda.amp import autocast, GradScaler

class SimpleNN(nn.Module):
    def __init__(self):
        super(SimpleNN, self).__init__()
        self.fc1 = nn.Linear(784, 256)
        self.relu = nn.ReLU()
        self.fc2 = nn.Linear(256, 10)
    
    def forward(self, x):
        x = self.fc1(x)
        x = self.relu(x)
        x = self.fc2(x)
        return x

```

**Initialize the Model and Optimizer:**

```python
model = SimpleNN().cuda()
criterion = nn.CrossEntropyLoss()
optimizer = optim.SGD(model.parameters(), lr=0.01)
```

**Mixed-Precision Setup:**

```python
scaler = GradScaler()
```
**training loop**

```python
for epoch in range(num_epochs):
    for batch_idx, (inputs, targets) in enumerate(train_loader):
        inputs, targets = inputs.cuda(), targets.cuda()
        
        optimizer.zero_grad()
        
        #Forward pass within autocast to use FP16 for forward computations
        with autocast():
            outputs = model(inputs)
            loss = criterion(outputs, targets)
        
        # Backward pass within autocast, scaled gradients to FP32
        scaler.scale(loss).backward()
        scaler.step(optimizer)
        scaler.update()
        
        if batch_idx % log_interval == 0:
            print(f"Epoch [{epoch+1}/{num_epochs}] Batch [{batch_idx+1}/{len(train_loader)}] Loss: {loss.item():.4f}")

```
>


