# Hififace Training

Adapt from [hififace](https://github.com/mindslab-ai/hififace)


### Installation:
```bash
git clone https://github.com/Peternal/hififace_train.git 
cd hififace_train
git clone https://github.com/sicxu/Deep3DFaceRecon_pytorch && git clone https://github.com/NVlabs/nvdiffrast && git clone https://github.com/deepinsight/insightface.git
cp -r insightface/recognition/arcface_torch/ Deep3DFaceRecon_pytorch/models/
cp -r insightface/recognition/arcface_torch/ ./model/
rm -rf insightface
cp -rf 3DMM/* Deep3DFaceRecon_pytorch
mv Deep3DFaceRecon_pytorch model/
rm -rf 3DMM
cd nvdiffrast
pip install .
cd ..
pip install requirements.txt
```
Follow [Deep3DFaceRecon_pytorch](https://github.com/sicxu/Deep3DFaceRecon_pytorch) to construct directory Deep3DFaceRecon_pytorch.\
Download [ms1mv3_arcface_r100_fp16_backbone.pth](https://1drv.ms/u/s!AswpsDO2toNKq0lWY69vN58GR6mw?e=p9Ov5d) and store in hififace_train folder.\
Download our [datasets](https://drive.google.com/file/d/1hPqQppICS6t3PF2ftTeRdkJFXxIeE4N9/view?usp=sharing) and extract it to hififace_train folder.

### Training:
You can modify the hyperparaneters in [config/model.yaml](config/model.yaml) and [config/trainer.yaml](config/trainer.yaml)

#### Run:
```bash
python hififace_trainer.py --model_config config/model.yaml --train_config config/trainer.yaml -n hififace
```

