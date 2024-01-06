## DeepCross_criteo_x4_001

A hands-on guide to run the DeepCrossing model on the Criteo_x4_001 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) Gold 6278C CPU @ 2.60GHz
  GPU: Tesla V100 32G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 10.2
  python: 3.6.4
  pytorch: 1.0.0
  pandas: 0.22.0
  numpy: 1.19.2
  scipy: 1.5.4
  sklearn: 0.22.1
  pyyaml: 5.4.1
  h5py: 2.8.0
  tqdm: 4.60.0
  fuxictr: 1.0.2
  ```

### Dataset
Dataset ID: [Criteo_x4_001](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Criteo/README.md#Criteo_x4_001). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.0.2](https://github.com/xue-pai/FuxiCTR/tree/v1.0.2) for this experiment. See the model code: [DeepCrossing](https://github.com/xue-pai/FuxiCTR/blob/v1.0.2/fuxictr/pytorch/models/DeepCrossing.py).

Running steps:

1. Download [FuxiCTR-v1.0.2](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.0.2.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Criteo/Criteo_x4`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [DeepCrossing_criteo_x4_tuner_config_01](./DeepCrossing_criteo_x4_tuner_config_01). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd DeepCross_criteo_x4_001
    nohup python run_expid.py --config ./DeepCrossing_criteo_x4_tuner_config_01 --expid DeepCrossing_criteo_x4_018_3638c8fb --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

| logloss | AUC  |
|:--------------------:|:--------------------:|
| 0.438392 | 0.813536  |


