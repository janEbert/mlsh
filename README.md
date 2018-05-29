Fork of the [original](https://github.com/openai/mlsh) Meta-Learning Shared Hierarchies repository.

# Meta-Learning Shared Hierarchies

Code for [Meta-Learning Shared Hierarchies](https://s3-us-west-2.amazonaws.com/openai-assets/MLSH/mlsh_paper.pdf).

Includes pre-trained checkpoints for task AntBandits-v1 (up to 2000 epochs).

##### Installation

Install [mujoco-py](https://github.com/openai/mujoco-py/) and MuJoCo by following the [installation instructions](https://github.com/openai/mujoco-py/#install-mujoco).

To test whether MuJoCo works, execute the following command in the `mjpro*/bin` folder:
```
./simulate ../model/humanoid.xml
```

Add to your `.bashrc` (replace ... with path to directory):
```
export PYTHONPATH=$PYTHONPATH:/.../mlsh/gym;
export PYTHONPATH=$PYTHONPATH:/.../mlsh/rl-algs;
```

Install MovementBandits environments:
```
cd test_envs
pip install -e .
```
Use `pip3` if `pip` links to an older version of Python (like in the university computers).

###### Installing on the university computers

If you are installing on the university computers, install mujoco-py version 0.5.7 with MuJoCo version 1.31 as newer versions will not work.
Also remember to always use `python3` or `pip3` instead of `python` or `pip`.
```
pip3 install mujoco-py==0.5.7
```

##### Running Experiments

The MLSH script works on any Gym environment that implements the `randomizeCorrect()` function. See the `envs/` folder for examples of such environments.

To run on multiple cores:
```
mpirun -np 12 python main.py ...
```

###### Training

```
python main.py --task AntBandits-v1 --num_subs 2 --macro_duration 1000 --num_rollouts 2000 --warmup_time 20 --train_time 30 --replay False AntAgent

```
Use `python3` if `python` links to an older version of Python (like in the university computers).

###### Visualization

Once you've trained your agent, view it by running:
```
python main.py [...] --replay True --continue_iter [your iteration] AntAgent
```
`[your iteration]` should be 2000 to view the latest uploaded checkpoint
