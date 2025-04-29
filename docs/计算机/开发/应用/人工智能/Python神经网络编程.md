# 神经网络

**输入层——中间层（隐藏层）——输出层**

**学习率**（0 ~ 1）：如果没有设置学习率，则模型只与最后一次训练样本最匹配，忽略了以前的所有的训练样本。并且限制训练样本中的噪声或错误的影响。

$$
y=\frac{1}{1+e^{-x}}
$$

## 代码的基本结构

```python
class neuralNetwork:
    # 初始化
    def __init__(self):
        pass

    # 训练
    def train():
        pass

    # 查询
    def query():
        pass
```

### 完整结构

```python
import numpy as np
import scipy.special as sl

class neuralNetwork:
    # 初始化
    def __init__(self, inputnodes, hiddennodes, outputnodes, learningrate):
        self.inodes = inputnodes
        self.hnodes = hiddennodes
        self.onodes = outputnodes

        self.lr = learningrate

        self.wih = (np.random.rand(self.hnodes, self.inodes)-0.5)
        self.who = (np.random.rand(self.onodes, self.hnodes)-0.5)

        self.activation_function = lambda x:sl.expit(x)

    # 训练
    def train(self, inputs_list, targets_list):
        inputs = np.array(inputs_list, ndmin=2).T
        targets = np.array(targets_list, ndmin=2).T

        hidden_inputs = np.dot(self.wih, inputs)
        hidden_outputs = self.activation_function(hidden_inputs)
        final_inputs = np.dot(self.who, hidden_outputs)
        final_outputs = self.activation_function(final_inputs)

        output_errors = targets - final_outputs

        hidden_errors = np.dot(self.who.T, output_errors)

        self.who += self.lr * np.dot((output_errors * final_outputs *(1.0 - final_outputs)), np.transpose(hidden_outputs))
        self.wih += self.lr * np.dot((hidden_errors * hidden_outputs *(1.0 - hidden_outputs)), np.transpose(inputs))
        pass


    # 查询
    def query(self, inputs_list):
        inputs = np.array(inputs_list, ndmin=2).T

        hidden_inputs = np.dot(self.wih, inputs)
        hidden_outputs = self.activation_function(hidden_inputs)

        final_inputs = np.dot(self.who, hidden_outputs)
        final_outputs = self.activation_function(final_inputs)

        return final_outputs
```

## 实际应用：手写数字MNIST

