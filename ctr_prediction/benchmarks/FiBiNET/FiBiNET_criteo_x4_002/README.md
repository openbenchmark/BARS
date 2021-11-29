## FiBiNET_Criteo_x4_002

A notebook to benchmark FiBiNET on Criteo_x4_002 dataset.

Author: [XUEPAI Team](https://github.com/xue-pai)


### Index
[Environments](#Environments) | [Dataset](#Dataset) | [Code](#Code) | [Results](#Results) | [Logs](#Logs)

### Environments
+ Hardware

  ```python
  CPU: Intel(R) Xeon(R) CPU E5-2690 v4 @ 2.6GHz
  RAM: 500G+
  ```
+ Software

  ```python
  python: 3.6.5
  pandas: 1.0.0
  numpy: 1.18.1
  ```

### Dataset
In this setting, we follow the winner's solution of the Criteo challenge to discretize each integer value x to ⌊log2 (x)⌋, if x > 2; and x = 1 otherwise. For all categorical fields, we replace infrequent features with a default <OOV> token by setting the threshold min_category_count=2.

We fix embedding_dim=40 in this setting.
### Code
1. Install FuxiCTR
  
    Install FuxiCTR via `pip install fuxictr==1.0` to get all dependencies ready. Then download [the FuxiCTR repository](https://github.com/huawei-noah/benchmark/archive/53e314461c19dbc7f462b42bf0f0bfae020dc398.zip) to your local path.

2. Downalod the dataset and run [the preprocessing script](https://github.com/xue-pai/Open-CTR-Benchmark/blob/master/datasets/Criteo/Criteo_x4/split_criteo_x4.py) for data splitting. 

3. Download the hyper-parameter configuration file: [FiBiNET_criteo_x4_tuner_config_03.yaml](./002/FiBiNET_criteo_x4_tuner_config_03.yaml)

4. Run the following script to reproduce the result. 
  + --config: The config file that defines the tuning space
  + --tag: Specify which expid to run (each expid corresponds to a specific setting of hyper-parameters in the tunner space)
  + --gpu: The available gpus for parameters tuning.

  ```bash
  cd FuxiCTR/benchmarks
  python run_param_tuner.py --config YOUR_PATH/002/FiBiNET_criteo_x4_tuner_config_03.yaml --tag 010 --gpu 0
  ```

### Results
```python
[Metrics] logloss: 0.438573 - AUC: 0.813350
```


### Logs
```python
2020-02-27 23:21:30,831 P1862 INFO {
    "batch_norm": "False",
    "batch_size": "5000",
    "bilinear_type": "field_interaction",
    "dataset_id": "criteo_x4_001_be98441d",
    "embedding_dim": "40",
    "embedding_dropout": "0",
    "embedding_regularizer": "l2(1.e-6)",
    "epochs": "100",
    "every_x_epochs": "1",
    "hidden_activations": "relu",
    "hidden_units": "[4096, 2048, 1024, 512]",
    "learning_rate": "0.001",
    "loss": "binary_crossentropy",
    "metrics": "['logloss', 'AUC']",
    "model": "FiBiNET",
    "model_id": "FiBiNET_criteo_x4_012_90314955",
    "model_root": "./Criteo/FiBiNET_criteo/",
    "monitor": "{'AUC': 1, 'logloss': -1}",
    "monitor_mode": "max",
    "net_dropout": "0",
    "net_regularizer": "0",
    "optimizer": "adam",
    "patience": "2",
    "pickle_feature_encoder": "True",
    "reduction_ratio": "3",
    "save_best_only": "True",
    "seed": "2019",
    "shuffle": "True",
    "task": "binary_classification",
    "use_hdf5": "True",
    "verbose": "0",
    "workers": "3",
    "data_format": "h5",
    "data_root": "../data/Criteo/",
    "test_data": "../data/Criteo/criteo_x4_001_be98441d/test.h5",
    "train_data": "../data/Criteo/criteo_x4_001_be98441d/train.h5",
    "valid_data": "../data/Criteo/criteo_x4_001_be98441d/valid.h5",
    "version": "pytorch",
    "gpu": "2"
}
2020-02-27 23:21:30,834 P1862 INFO Set up feature encoder...
2020-02-27 23:21:30,834 P1862 INFO Load feature_map from json: ../data/Criteo/criteo_x4_001_be98441d/feature_map.json
2020-02-27 23:21:30,834 P1862 INFO Loading data...
2020-02-27 23:21:30,838 P1862 INFO Loading data from h5: ../data/Criteo/criteo_x4_001_be98441d/train.h5
2020-02-27 23:21:36,939 P1862 INFO Loading data from h5: ../data/Criteo/criteo_x4_001_be98441d/valid.h5
2020-02-27 23:21:38,683 P1862 INFO Train samples: total/36672493, pos/9396350, neg/27276143, ratio/25.62%
2020-02-27 23:21:38,809 P1862 INFO Validation samples: total/4584062, pos/1174544, neg/3409518, ratio/25.62%
2020-02-27 23:21:38,809 P1862 INFO Loading train data done.
2020-02-27 23:21:54,025 P1862 INFO **** Start training: 7335 batches/epoch ****
2020-02-28 01:43:27,077 P1862 INFO [Metrics] logloss: 0.440543 - AUC: 0.811105
2020-02-28 01:43:27,187 P1862 INFO Save best model: monitor(max): 0.370562
2020-02-28 01:43:30,186 P1862 INFO --- 7335/7335 batches finished ---
2020-02-28 01:43:30,247 P1862 INFO Train loss: 0.455204
2020-02-28 01:43:30,250 P1862 INFO ************ Epoch=1 end ************
2020-02-28 04:04:20,459 P1862 INFO [Metrics] logloss: 0.438986 - AUC: 0.812933
2020-02-28 04:04:20,563 P1862 INFO Save best model: monitor(max): 0.373946
2020-02-28 04:04:24,632 P1862 INFO --- 7335/7335 batches finished ---
2020-02-28 04:04:24,709 P1862 INFO Train loss: 0.448318
2020-02-28 04:04:24,711 P1862 INFO ************ Epoch=2 end ************
2020-02-28 06:24:23,362 P1862 INFO [Metrics] logloss: 0.443736 - AUC: 0.809294
2020-02-28 06:24:23,437 P1862 INFO Monitor(max) STOP: 0.365557 !
2020-02-28 06:24:23,438 P1862 INFO Reduce learning rate on plateau: 0.000100
2020-02-28 06:24:23,438 P1862 INFO --- 7335/7335 batches finished ---
2020-02-28 06:24:23,513 P1862 INFO Train loss: 0.442901
2020-02-28 06:24:23,514 P1862 INFO ************ Epoch=3 end ************
2020-02-28 08:44:06,302 P1862 INFO [Metrics] logloss: 0.532712 - AUC: 0.772564
2020-02-28 08:44:06,376 P1862 INFO Monitor(max) STOP: 0.239852 !
2020-02-28 08:44:06,376 P1862 INFO Reduce learning rate on plateau: 0.000010
2020-02-28 08:44:06,376 P1862 INFO Early stopping at epoch=4
2020-02-28 08:44:06,376 P1862 INFO --- 7335/7335 batches finished ---
2020-02-28 08:44:06,453 P1862 INFO Train loss: 0.348021
2020-02-28 08:44:06,454 P1862 INFO Training finished.
2020-02-28 08:44:06,454 P1862 INFO Load best model: /cache/zhujieming/FuxiCTR/benchmarks/Criteo/FiBiNET_criteo/criteo_x4_001_be98441d/FiBiNET_criteo_x4_012_90314955_criteo_x4_001_be98441d_model.ckpt
2020-02-28 08:44:09,581 P1862 INFO ****** Train/validation evaluation ******
2020-02-28 09:30:14,627 P1862 INFO [Metrics] logloss: 0.420199 - AUC: 0.832668
2020-02-28 09:35:55,150 P1862 INFO [Metrics] logloss: 0.438986 - AUC: 0.812933
2020-02-28 09:35:55,339 P1862 INFO ******** Test evaluation ********
2020-02-28 09:35:55,339 P1862 INFO Loading data...
2020-02-28 09:35:55,340 P1862 INFO Loading data from h5: ../data/Criteo/criteo_x4_001_be98441d/test.h5
2020-02-28 09:35:56,258 P1862 INFO Test samples: total/4584062, pos/1174544, neg/3409518, ratio/25.62%
2020-02-28 09:35:56,258 P1862 INFO Loading test data done.
2020-02-28 09:41:36,705 P1862 INFO [Metrics] logloss: 0.438573 - AUC: 0.813350


```