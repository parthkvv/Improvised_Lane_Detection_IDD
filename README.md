### Prepare CULane data 

```
CULane
├── driver_100_30frame
├── driver_161_90frame
├── driver_182_30frame
├── driver_193_90frame
├── driver_23_30frame
├── driver_37_30frame
├── laneseg_label_w16
├── laneseg_label_w16_test
└── list
```

 Note: Enter absolute path.

### Prepare Tusimple data 

```
Tusimple
├── clips
├── label_data_0313.json
├── label_data_0531.json
├── label_data_0601.json
└── test_label.json
```


### Trained Model 

Model trained on CULane Dataset can be converted from [official implementation](https://github.com/XingangPan/SCNN#Testing)， which can be downloaded [here](https://drive.google.com/open?id=1Wv3r3dCYNBwJdKl_WPEfrEOt-XGaROKu). Please put the `vgg_SCNN_DULR_w9.t7` file into `experiments/vgg_SCNN_DULR_w9`.

  ```bash
  python experiments/vgg_SCNN_DULR_w9/t7_to_pt.py
  ```

Model will be cached into `experiments/vgg_SCNN_DULR_w9/vgg_SCNN_DULR_w9.pth`. 


For single image demo test:

```shell
python demo_test.py   -i demo/demo.jpg 
                      -w experiments/vgg_SCNN_DULR_w9/vgg_SCNN_DULR_w9.pth 
                      [--visualize / -v]
```

### Train 

1. Specify an experiment directory, e.g. `experiments/exp0`. 

2. Modify the hyperparameters in `experiments/exp0/cfg.json`.

3. Start training:

   ```shell
   python train.py --exp_dir ./experiments/exp0 [--resume/-r]
   ```

4. Monitor on tensorboard:

   ```bash
   tensorboard --logdir='experiments/exp0'
   ```

### Evaluation

  1. Please build the CPP code first.  
  2. Then modify `root` as absolute project path in `utils/lane_evaluation/CULane/Run.sh`.

  ```bash
  cd utils/lane_evaluation/CULane
  mkdir build && cd build
  cmake ..
  make
  ```

  Just run the evaluation script. Result will be saved into corresponding `exp_dir` directory, 

  ``` shell
  python test_CULane.py --exp_dir ./experiments/exp10
  ```

  For Tusimple 

  ```Shell
  python test_tusimple.py --exp_dir ./experiments/exp0
  ```
