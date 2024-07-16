# Installation setup

### With conda
```bash
conda create -n swin_od python=3.8 -y
source /trinity/shared/opt/anaconda3/bin/activate swin_od
```

### With mamba
```bash
mamba create -n swin_od python=3.8 -y
source /trinity/shared/opt/mambaforge3/bin/activate swin_od
```

### Next steps
From repo root
```bash
pip install "numpy<1.24"
pip3 install torch==1.7.1+cu110 torchvision==0.8.2+cu110 -f https://download.pytorch.org/whl/torch_stable.html
pip3 install -U openmim
mim install mmcv-full==1.3.0
pip install cython==0.29.33
pip3 install -e .
pip3 install yapf==0.40.1
```

# Train

## From scratch

### Mask R-CNN
```bash
bash tools/dist_train.sh configs/swin/mask_rcnn_swin_tiny_patch4_window7_mstrain_480-800_adamw_3x_coco.py 1
```

### Mask R-CNN
```bash
bash tools/dist_train.sh configs/swin/cascade_mask_rcnn_swin_tiny_patch4_window7_mstrain_480-800_giou_4conv1f_adamw_3x_coco.py 1
```


## Finetune
TODO


# Test

### Mask R-CNN
```bash
python tools/test.py configs/swin/mask_rcnn_swin_tiny_patch4_window7_mstrain_480-800_adamw_3x_coco.py /gpfs/gpfs0/dermilov_group/checkpoints/swin_od/mask_rcnn_swin_small_patch4_window7.pth --eval bbox segm
```

### Cascade Mask R-CNN
```bash
python tools/test.py configs/swin/cascade_mask_rcnn_swin_tiny_patch4_window7_mstrain_480-800_giou_4conv1f_adamw_3x_coco.py /gpfs/gpfs0/dermilov_group/checkpoints/swin_od/cascade_mask_rcnn_swin_tiny_patch4_window7.pth --eval bbox segm
```