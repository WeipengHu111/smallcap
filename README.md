# replication of smallcap

** big files and model are in google drive!**

demo link: https://drive.google.com/drive/folders/103M-rFeWW99nrYBqFjdiqAsqZd0jKvZ8?usp=sharing

to run the demo, you can simply download the files and then run the jupyter notebook code

since the there are a lot of files are too big to upload in github, I place it in my google drive link

google drive link: https://drive.google.com/drive/folders/103M-rFeWW99nrYBqFjdiqAsqZd0jKvZ8?usp=sharing

my trained model is at experiment/rag_7M_gpt2/ or the main file in my google drive folder.

here some demo examples from my replicated model, you can also run the juypternote book from google drive to test it

if you would like to use your own picture to test, you may put your own picture into the data/ directory after you download it to your local


![Screenshot from 2023-12-11 21-09-56](https://github.com/WeipengHu111/replication_of_smallcap/assets/70785418/7c3c75bd-b1ec-43b5-a374-f3588b768ff6)

![Screenshot from 2023-12-11 21-09-42](https://github.com/WeipengHu111/replication_of_smallcap/assets/70785418/7db4facd-350c-4844-ac9f-184dfd41c3b9)


## Dependencies

The code was developed in Python 3.9.

```
conda create -n smallcap python=3.9
conda activate smallcap
pip install -r requirements.txt
```
## Interacting with SmallCap

Our pretrained model is available on experiment/rag_7M_gpt2/ or you can find it in the demo link. 
To use it, you also need the retrieval datastore:

```
mkdir datastore
```

Download the COCO [index](https://drive.google.com/file/d/1ZP5I-xbjaNU7cU48C_ctHd95SaA0jBHe/view?usp=sharing) and associated [captions](https://drive.google.com/file/d/1BT0Qc6g40fvtnJ_yY0aipfCuCMgu5qaR/view?usp=sharing) and place them in `datastore/`.

See `SmallCap_demo.inynb` for a demo of our pretrained model.

## Training SmallCap

<details>
<summary>Click to expand</summary>

### Data

Download the COCO Karpathy splits file `dataset_coco.json` from [here](https://www.kaggle.com/datasets/shtvkumar/karpathy-splits) and place it in `data/`.

Download all COCO images (train, val and test, 2017 version) from [here](https://cocodataset.org/#download) and place them in `data/images`. The expected naming format is twelve digits followed by a `.jpg` extension, e.g. `data/images/000000000001.jpg` for image with COCO id `1`.

### Preprocessing

At the moment CLIP models based on ResNet are not available through HuggingFace so it is necessary to also install the original CLIP implementation from [here](https://github.com/openai/CLIP):

```
pip install git+https://github.com/openai/CLIP.git
```

Extract train and val features: 

```
mkdir features
python src/extract_features.py
```

Retrieve captions

```python src/retrieve_captions.py```

### Model training

```python train.py```

Models are saved under name <rag/norag>_<num params>M, e.g. `rag_7M` for a model trained with retrieval augmentation and 7M trainable parameters.







