---
{"dg-publish":true,"permalink":"/czc知识库/硕士研究生/竞赛/2024华为杯数学建模/赛中/临时/pso伪代码/","dgPassFrontmatter":true,"created":"2024-09-23T11:25:06.507+08:00","updated":"2024-12-08T15:17:38.499+08:00"}
---



### 粒子群优化算法的伪代码

1. **绘制目标函数的图形**
    
    - 定义自变量 x1x_1x1​ 和 x2x_2x2​ 的取值范围为 [−15,15][-15, 15][−15,15]。
    - 计算目标函数 y=x12+x22−x1⋅x2−10⋅x1−4⋅x2+60y = x1^2 + x2^2 - x1 \cdot x2 - 10 \cdot x1 - 4 \cdot x2 + 60y=x12+x22−x1⋅x2−10⋅x1−4⋅x2+60 在定义域中的值。
    - 绘制函数的三维图像。
2. **初始化粒子群算法的参数**
    
    - 设置粒子数量 n=30n = 30n=30、维度数量 narvs=2narvs = 2narvs=2、学习因子 c1=2,c2=2c1 = 2, c2 = 2c1=2,c2=2。
    - 初始和结束时的惯性权重 wstart=0.9w_{start} = 0.9wstart​=0.9, wend=0.4w_{end} = 0.4wend​=0.4。
    - 最大迭代次数 K=100K = 100K=100。
    - 粒子最大速度 vmax=[6,6]vmax = [6, 6]vmax=[6,6]，定义域上下界 xlb=[−15,−15]x_{lb} = [-15, -15]xlb​=[−15,−15], xub=[15,15]x_{ub} = [15, 15]xub​=[15,15]。
3. **初始化粒子的位置和速度**
    
    - 随机生成粒子在定义域范围内的初始位置。
    - 随机生成粒子在最大速度限制范围内的初始速度。
4. **计算初始粒子的适应度**
    
    - 对每个粒子，使用目标函数计算适应度。
    - 将粒子的初始位置设置为该粒子找到的最佳位置 pbestpbestpbest。
    - 记录全局最优位置 gbestgbestgbest，即所有粒子找到的最优位置。
5. **粒子群优化主循环**
    
    - **循环 KKK 次，执行迭代更新：**
        1. **更新每个粒子的速度和位置**
            
            - 根据当前惯性权重 www 以及个体学习因子和社会学习因子，计算每个粒子的速度。
            - 限制速度在最大值范围内。
            - 根据更新后的速度，计算新的位置，并确保位置在定义域范围内。
        2. **更新每个粒子的适应度**
            
            - 计算每个粒子的新适应度。
            - 如果当前适应度优于粒子之前找到的最优适应度，则更新粒子的最优位置 pbestpbestpbest。
            - 如果当前适应度优于全局最优适应度，则更新全局最优位置 gbestgbestgbest。
        3. **记录当前迭代的全局最优适应度值**。
            
        4. **更新图像显示**：在三维图中更新粒子的位置。
            
6. **绘制结果**
    
    - 输出每次迭代后的全局最优适应度随迭代次数的变化。
    - 输出最终的最优位置 gbestgbestgbest 和对应的最优值。
7. **比较不同惯性权重的递减方式**
    
    - 定义三种不同递减方式的惯性权重 w1,w2,w3w1, w2, w3w1,w2,w3，并绘制它们随迭代次数变化的曲线。

---

### 伪代码解释：

- **初始化参数**：首先确定算法中使用的参数，包括粒子的数量、变量的范围、最大速度、惯性权重和学习因子等。
- **位置和速度更新**：根据粒子群算法的公式，使用粒子的历史信息（个体最优和全局最优）来调整它们的速度，并更新它们的位置。
- **适应度计算**：使用目标函数评估粒子的位置，并根据评估结果更新个体和全局最优。
- **循环更新**：通过多次迭代，不断调整粒子的速度和位置，逐步逼近全局最优解。
- **惯性权重策略**：测试和对比不同的惯性权重递减策略，以优化收敛过程。




```matlab
for it=1:MaxIt
    for i=1:nPop
        rep_h=SelectLeader(rep,beta);
 
        particle(i).Velocity=w*particle(i).Velocity ...
                             +c1*rand*(particle(i).Best.Position - particle(i).Position) ...
                             +c2*rand*(rep_h.Position -  particle(i).Position);
 
        particle(i).Velocity=min(max(particle(i).Velocity,-VelMax),+VelMax);
 
        particle(i).Position=particle(i).Position + particle(i).Velocity;
 
        flag=(particle(i).Position<VarMin | particle(i).Position>VarMax);
        particle(i).Velocity(flag)=-particle(i).Velocity(flag);
        
        particle(i).Position=min(max(particle(i).Position,VarMin),VarMax);
 
        particle(i).Cost=CostFunction(particle(i).Position);
 
        if Dominates(particle(i),particle(i).Best)
            particle(i).Best.Position=particle(i).Position;
            particle(i).Best.Cost=particle(i).Cost;
            
        elseif ~Dominates(particle(i).Best,particle(i))
            if rand<0.5
                particle(i).Best.Position=particle(i).Position;
                particle(i).Best.Cost=particle(i).Cost;
            end
        end
 
    end
    
    particle=DetermineDomination(particle);
    nd_particle=GetNonDominatedParticles(particle);
    
    rep=[rep
         nd_particle];
    
    rep=DetermineDomination(rep);
    rep=GetNonDominatedParticles(rep);
    
    for i=1:numel(rep)
        [rep(i).GridIndex rep(i).GridSubIndex]=GetGridIndex(rep(i),G);
    end
    
    if numel(rep)>nRep
        EXTRA=numel(rep)-nRep;
        rep=DeleteFromRep(rep,EXTRA,gamma);
        
        rep_costs=GetCosts(rep);
        G=CreateHypercubes(rep_costs,nGrid,alpha);
        
    end
   
    disp(['Iteration ' num2str(it) ': Number of Repository Particles = ' num2str(numel(rep))]);
    
    w=w*wdamp;
end
A_055
```



