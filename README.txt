0. 新增了SGPN.py和SGPNloss.py文件，分别是SGPN的架构和SGPN的自定义loss函数。
    SGPN.py使用了tf.keras库将原本的tensorflow代码转换成了keras模型。
    实现过程中没有使用register_conf的功能，因为SGPN是一个多输出模型，使用net_from_config中的方式比较麻烦。
    因此直接在net_from_config函数中调用了SGPN.py中的函数来构建模型。

1. 由于项目需要自定义loss而框架不支持，因此修改了部分框架内容，修改了数据集读取和预处理方式，分别是：
    utils/modelutil.py,     utils/confutil.py,	   utils/datasetutil.py,      utils/kerasutil.py,     run.py

2. 使用方式和原框架相同，在根目录下，运行：python   CG-Final-Project-F/run.py   conf/sgpn/sgpn.pyconf
    运行时需要注意不要安装1.10.5版本的hdf5包。

3. tf.keras自定义使用多输出的loss(loss的计算需要同时用到所有输出)非常麻烦，
    需要将点云数据和两组label同时作为模型的输入，
    因此制作数据集时使用了字典结构作为输入，key值为'input_1', 'input_2', 'input_3',
    使用spyder运行时需要注意，每次训练需要使用新的Ipython kernel，否则输入的key值会改变导致报错。
    错误原因不明，只知道这样会报错。