[MNIST 数据集](http://yann.lecun.com/exdb/mnist/)MNIST数据集来自美国国家标准与技术研究所, National Institute of Standards and Technology (NIST)。训练集（training set）由来自250个不同人手写的数字构成，其中50%是高中学生，50%来自人口普查局（the Census Bureau）的工作人员。测试集（test set）也是同样比例的手写数字数据，但保证了测试集和训练集的作者集不相交。
MNIST数据集一共有7万张图片，其中6万张是训练集，1万张是测试集。每张图片是28 × 28 的0 − 9的手写数字图片组成。每个图片是黑底白字的形式，黑底用0表示，白字用0-1之间的浮点数表示，越接近1，颜色越白。
MNIST是一个非常经典的手写数字数据集，许多库都包括它。当然除了导入库以外也可以自行下载对应的csv文件使用。

为了方便，这里使用Pytorch的mnist数据集，并转换为numpy数组：

```python
import numpy as np
import torchvision.datasets as datasets

mnist_train = datasets.MNIST(root="./data", train=True, download=True)
mnist_test = datasets.MNIST(root="./data", train=False, download=True)

mnist_train_data = (mnist_train.data).numpy()
mnist_train_targets = (mnist_train.targets).numpy()
```

查看第i+1张图片，方便验证：

```python
import matplotlib.pyplot as plt

matplotlib.pyplot.imshow(mnist_train_data[i], cmap='Greys')
plt.axis('off')
plt.show()
```

### 代码

图片由28* 28个像素点组成，需要得到数字 0 ~ 9

因此，输入层节点设置为784个，输出层节点设置为10个
隐藏层节点个数与学习率先设置为100、0.3，后续再进行[[# 优化思路|优化]]

```python
input_nodes = 784
hidden_nodes = 100
output_nodes = 10
learning_rate = 0.3

n = neuralNetwork(input_nodes, hidden_nodes, output_nodes, learning_rate)

for i in range(60000): # 已知训练集共60000个数据，测试时可适当减少
    inputs = (mnist_train_data[i].flatten() / 255.0 * 0.99) + 0.01
	# 为了使输入值处于激活函数的舒适区间内
	# 把颜色值从[0,255]，映射到(0,1]。不取0是为了避免权重更新失败
	# 实际上可以选取下界为0.01，即映射到[0.01,1]
    targets = np.zeros(output_nodes) + 0.01
    targets[int(mnist_train_targets[i])] = 0.99
    n.train(inputs, targets)
```

#### 测试

使用测试集计算准确率：
```python
mnist_test_data = (mnist_test.data).numpy()
mnist_test_targets = (mnist_test.targets).numpy()
sum = 0
for j in range(10000): # 已知测试集共10000个数据
    if np.argmax(n.query((mnist_test_data[j].flatten() / 255.0 * 0.99) + 0.01)) == mnist_test_targets[j]:
        sum += 1
print('{}%'.format(sum/100))
```

也可以直接查看某一张测试图片以及预测结果：

```python
plt.rcParams['font.sans-serif']=['SimHei']
# （为了显示中文）指定字体为：'SimHei'

def test(k):
    plt.imshow(mnist_test_data[k], cmap='Greys')
    plt.title('预测数字：' + str(np.argmax(n.query((mnist_test_data[k].flatten() / 255.0 * 0.99) + 0.01))))
    plt.axis('off')
    plt.show()
```

#### 使用手写数字测试

28 * 28像素的手写图片

```python
from PIL import Image
import numpy as np

plt.rcParams['font.sans-serif']=['SimHei']
# （为了显示中文）指定字体为：'SimHei'

image =Image.open(r'手写图片.jpg').convert('L')
img_array = np.asarray(image)
img_data = 255.0 - img_array.reshape(784)
img_data = (img_data / 255.0 * 0.99) + 0.01
plt.imshow(img_array, cmap='gray')
plt.title('预测数字：' + str(np.argmax(n.query(img_data))))
plt.axis('off')
plt.show()
```

### 优化思路

#### 增大训练集

更大的训练集一般可以得到更好的神经网络

##### 创建训练数据

利用已有图片样本，顺时针或逆时针旋转图片数组，创建新的样本，模拟人的不同书写风格
注意旋转角度过大会使神经网络性能下降，选择10度左右

`img_array = nd.rotate(img_array, 10, cval = 0.01, reshape = False)`

#### 调整学习率

过高的学习率，导致在梯度下降过程中有一些跳动和超调
过低的学习率，梯度下降的步长太小，限制了梯度下降的速度

#### 重复训练

使用数据集重复多次训练，修改训练部分代码如下：

```python
epochs = 2
for e in range(epochs):
    for i in range(60000):
        inputs = (mnist_train_data[i].flatten() / 255.0 * 0.99) + 0.01
        targets = np.zeros(output_nodes) + 0.01
        targets[int(mnist_train_targets[i])] = 0.99
        n.train(inputs, targets)
```

太多的训练会导致模型过拟合，性能下降。一般在5或7个世代最佳。
在多个世代的情况下，减小学习率能够得到更好的性能

#### 增加隐藏层节点

如果隐藏层节点太少，根本没有足够的空间让神经网络学习知识
在隐藏层节点数量达到某个值，继续增加隐藏层节点数量，性能变化不显著，但是训练所需时间显著增加

### 反向查询

```python
# 下列的代码是需要增加的部分代码
class neuralNetwork:
	def __init__(self, inputnodes, hiddennodes, outputnodes, learningrate):
		self.inverse_activation_function = lambda x:sl.logit(x)
    def backquery(self, targets_list):
        # transpose the targets list to a vertical array
        final_outputs = np.array(targets_list, ndmin=2).T
        
        # calculate the signal into the final output layer
        final_inputs = self.inverse_activation_function(final_outputs)

        # calculate the signal out of the hidden layer
        hidden_outputs = np.dot(self.who.T, final_inputs)
        # scale them back to 0.01 to .99
        hidden_outputs -= np.min(hidden_outputs)
        hidden_outputs /= np.max(hidden_outputs)
        hidden_outputs *= 0.98
        hidden_outputs += 0.01
        
        # calculate the signal into the hidden layer
        hidden_inputs = self.inverse_activation_function(hidden_outputs)
        
        # calculate the signal out of the input layer
        inputs = np.dot(self.wih.T, hidden_inputs)
        # scale them back to 0.01 to .99
        inputs -= np.min(inputs)
        inputs /= np.max(inputs)
        inputs *= 0.98
        inputs += 0.01
        
        return inputs.reshape(28,28)
```

```python
# 调用
plt.imshow(n.backquery([0.99, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01]), cmap='gray')
plt.axis('off')
plt.show()
```

### 完整代码

完整代码并添加终端进度条功能：

```python
import numpy as np
import scipy.special as sl
import torchvision.datasets as datasets
import matplotlib.pyplot as plt

class neuralNetwork:
    # 初始化
    def __init__(self, inputnodes, hiddennodes, outputnodes, learningrate):
        self.inodes = inputnodes
        self.hnodes = hiddennodes
        self.onodes = outputnodes

        self.lr = learningrate

        self.wih = (np.random.rand(self.hnodes, self.inodes)-0.5)
        self.who = (np.random.rand(self.onodes, self.hnodes)-0.5)

        self.activation_function = lambda x:sl.expit(x)
        self.inverse_activation_function = lambda x:sl.logit(x)

    # 训练
    def train(self, inputs_list, targets_list):
        inputs = np.array(inputs_list, ndmin=2).T
        targets = np.array(targets_list, ndmin=2).T

        hidden_inputs = np.dot(self.wih, inputs)
        hidden_outputs = self.activation_function(hidden_inputs)
        final_inputs = np.dot(self.who, hidden_outputs)
        final_outputs = self.activation_function(final_inputs)

        output_errors = targets - final_outputs

        hidden_errors = np.dot(self.who.T, output_errors)

        self.who += self.lr * np.dot((output_errors * final_outputs *(1.0 - final_outputs)), np.transpose(hidden_outputs))
        self.wih += self.lr * np.dot((hidden_errors * hidden_outputs *(1.0 - hidden_outputs)), np.transpose(inputs))
        pass


    # 查询
    def query(self, inputs_list):
        inputs = np.array(inputs_list, ndmin=2).T

        hidden_inputs = np.dot(self.wih, inputs)
        hidden_outputs = self.activation_function(hidden_inputs)

        final_inputs = np.dot(self.who, hidden_outputs)
        final_outputs = self.activation_function(final_inputs)

        return final_outputs
    
    # 反向查询
    def backquery(self, targets_list):
        # transpose the targets list to a vertical array
        final_outputs = np.array(targets_list, ndmin=2).T
        
        # calculate the signal into the final output layer
        final_inputs = self.inverse_activation_function(final_outputs)

        # calculate the signal out of the hidden layer
        hidden_outputs = np.dot(self.who.T, final_inputs)
        # scale them back to 0.01 to .99
        hidden_outputs -= np.min(hidden_outputs)
        hidden_outputs /= np.max(hidden_outputs)
        hidden_outputs *= 0.98
        hidden_outputs += 0.01
        
        # calculate the signal into the hidden layer
        hidden_inputs = self.inverse_activation_function(hidden_outputs)
        
        # calculate the signal out of the input layer
        inputs = np.dot(self.wih.T, hidden_inputs)
        # scale them back to 0.01 to .99
        inputs -= np.min(inputs)
        inputs /= np.max(inputs)
        inputs *= 0.98
        inputs += 0.01
        
        return inputs.reshape(28,28)
    
def accuracy_rate():
    mnist_test_data = (mnist_test.data).numpy()
    mnist_test_targets = (mnist_test.targets).numpy()
    mnist_test_times = 10000
    sum = 0

    print('正在测试准确率:', end='')
    t2 = int(mnist_test_times/50)
    for j in range(mnist_test_times):
        if np.argmax(n.query((mnist_test_data[j].flatten() / 255.0 * 0.99) + 0.01)) == mnist_test_targets[j]:
            sum += 1
        if j % t2 == 0:
            print("▋", end='', flush=True)
    print('')
    print('准确率为：{}%'.format(sum/100))

    
input_nodes = 784
hidden_nodes = 150
output_nodes = 10
learning_rate = 0.1

n = neuralNetwork(input_nodes, hidden_nodes, output_nodes, learning_rate)

mnist_train = datasets.MNIST(root="./data", train=True, download=True)
mnist_test = datasets.MNIST(root="./data", train=False, download=True)

mnist_train_data = (mnist_train.data).numpy()
mnist_train_targets = (mnist_train.targets).numpy()
mnist_train_times = 60000

epochs = 4
for e in range(epochs):
    print('正在第{}次训练:'.format(e+1), end='')
    t1 = int(mnist_train_times/50)
    for i in range(mnist_train_times):
        if i % t1 == 0:
            print("▋", end='', flush=True)
        inputs = (mnist_train_data[i].flatten() / 255.0 * 0.99) + 0.01
        targets = np.zeros(output_nodes) + 0.01
        targets[int(mnist_train_targets[i])] = 0.99
        n.train(inputs, targets)
    print('')
    accuracy_rate()

# plt.imshow(n.backquery([0.99, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01]), cmap='gray')
# plt.axis('off')
# plt.show()
```

保存、调用训练好的模型：
```python
import dill

with open('net.dill', 'wb') as f:
    dill.dump(n, f)

with open('net.dill', 'rb') as f:
    n = dill.load(f)
```

### 使用Pytorch框架重写代码

```python
import torch
from torch.utils.data import DataLoader
from torchvision import transforms
from torchvision.datasets import MNIST
import matplotlib.pyplot as plt

class Net(torch.nn.Module):
    def __init__(self):
        super().__init__()
        self.fc1 = torch.nn.Linear(784, 64)
        self.fc2 = torch.nn.Linear(64, 64)
        self.fc3 = torch.nn.Linear(64, 64)
        self.fc4 = torch.nn.Linear(64, 10)

    def forward(self, x):
        x = torch.nn.functional.relu(self.fc1(x))
        x = torch.nn.functional.relu(self.fc2(x))
        x = torch.nn.functional.relu(self.fc3(x))
        x = torch.nn.functional.log_softmax(self.fc4(x), dim=1)
        return x
    
def get_data_loader(is_train):
    to_sensor = transforms.Compose([transforms.ToTensor()])
    data_set = MNIST("./data", is_train, transform=to_sensor, download=True)
    return DataLoader(data_set, batch_size=15, shuffle=True)

def evaluate(test_data, net):
    n_correct = 0
    n_total = 0
    with torch.no_grad():
        for (x, y) in test_data:
            outputs = net.forward(x.view(-1, 784))
            for i, output in enumerate(outputs):
                if torch.argmax(output) == y[i]:
                    n_correct += 1
                n_total += 1
    return n_correct / n_total
    
def main():
    train_data = get_data_loader(is_train=True)
    test_data = get_data_loader(is_train=False)
    net = Net()

    print('initial accuracy', evaluate(test_data, net))
    optimizer = torch.optim.Adam(net.parameters(), lr=0.001)
    for epoch in range(2):
        for (x, y) in train_data:
            net.zero_grad()
            output = net.forward(x.view(-1, 784))
            loss = torch.nn.functional.nll_loss(output, y)
            loss.backward()
            optimizer.step()
        print("epoch", epoch, "accuracy:", evaluate(test_data, net))

    for (n, (x, _)) in enumerate(test_data):
        if n>3:
            break
        predict = torch.argmax(net.forward(x[0].view(-1, 784)))
        plt.figure(n)
        plt.imshow(x[0].view(28, 28))
        plt.title('prediction:' + str(int(predict)))
    plt.show()

if __name__ == "__main__":
    main()
```
