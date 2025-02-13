.. _cn_api_paddle_incubate_asp_prune_model:

prune_model
-------------------------------

.. py:function:: paddle.incubate.asp.prune_model(model, n=2, m=4, mask_algo='mask_1d', with_mask=True)


使用 `mask_algo` 指定的掩码生成函数裁剪 model 中支持 ASP（Auto SParsity） 的子层参数。支持训练和推理，并由 `with_mask` 参数控制。如果 with_mask 是 True ，则还会裁剪与参数相关的 ASP 掩码变量，如果是 False，则仅裁剪参数本身。

.. note::
    - 在静态图模式下，使用 `with_mask` 调用函数时，需要先调用 OptimizerWithSparsityGuarantee.minimize 和 exe.run(startup_program) 来成功获取掩码变量。通常情况下训练时（已调用 OptimizerWithSparsityGuarantee.minimize）设置 `with_mask` 为 True。而仅进行推理时，设置 `with_mask` 为 False。 获取 OptimizerWithSparsityGuarantee 请参考 :ref:`paddle.incubate.asp.decorate <cn_api_paddle_incubate_asp_decorate>`。
    - 在动态图模式下，使用 with_mask 调用函数时，需要先调用 :ref:`paddle.incubate.asp.decorate <cn_api_paddle_incubate_asp_decorate>` 来获取掩码变量。


参数
:::::::::
- **model** (Program|nn.Layer) - 包含模型定义和参数的 Program ，或者 paddle.nn.Layer 对象
- **n** (int，可选) - n:m 稀疏模式中的 n ，默认值为 2。
- **m** (int，可选) - n:m 稀疏模式中的 m ，默认值为 4。
- **mask_algo** (string，可选) - 生成稀疏掩码的函数名。默认值为 mask_1d。有效输入应为 mask_1d ， mask_2d_greedy 和 mask_2d_best 中的一个。
- **with_mask** (bool，可选) - 选择是否裁剪参数相关的 ASP 掩码变量，True 是要裁剪，False 就是不裁剪。默认是 True。

返回
:::::::::

**dictionary** - 一个字典，key 是参数名称，value 是对应的掩码变量。

代码示例
:::::::::

1. 动态图模式

COPY-FROM: paddle.incubate.asp.prune_model:dynamic-graph

2. 静态图模式

COPY-FROM: paddle.incubate.asp.prune_model:static-graph
