## CPB: Citrus Pest Benchmark

This [work](https://arxiv.org/pdf/2004.11252.pdf) was accepted by The Agriculture-Vision Workshop in CVPR 2029.

We created a benchmark containing images divided into mite and negative classes. The images were collected via a mobile device coupled with a lens magnifier. In the acquisition process, we employa Samsung Galaxy A5 with a 13 MP camera coupled witha 60×magnifier, equipped with a white LED lighting andultraviolet LED.

To  generate  the Citrus  Pest  Database,  the  mite  images were captured at a Farm, located in the city of Rio Claro, São Paulo State, in Brazil.  The data acquisition period  was  from  March  2018  to  January  2019.   Guided  by MIP inspectors, we carried out scheduled inspections in the production unit areas, which contain up to 1000 citrus trees divided into groups arranged in lines. The inspectors chose samples from the crop lines, not near the border, to analyzethe fruits, new germinations and stem. Then, they moved onto the next thirtieth plant individuals.  We used the samples examined by the inspectors to obtain the mite images.  After completing a crop sector line, every three planting lines were examined.

We  partitioned  the  image  collection  into  three  groups, referred to as training,  validation and test,  containing approximately  60%,  20%,  and  20%  of  the  mites  from  each class totaling 6380, 2239 and 2197 images, respectively.


![Mite Images](https://github.com/edsonbollis/Weakly-Supervised-Learning-Citrus-Pest-Benchmark/blob/master/mites.png)


The training, validation and test sets are available in CSV files inside the database with the names pests_train_original.csv, pests_validation_original.csv and pests_test_original.csv. You can use the dataset with the folloing python code:


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


### Additional Information
Please cite it as
```
@article{bollis2020weakly,
  title={Weakly Supervised Learning Guided by Activation Mapping Applied to a Novel Citrus Pest Benchmark},
  author={Bollis, Edson and Pedrini, Helio and Avila, Sandra},
  journal={arXiv preprint arXiv:2004.11252},
  year={2020}
}
```

ATTN: This dataset is free for academic usage. For other purposes, please contact Edson Bollis (edsonbollis@gmail.com).
