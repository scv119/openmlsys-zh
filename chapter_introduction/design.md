## 机器学习框架的设计目标

为了支持在不同应用中高效开发机器学习算法，人们设计和实现了**机器学习框架**（如TensorFlow、PyTorch、MindSpore等）。广义来说，这些框架实现了以下共性的设计目标：

-   **神经网络编程：**
    深度学习的巨大成功使得神经网络成为了许多机器学习应用的核心。根据应用的需求，人们需要定制不同的神经网络，如卷积神经网络（Convolutional Neural Networks）和自注意力神经网络（Self-Attention Neural Networks）等。这些神经网络需要一个共同的系统软件进行开发、训练和部署。

-   **自动微分：**
    训练神经网络会具有模型参数。这些参数需要通过持续计算梯度（Gradients）迭代改进。梯度的计算往往需要结合训练数据、数据标注和损失函数（Loss
    Function）。考虑到大多数开发人员并不具备手工计算梯度的知识，机器学习框架需要根据开发人员给出的神经网络程序，全自动地计算梯度。这一过程被称之为自动微分。

-   **数据管理和处理：**
    机器学习的核心是数据。这些数据包括训练、验证、测试数据集和模型参数。因此，需要系统本身支持数据读取、存储和预处理（例如数据增强和数据清洗）。

-   **模型训练和部署：**
    为了让机器学习模型达到最佳的性能，需要使用优化方法（例如Mini-Batch SGD）来通过多步迭代反复计算梯度，这一过程称之为训练。训练完成后，需要将训练好的模型部署到推理设备。

-   **硬件加速器：**
    神经网络的相关计算往往通过矩阵计算实现。这一类计算可以被硬件加速器（例如，通用图形处理器-GPU）加速。因此，机器学习系统需要高效利用多种硬件加速器。

-   **分布式执行：**
    随着训练数据量和神经网络参数量的上升，机器学习系统的内存用量远远超过了单个机器可以提供的内存。因此，机器学习框架需要天然具备分布式执行的能力。

在设计机器学习框架之初，开发者曾尝试通过传统的**神经网络开发库**（如Theano和Caffe）、以及**数据处理框架**（如Apache Spark和Google Pregel）等方式达到以上设计目标。可是他们发现，
神经网络库虽然提供了神经网络开发、自动微分和硬件加速器的支持，但缺乏管理和处理大型数据集、模型部署和分布式执行的能力，无法满足当今产品级机器学习应用的开发任务。
另一方面，虽然并行数据计算框架具有成熟的分布式运行和数据管理能力，但缺乏对神经网络、自动微分和加速器的支持，并不适合开发以神经网络为核心的机器学习应用。

考虑到上述已有软件系统的种种不足，许多公司开发人员和大学研究人员开始从头设计和实现针对机器学习的软件框架。在短短数年间，机器学习框架如雨后春笋般出现（较为知名的例子包括TensorFlow、PyTorch、MindSpore、MXNet、PaddlePaddle、OneFlow、CNTK等），极大推进了人工智能在上下游产业中的发展。表 :numref:`comparison_of_ml_frameworks` 总结了机器学习框架和相关系统的区别。

:机器学习框架和相关系统的区别

|  方式  | 神经网络 | 自动微分 | 数据管理 | 训练和部署 | 硬件加速器 | 分布式执行 |
|:-: |:-:| :-: |:-:|:-: |:-:|:-:|
| 神经网络库 | 是      | 是      | 否            | 否        | 是    | 否    |
| 大数据框架 | 否      | 否      | 是            | 否        | 否    | 是    |
| 机器学习框架 | 是      | 是      | 是            | 是        | 是    | 是    |
:label:`comparison_of_ml_frameworks`