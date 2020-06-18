# Zeolite GAN

`Tensorflow 1.x` implementation of [ZeoGAN](http://advances.sciencemag.org/lookup/doi/10.1126/sciadv.aax9324).
> tested on `tensorflow-gpu==1.12.0`

Generate energy/material shapes (in voxel format).

## Input Arguments
```
--dataset_path /path/to/input_shapes              
--device       1                     # gpu device number
--logdir       /path/to/logdir       # path for log, checkpoint
--z_size       1024
--voxel_size   32
--rate         0.5
--move         True
--rotate       True
--invert       True
--energy_limit -4000 5000
--energy_scale -4000 5000
--cell_length_scale 0.0 150.0
--save_every     1000                # frequency of saving checkpoints
--batch_size     32
--bottom_size    4
--bottom_filters 256
--top_size       4
--filter_unit    32
--d_learning_rate 1e-4
--g_learning_rate 1e-4
--minibatch                False
--minibatch_kernel_size    256
--minibatch_dim_per_kernel 5
--l2_loss False
--train_gen_per_disc 1
--n_critics 5
--gp_lambda 10
--feature_matching True
--in_temper 298.0
--user_desired False                 # non-user-desired generation
--user_range 18 22
#--restore_ckpt /path/to/checkpoint  # if use pre-trained checkpoints
```


## Training of Model
```bash
$ python main.py @input_example.in
```

In `input_example.in`,
```
--dataset_path /path/to/input_shapes              
--device       1                     # gpu device number
--logdir       /path/to/logdir       # path for log, checkpoint

...

--user_range 18 22
#--restore_ckpt /path/to/checkpoint  # if use pre-trained checkpoints
```

## Generation of Material Shapes from Trained Model

```bash
$ python gen.py --checkpoint {} --n_samples {} --savedir={} --device {} --batch_size {} --type normal
```

**checkpoint**: checkpoint path in log_dir
> E.g. `./test_log/save-2020-06-17T13:52:51.090310-100000`

**n_samples**: number of generated shapes
> E.g. `100000`

**savedir**: directory for generated shapes 
> E.g. `./test_generation`

**device**: `GPU device index`

**batch_size:** batch size for generation \
> (Requirement) < 1/100 of n_samples

```bash
$ python gen.py --checkpoint ./test_log/save-2020-06-17T13:52:51.090310-100000 --n_samples 10000 --savedir=./test_generation --device 0 --batch_size 100 --type normal
```
