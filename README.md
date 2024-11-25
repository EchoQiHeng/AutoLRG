# AutoLRG

### News
* **`November 19, 2024`:** Code will be released after the paper is accepted.

#### AutoLRG: A Two-stage Framework for Automated Lane-Level Road Graph Construction

<div align="center">
  <img src="https://github.com/EchoQiHeng/AutoLRG/blob/main/figure1.png">
</div>


## Getting Started

AutoLRG is essentially a sequential model comprising two different tasks. Since the later stage is susceptible to the predictions from the previous stage, we adopt a teacher forcing training strategy to enhance model convergence and reduce cumulative errors. We aim for the segmentation network in the first stage to accurately predict the position and direction of the lane centerlines, which has led us to incorporate a multi-source data fusion module in the segmentation network. Additionally, during the training of the second stage, the lane decoder’s inputs are derived from ground-truth labels to enable guided learning from the "teacher." This approach ensures the extraction of potential lane vertex coordinates and instance information from the predicted masks, facilitating the development of the lane decoder and intersection topology construction module.

<div align="center">
  <img src="https://github.com/EchoQiHeng/AutoLRG/blob/main/figure2.png">
</div>

### Stage 1: Lane Centerline Segmentation Based on Multi-Source Data Fusion

```
python dir_pspnet_fus.py /path/to/urbanlanegraph/dataset/ /path/to/raw/output <city_name> <split>
```
The parameter `<city_name>` can be either of `miami`, `paloalto`, `pittsburgh`, `austin`, `washington`, `detroit`.
The parameter `<split>` can be either of `train`, `val`.

### Stage 2: Lane-Level Road Graph Construction

Train Lane Decoder with 2 GPUs.
```
./tools/dist_train.sh ./projects/configs/LaneGraph/lanegraph.py 2
```
Run regulation-constrained intersection topology construction module.
```
python topo.py ./projects/configs/LaneGraph/lanetopo.py
```

### Installing

### Step-by-step installation instructions

Following https://github.com/jzuern/lanegnn/tree/main?tab=readme-ov-file (Stage 1)
Following https://mmdetection3d.readthedocs.io/en/latest/getting_started.html#installation (Stage 2)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

