## AFM_avazu_x4_002

A hands-on guide to run the AFM model on the Avazu_x4_002 dataset.

Author: [XUEPAI](https://github.com/xue-pai)

### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.60GHz
  GPU: Tesla P100 16G
  RAM: 755G

  ```

+ Software

  ```python
  CUDA: 10.0
  python: 3.6.5
  pytorch: 1.0.1.post2
  pandas: 0.23.0
  numpy: 1.18.1
  scipy: 1.1.0
  sklearn: 0.23.1
  pyyaml: 5.1
  h5py: 2.7.1
  tqdm: 4.59.0
  fuxictr: 1.0.2
  ```

### Dataset
Dataset ID: [Avazu_x4_002](https://github.com/openbenchmark/BARS/blob/master/ctr_prediction/datasets/Avazu/README.md#Avazu_x4_002). Please refer to the dataset details to get data ready.

### Code

We use [FuxiCTR-v1.0.2](https://github.com/xue-pai/FuxiCTR/tree/v1.0.2) for this experiment. See the model code: [AFM](https://github.com/xue-pai/FuxiCTR/blob/v1.0.2/fuxictr/pytorch/models/AFM.py).

Running steps:

1. Download [FuxiCTR-v1.0.2](https://github.com/xue-pai/FuxiCTR/archive/refs/tags/v1.0.2.zip) and install all the dependencies listed in the [environments](#environments). Then modify [run_expid.py](./run_expid.py#L5) to add the FuxiCTR library to system path
    
    ```python
    sys.path.append('YOUR_PATH_TO_FuxiCTR/')
    ```

2. Create a data directory and put the downloaded csv files in `../data/Avazu/Avazu_x4`.

3. Both `dataset_config.yaml` and `model_config.yaml` files are available in [AFM_avazu_x4_tuner_config_02](./AFM_avazu_x4_tuner_config_02). Make sure the data paths in `dataset_config.yaml` are correctly set to what we create in the last step.

4. Run the following script to start.

    ```bash
    cd AFM_avazu_x4_002
    nohup python run_expid.py --config ./AFM_avazu_x4_tuner_config_02 --expid AFM_avazu_x4_009_50fcacf1 --gpu 0 > run.log &
    tail -f run.log
    ```

### Results

| logloss | AUC  |
|:--------------------:|:--------------------:|
| 0.378094 | 0.784028  |


### Logs
```python
2020-01-11 07:12:02,228 P41426 INFO {
    "attention_dim": "40",
    "attention_dropout": "0",
    "batch_size": "10000",
    "dataset_id": "avazu_x4_001_d45ad60e",
    "embedding_dim": "40",
    "embedding_dropout": "0",
    "embedding_regularizer": "1e-07",
    "epochs": "100",
    "every_x_epochs": "1",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['logloss', 'AUC']",
    "model": "AFM",
    "model_id": "AFM_avazu_x4_009_50fcacf1",
    "model_root": "./Avazu/AFM_avazu/",
    "monitor": "{'AUC': 1, 'logloss': -1}",
    "monitor_mode": "max",
    "net_regularizer": "0",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "save_best_only": "True",
    "seed": "2019",
    "shuffle": "True",
    "task": "binary_classification",
    "use_hdf5": "True",
    "verbose": "0",
    "workers": "3",
    "data_format": "csv",
    "data_root": "../data/Avazu/",
    "feature_cols": "[{'active': False, 'dtype': 'str', 'name': 'id', 'type': 'categorical'}, {'active': True, 'dtype': 'str', 'name': 'hour', 'preprocess': 'convert_hour', 'type': 'categorical'}, {'active': True, 'dtype': 'str', 'name': ['C1', 'banner_pos', 'site_id', 'site_domain', 'site_category', 'app_id', 'app_domain', 'app_category', 'device_id', 'device_ip', 'device_model', 'device_type', 'device_conn_type', 'C14', 'C15', 'C16', 'C17', 'C18', 'C19', 'C20', 'C21'], 'type': 'categorical'}, {'active': True, 'dtype': 'str', 'name': 'weekday', 'preprocess': 'convert_weekday', 'type': 'categorical'}, {'active': True, 'dtype': 'str', 'name': 'weekend', 'preprocess': 'convert_weekend', 'type': 'categorical'}]",
    "label_col": "{'dtype': 'float', 'name': 'click'}",
    "min_categr_count": "1",
    "test_data": "../data/Avazu/Avazu_x4/test.csv",
    "train_data": "../data/Avazu/Avazu_x4/train.csv",
    "valid_data": "../data/Avazu/Avazu_x4/valid.csv",
    "version": "pytorch",
    "gpu": "1"
}
2020-01-11 07:12:02,229 P41426 INFO Set up feature encoder...
2020-01-11 07:12:02,229 P41426 INFO Load feature_encoder from pickle: ../data/Avazu/avazu_x4_001_d45ad60e/feature_encoder.pkl
2020-01-11 07:12:08,617 P41426 INFO Loading data...
2020-01-11 07:12:08,667 P41426 INFO Loading data from h5: ../data/Avazu/avazu_x4_001_d45ad60e/train.h5
2020-01-11 07:12:11,321 P41426 INFO Loading data from h5: ../data/Avazu/avazu_x4_001_d45ad60e/valid.h5
2020-01-11 07:12:12,740 P41426 INFO Train samples: total/32343172, pos/5492052, neg/26851120, ratio/16.98%
2020-01-11 07:12:12,913 P41426 INFO Validation samples: total/4042897, pos/686507, neg/3356390, ratio/16.98%
2020-01-11 07:12:12,913 P41426 INFO Loading train data done.
2020-01-11 07:12:23,857 P41426 INFO **** Start training: 3235 batches/epoch ****
2020-01-11 07:31:58,140 P41426 INFO [Metrics] logloss: 0.382760 - AUC: 0.775380
2020-01-11 07:31:58,202 P41426 INFO Save best model: monitor(max): 0.392620
2020-01-11 07:31:59,529 P41426 INFO --- 3235/3235 batches finished ---
2020-01-11 07:31:59,584 P41426 INFO Train loss: 0.396495
2020-01-11 07:31:59,584 P41426 INFO ************ Epoch=1 end ************
2020-01-11 07:51:30,237 P41426 INFO [Metrics] logloss: 0.378243 - AUC: 0.783821
2020-01-11 07:51:30,296 P41426 INFO Save best model: monitor(max): 0.405578
2020-01-11 07:51:32,955 P41426 INFO --- 3235/3235 batches finished ---
2020-01-11 07:51:33,024 P41426 INFO Train loss: 0.374134
2020-01-11 07:51:33,024 P41426 INFO ************ Epoch=2 end ************
2020-01-11 08:11:05,978 P41426 INFO [Metrics] logloss: 0.386375 - AUC: 0.779663
2020-01-11 08:11:06,044 P41426 INFO Monitor(max) STOP: 0.393288 !
2020-01-11 08:11:06,045 P41426 INFO Reduce learning rate on plateau: 0.000100
2020-01-11 08:11:06,045 P41426 INFO --- 3235/3235 batches finished ---
2020-01-11 08:11:06,115 P41426 INFO Train loss: 0.343363
2020-01-11 08:11:06,115 P41426 INFO ************ Epoch=3 end ************
2020-01-11 08:30:38,278 P41426 INFO [Metrics] logloss: 0.409156 - AUC: 0.773033
2020-01-11 08:30:38,351 P41426 INFO Monitor(max) STOP: 0.363876 !
2020-01-11 08:30:38,351 P41426 INFO Reduce learning rate on plateau: 0.000010
2020-01-11 08:30:38,351 P41426 INFO Early stopping at epoch=4
2020-01-11 08:30:38,351 P41426 INFO --- 3235/3235 batches finished ---
2020-01-11 08:30:38,415 P41426 INFO Train loss: 0.306409
2020-01-11 08:30:38,416 P41426 INFO Training finished.
2020-01-11 08:30:38,416 P41426 INFO Load best model: /home/XXX/benchmarks/Avazu/AFM_avazu/avazu_x4_001_d45ad60e/AFM_avazu_x4_009_50fcacf1_avazu_x4_001_d45ad60e_model.ckpt
2020-01-11 08:30:40,339 P41426 INFO ****** Train/validation evaluation ******
2020-01-11 08:36:44,997 P41426 INFO [Metrics] logloss: 0.332621 - AUC: 0.853023
2020-01-11 08:37:29,130 P41426 INFO [Metrics] logloss: 0.378243 - AUC: 0.783821
2020-01-11 08:37:29,344 P41426 INFO ******** Test evaluation ********
2020-01-11 08:37:29,344 P41426 INFO Loading data...
2020-01-11 08:37:29,345 P41426 INFO Loading data from h5: ../data/Avazu/avazu_x4_001_d45ad60e/test.h5
2020-01-11 08:37:30,004 P41426 INFO Test samples: total/4042898, pos/686507, neg/3356391, ratio/16.98%
2020-01-11 08:37:30,005 P41426 INFO Loading test data done.
2020-01-11 08:38:13,464 P41426 INFO [Metrics] logloss: 0.378094 - AUC: 0.784028

```