### Logs
```python
2020-07-10 00:37:03,171 P4161 INFO {
    "batch_norm": "False",
    "batch_size": "10000",
    "data_format": "h5",
    "data_root": "../data/Criteo/",
    "dataset_id": "criteo_x4_5c863b0f",
    "debug": "False",
    "dnn_activations": "relu",
    "embedding_dim": "16",
    "embedding_dropout": "0",
    "embedding_regularizer": "1e-05",
    "epochs": "100",
    "every_x_epochs": "1",
    "gpu": "0",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['logloss', 'AUC']",
    "model": "DeepCrossing",
    "model_id": "DeepCrossing_criteo_x4_5c863b0f_018_d094b29c",
    "model_root": "./Criteo/DeepCrossing_criteo/min10/",
    "monitor": "{'AUC': 1, 'logloss': -1}",
    "monitor_mode": "max",
    "net_dropout": "0.2",
    "net_regularizer": "0",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "residual_blocks": "[1000, 1000]",
    "save_best_only": "True",
    "seed": "2019",
    "shuffle": "True",
    "task": "binary_classification",
    "test_data": "../data/Criteo/criteo_x4_5c863b0f/test.h5",
    "train_data": "../data/Criteo/criteo_x4_5c863b0f/train.h5",
    "use_hdf5": "True",
    "use_residual": "True",
    "valid_data": "../data/Criteo/criteo_x4_5c863b0f/valid.h5",
    "verbose": "0",
    "version": "pytorch",
    "workers": "3"
}
2020-07-10 00:37:03,173 P4161 INFO Set up feature encoder...
2020-07-10 00:37:03,173 P4161 INFO Load feature_map from json: ../data/Criteo/criteo_x4_5c863b0f/feature_map.json
2020-07-10 00:37:03,174 P4161 INFO Loading data...
2020-07-10 00:37:03,178 P4161 INFO Loading data from h5: ../data/Criteo/criteo_x4_5c863b0f/train.h5
2020-07-10 00:37:10,440 P4161 INFO Loading data from h5: ../data/Criteo/criteo_x4_5c863b0f/valid.h5
2020-07-10 00:37:12,313 P4161 INFO Train samples: total/36672493, pos/9396350, neg/27276143, ratio/25.62%
2020-07-10 00:37:12,439 P4161 INFO Validation samples: total/4584062, pos/1174544, neg/3409518, ratio/25.62%
2020-07-10 00:37:12,439 P4161 INFO Loading train data done.
2020-07-10 00:37:17,156 P4161 INFO Start training: 3668 batches/epoch
2020-07-10 00:37:17,156 P4161 INFO ************ Epoch=1 start ************
2020-07-10 00:43:04,392 P4161 INFO [Metrics] logloss: 0.445513 - AUC: 0.805904
2020-07-10 00:43:04,396 P4161 INFO Save best model: monitor(max): 0.360390
2020-07-10 00:43:04,470 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 00:43:04,515 P4161 INFO Train loss: 0.458962
2020-07-10 00:43:04,516 P4161 INFO ************ Epoch=1 end ************
2020-07-10 00:48:48,526 P4161 INFO [Metrics] logloss: 0.443227 - AUC: 0.808416
2020-07-10 00:48:48,528 P4161 INFO Save best model: monitor(max): 0.365189
2020-07-10 00:48:48,627 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 00:48:48,680 P4161 INFO Train loss: 0.453034
2020-07-10 00:48:48,680 P4161 INFO ************ Epoch=2 end ************
2020-07-10 00:54:33,001 P4161 INFO [Metrics] logloss: 0.441943 - AUC: 0.809699
2020-07-10 00:54:33,002 P4161 INFO Save best model: monitor(max): 0.367756
2020-07-10 00:54:33,090 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 00:54:33,150 P4161 INFO Train loss: 0.450947
2020-07-10 00:54:33,150 P4161 INFO ************ Epoch=3 end ************
2020-07-10 01:00:17,275 P4161 INFO [Metrics] logloss: 0.441291 - AUC: 0.810400
2020-07-10 01:00:17,276 P4161 INFO Save best model: monitor(max): 0.369109
2020-07-10 01:00:17,371 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 01:00:17,418 P4161 INFO Train loss: 0.449773
2020-07-10 01:00:17,418 P4161 INFO ************ Epoch=4 end ************
2020-07-10 01:06:01,492 P4161 INFO [Metrics] logloss: 0.441612 - AUC: 0.810555
2020-07-10 01:06:01,493 P4161 INFO Monitor(max) STOP: 0.368943 !
2020-07-10 01:06:01,493 P4161 INFO Reduce learning rate on plateau: 0.000100
2020-07-10 01:06:01,493 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 01:06:01,564 P4161 INFO Train loss: 0.448975
2020-07-10 01:06:01,564 P4161 INFO ************ Epoch=5 end ************
2020-07-10 01:11:45,507 P4161 INFO [Metrics] logloss: 0.438737 - AUC: 0.813095
2020-07-10 01:11:45,509 P4161 INFO Save best model: monitor(max): 0.374358
2020-07-10 01:11:45,631 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 01:11:45,683 P4161 INFO Train loss: 0.436915
2020-07-10 01:11:45,683 P4161 INFO ************ Epoch=6 end ************
2020-07-10 01:17:29,535 P4161 INFO [Metrics] logloss: 0.438975 - AUC: 0.812917
2020-07-10 01:17:29,536 P4161 INFO Monitor(max) STOP: 0.373942 !
2020-07-10 01:17:29,536 P4161 INFO Reduce learning rate on plateau: 0.000010
2020-07-10 01:17:29,536 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 01:17:29,610 P4161 INFO Train loss: 0.431932
2020-07-10 01:17:29,610 P4161 INFO ************ Epoch=7 end ************
2020-07-10 01:23:09,369 P4161 INFO [Metrics] logloss: 0.439968 - AUC: 0.812268
2020-07-10 01:23:09,370 P4161 INFO Monitor(max) STOP: 0.372300 !
2020-07-10 01:23:09,370 P4161 INFO Reduce learning rate on plateau: 0.000001
2020-07-10 01:23:09,370 P4161 INFO Early stopping at epoch=8
2020-07-10 01:23:09,370 P4161 INFO --- 3668/3668 batches finished ---
2020-07-10 01:23:09,420 P4161 INFO Train loss: 0.426959
2020-07-10 01:23:09,420 P4161 INFO Training finished.
2020-07-10 01:23:09,420 P4161 INFO Load best model: /cache/XXX/FuxiCTR/benchmarks/Criteo/DeepCrossing_criteo/min10/criteo_x4_5c863b0f/DeepCrossing_criteo_x4_5c863b0f_018_d094b29c_model.ckpt
2020-07-10 01:23:09,724 P4161 INFO ****** Train/validation evaluation ******
2020-07-10 01:27:02,035 P4161 INFO [Metrics] logloss: 0.424063 - AUC: 0.828717
2020-07-10 01:27:28,811 P4161 INFO [Metrics] logloss: 0.438737 - AUC: 0.813095
2020-07-10 01:27:28,890 P4161 INFO ******** Test evaluation ********
2020-07-10 01:27:28,890 P4161 INFO Loading data...
2020-07-10 01:27:28,890 P4161 INFO Loading data from h5: ../data/Criteo/criteo_x4_5c863b0f/test.h5
2020-07-10 01:27:29,917 P4161 INFO Test samples: total/4584062, pos/1174544, neg/3409518, ratio/25.62%
2020-07-10 01:27:29,917 P4161 INFO Loading test data done.
2020-07-10 01:27:59,868 P4161 INFO [Metrics] logloss: 0.438392 - AUC: 0.813536

```
