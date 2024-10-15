
## nn.module

通过继承 nn.Module 并在其子类中定义模型结构和前向传播逻辑（forward() 方法），开发者能够方便地搭建并训练深度学习模型。

在自定义一个新的模型类时，通常需要：

* 继承 nn.Module 类
* 重新实现 __init__ 构造函数
* 重新实现 forward 方法

```
import torch.nn as nn
import torch.nn.functional as F

class Model(nn.Module):
    # nn.Module的子类函数必须在构造函数中执行父类的构造函数
    def __init__(self):
        super(Model, self).__init__()   # 等价与nn.Module.__init__() 
        #super(type, obj)返回type类型的父类在obj实例所属类中的方法解析顺序的下一个类，通常在多继承中使用保证调用的准确性。
        # Model为当前类，self为Model类中的对象
        self.conv1 = nn.Conv2d(1, 20, 5)
        self.conv2 = nn.Conv2d(20, 20, 5)
	def forward(self, x):
		x = F.relu(self.conv1(x))
		return F.relu(self.conv2(x))
    
   
model=Model()
print(model)

```

* 一般把网络中具有可学习参数的层（如全连接层、卷积层）放在构造函数 __init__() 中
* forward() 方法必须重写，它是实现模型的功能，实现各个层之间连接关系的核心

nn.Module类中的关键属性和方法包括：

    1.初始化 (init)：在类的初始化方法中定义并实例化所有需要的层、参数和其他组件。
        在实现自己的MyModel类时继承了nn.Module，   
        在构造函数中要调用Module的构造函数 super(MyModel,self).init()

    2.前向传播 (forward)：实现前向传播函数来描述输入数据如何通过网络产生输出结果。
        因为parameters是自动求导，所以调用forward()后，不用自己写和调用backward()函数。   
        而且一般不是显式的调用forward(layer.farword)，而是layer(input)，会自执行forward()。

    3.管理参数和模块：

        使用 .parameters() 访问模型的所有可学习参数。
        使用 add_module() 添加子模块，并给它们命名以便于访问。
        使用 register_buffer() 为模型注册非可学习的缓冲区变量。

    4.训练与评估模式切换：

        使用 model.train() 将模型设置为训练模式，这会影响某些层的行为，如批量归一化层和丢弃层。
        使用 model.eval() 将模型设置为评估模式，此时会禁用这些依赖于训练阶段的行为。

    5.保存和加载模型状态：

        调用 model.state_dict() 获取模型权重和优化器状态的字典形式。
        使用 torch.save() 和 torch.load() 来保存和恢复整个模型或者仅其状态字典。
        通过 model.load_state_dict(state_dict) 加载先前保存的状态字典到模型中。
        此外，nn.Module 还提供了诸如移动模型至不同设备（CPU或GPU）、零化梯度等实用功能，这些功能在整个模型训练过程中起到重要作用。