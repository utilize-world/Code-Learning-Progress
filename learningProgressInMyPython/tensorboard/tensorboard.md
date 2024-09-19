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
        
        import torch
from torch.utils.tensorboard import SummaryWriter




    class TensorboardWriter:
        def __init__(self, log_dir, writer=None, time_step=None):
            self.writer = writer
            self.log_dir = log_dir
            self.time_step = time_step
            self.write_enabled = True  # 添加标志位来控制写入操作
            self.hist_enable = False
        # 创建writer
        def create_writer(self):
            self.writer = SummaryWriter(log_dir=self.log_dir)
            return self.writer

        def get_timestep(self, time_step):
            self.time_step = time_step

        # 记录网络数据
        def tensorboard_model_collect(self, wrapper, alg):
            if not self.write_enabled:
                return
            # 生成虚拟输入向量
            # 因为目的是为了看网络结构，所以输入的维度只要保证最后一维能连上就行
            if alg == "MADDPG":
                ac_input_dim = wrapper.actor.get_input_dim()
                cr_input_dim_o, cr_input_dim_a = wrapper.critic.get_input_dim()
                dummy_input_Actor = torch.randn(1, ac_input_dim).cuda()
                dummy_input_Critic_state = torch.randn(1, cr_input_dim_o).cuda()
                dummy_input_Critic_action = torch.randn(1, cr_input_dim_a).cuda()
                self.writer.add_graph(wrapper, (dummy_input_Critic_state, dummy_input_Critic_action, dummy_input_Actor),)
            if alg == "MLGA2C":
                ac_input_dim = wrapper.actor.input_dim
                dummy_input_Actor = torch.randn(1, ac_input_dim).cuda()
                dummy_input_Critic_state = torch.randn(2, 7, 2).cuda()
                dummy_input_Critic_state_o = [torch.randn(2, 7, 2).cuda(), torch.randn(2, 7, 2).cuda()]
                dummy_input_critic_ac = torch.randn(2, 1, 2).cuda()
                dummy_input_critic_ac_o = [torch.randn(2, 1, 2).cuda(),torch.randn(2, 1, 2).cuda()]
                self.writer.add_graph(wrapper, (dummy_input_Actor,
                                                dummy_input_Critic_state,
                                                dummy_input_Critic_state_o,
                                                dummy_input_critic_ac,
                                                dummy_input_critic_ac_o))
        # 记录常量数据
        def tensorboard_scalardata_collect(self, metrics, timestep, name=None):
            if not self.write_enabled:
                return
            self.writer.add_scalar(f"{name}_", metrics, timestep)

        # 记录parameter变化
        def tensorboard_histogram_collect(self, actor, critic, timestep, agent_id):
            if not self.write_enabled or not self.hist_enable:
                return
            # 记录 Actor 网络的参数
            for name, param in actor.named_parameters():
                self.writer.add_histogram(f'Actor{agent_id}/Parameters/{name}', param, timestep)

            # 记录 Critic 网络的参数
            for name, param in critic.named_parameters():
                self.writer.add_histogram(f'Critic{agent_id}/Parameters/{name}', param, timestep)

        # 关闭writer
        def close_writer(self):
            self.writer.close()

        # 启用写入操作
        def enable_write(self):
            self.write_enabled = True

        # 禁用写入操作
        def disable_write(self):
            self.write_enabled = False

        def enable_hist(self):
            self.hist_enable = True

        def disable_hist(self):
            self.hist_enable = False
    