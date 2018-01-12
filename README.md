# Domain Classifier Using BiLSTM_Attention


## Training

To train classifier, run:

```python model_training classifier_train.py --data_path=<data-path> --model=<model-name>```


	<data-path> should store "vocab_processor.bin" (vocab), "trainset.txt", "testset.txt", "validset.txt"
	
	<model-name> is the classifier type want to train, for now support "bilstm_attention_mdl" 

Configuration will be loaded automatically from `model_training/conf.py`

Training log will be stored in `model_training/log`, the model will be stored in `model/training-ckpt`

## Predict

To predict the data using trained model, run:

```python model_training classifier_predict.py --data_path=<data-path> --model=<model-name> --pred-file=<pred-file>```

	<data-path> should store "vocab_processor.bin" (vocab)
	
	<model-name> is the type of classifier to load, for now support "bilstm_attnetion_mdl"
	
	<pred-file> stores the data want to predict
	
	"--with_label" is optional. If chosed, accuracy will be calculated and wrong prediction will be logged
	
Classifier will be loaded automatically from `model/training-ckpt`

Prediction log will be stored in `bin/log`

## Export

To use the training model online, the model need to be exported for TF-Serving.

```python model_training classifier_export.py```

The script will automatically load trained models in `model/model-ckpt`

Result will be exported into `model/tfserving/1`


## TF-Serving

To start serving 

```bazel-bin/tensorflow_serving/model_servers/tensorflow_model_server --port=<port> --model_name=<model path> ```

## Client

To user client for testing tfserving.

```cd model_serving/client && python classifier_client.py ```

---

### testset Acc: 0.973
