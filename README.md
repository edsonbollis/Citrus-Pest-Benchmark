## Citrus Pest Benchmark (CPB)

This project contains the data described in 'Weakly supervised learning guided by activation mapping applied to a novel citrus pest benchmark.' This [work](https://arxiv.org/pdf/2004.11252.pdf) was published in Agriculture-Vision Workshop @ CVPR 2020.

We created a benchmark containing images divided into mite and negative classes. The images were collected via a mobile device coupled with a lens magnifier. In the acquisition process, we employ a Samsung Galaxy A5 with a 13 MP camera coupled witha 60× magnifier, equipped with a white LED lighting and ultraviolet LED.

To generate our citrus pest database, the mite images were captured at São José Farm, located in the city of Rio Claro, São Paulo State, in Brazil. The data acquisition period was from March 2018 to January 2019. Guided by MIP inspectors, we carried out scheduled inspections in the production unit areas, which contain up to 1000 citrus trees divided into groups arranged in lines. The inspectors chose samples from the crop lines, not near the border, to analyze the fruits, new germinations and stem. Then, they moved on to the next thirtieth plant individuals. We used the samples examined by the inspectors to obtain the mite images. After completing a crop sector line, every three planting lines were examined.

The dataset consists of 10,816 multi-class images categorized into seven classes: (i) 1,902 images with Red Spider mites (*Panonychus citri*, *Eutetranychus banksi*, *Tetranychus mexicanus*), the largest of all other species which produces a yellowish symptom on the leaves and fruits; (ii) 1,426 images with Phytoseiid mites (*Euseius citrifolius*, *Iphiseiodes zuluagai*), the predator mite that helps control other mites; (iii) 1,386 images with Rust mites (*Phyllocoptruta oleivora*), responsible for the rust symptom and significant crop losses; (iv) 1,750 images with False Spider mites (*Brevipalpus phoenicis*), a vector of the Leprosis virus; (v) 806 images with Broad mites (*Polyphagotarsonemus latus*), responsible for causing a white cap on the fruits; (vi) 696 images with Two-Spotted Spider mites, which do not bring significant crop losses, however, they are clearly visible in the field; and (vii) 3,455 negative images.

We partitioned the image collection into three groups, referred to as training, validation and test, containing approximately 60%, 20%, and 20% of the mites from each class totaling 6380, 2239 and 2197 images, respectively.

<p align="center">
<img src="https://github.com/edsonbollis/Citrus-Pest-Benchmark/blob/master/mites.png" width="70%" />
</p>

The training, validation, and test sets are available in CSV files inside the path of the dataset with the names `pests_train_original.csv`, `pests_validation_original.csv`, and `pests_test_original.csv`, respectively. You can use the CPB sets with the following python code:

```python

prefix = 'path'

folder = prefix + 'dataset_folder_name'

y_csv = folder + 'pests_train_original.csv'

labels= ['Negative', 'Mite']

def load_data(directory=y_csv):
    load = pd.read_csv(directory,delim_whitespace=False,header=1,delimiter=',',
                       names = ['images', labels[0], labels[1]])

    class_vet = [labels[i] for i in load['Mite']]

    load['classes'] = np.array(class_vet)
    load['classes_id'] = load['Mite'].to_numpy()

    count = 0
    print(load)
    for i in load['images']:
        if os.path.isfile(folder + i):
            count += 1
        print("Images found:", count, " Images remaining:", len(load['images']) - count)
    return load
```

See  the code for our Weakly Supervised Learning Method [here](https://arxiv.org/pdf/2004.11252.pdf).


### Citation
```
@inproceedings{bollis2020weakly,
  title={Weakly Supervised Learning Guided by Activation Mapping Applied to a Novel Citrus Pest Benchmark},
  author={Edson Bollis and Helio Pedrini and Sandra Avila},
  journal={{IEEE} Conference on Computer Vision and Pattern Recognition Workshops (CVPRW)},
  year={2020}
}
```

### Acknowledgments
E. Bollis is partially funded by CAPES (88882.329130/2019-01). H. Pedrini is partially funded by FAPESP (2014/12236-1, 2017/12646-3) and CNPq (309330/2018-1). S. Avila is partially funded by FAPESP (2013/08293-7, 2017/16246-0) and Google Research Awards for Latin America 2019. RECOD Lab. is partially supported by diverse projects and grants from FAPESP, CNPq, and CAPES. We gratefully acknowledge the donation of GPUs by NVIDIA Corporation.

ATTN: This dataset is free for academic usage. For other purposes, please contact Edson Bollis (edsonbollis@gmail.com).
