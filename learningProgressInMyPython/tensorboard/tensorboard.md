# 关于Tensorboard的用法

## 准备工作

1. 首先得准备好cuda和pytorch的安装。在最开始导入SummaryWriter

        from torch.utils.tensorboard import SummaryWriter

2. 在终端中输入`dir`查看当前项目中文件夹的文件，在后续SummaryWriter写入数据时需要提供一个目录来记录信息

3. 终端输入`tensorboard --logdir=./runs` `./runs`为想要可视化数据所在的文件夹路径


## 使用方法

1. 创建接口

        writer = SummaryWriter(
            log_dir="./runs", 
            comment="不指定文件夹目录时，文件夹后缀",filename_suffix="event file文件夹后缀"
            )
2. 记录标量

        writer.add_scalars("name",{"dic":val},epoch)

3. 统计直方图add_histogram()

        writer.add_histogram("weight",self.fc.weight,epoch)

4. 查看模型图
        
        writer.add_graph(model=net,input_to_model=torch.randn(1,3, 224, 224).to(device))

5. 查看网络层形状、参数 torchsummary

        from torchsummary import summary
        summary(net, input_size=(3, 224, 224))

参考:
自己写的一个类：
        
        class TensorboardWriter:
            def __init__(self, log_dir, writer=None):
                self.writer = writer
                self.log_dir = log_dir

            # 创建writer
            def create_writer(self):
                self.writer = SummaryWriter(log_dir=self.log_dir)

            # 记录网络数据
            def tensorboard_model_collect(self, actor, critic, ac_input, critic_input):
                self.writer.add_graph(actor, ac_input)
                self.writer.add_graph(critic, critic_input)

            # 记录常量数据
            def tensorboard_scalarData_collect(self, metrics, timestep):
                self.writer.add_scalar(f'{metrics}', metrics, timestep)

            def tensorboard_histogram_collect(self, actor, critic, timestep):
                # 记录 Actor 网络的参数
                for name, param in actor.named_parameters():
                    writer.add_histogram(f'Actor/Parameters/{name}', param, timestep)

                # 记录 Critic 网络的参数
                for name, param in critic.named_parameters():
                    writer.add_histogram(f'Critic/Parameters/{name}', param, timestep)

            # 关闭writer
            def close_writer(self):
                self.writer.close()
    