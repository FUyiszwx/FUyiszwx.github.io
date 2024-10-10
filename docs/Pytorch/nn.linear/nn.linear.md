# Pytorch

For full documentation visit [mkdocs.org](https://www.mkdocs.org).  

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


## nn.linear(in_features, out_features, bias = True)

* `in_features` - 输入的二维张量的大小，即输入的 [batch_size, size] 中的size（输入图片的特征共有多少个，上一个全连接层神经元的个数）。
* `out_features` - 输出的二维张量的大小，即输出的二维张量的形状为[batch_size，output_size]，当然，它也代表了该全连接层的神经元个数。
* `bias` - 是否在线性变换中使用偏置项。默认为True



    PyTorch的nn.Linear（）是用于设置网络中的全连接层的，需要注意在二维图像处理的任务中，
    全连接层的输入与输出一般都设置为二维张量，形状通常为[batch_size, size]，不同于卷积层要求输入输出是四维张量。
