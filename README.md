# Face Swapping to Painting

Adapt from [hififace](https://github.com/mindslab-ai/hififace) and [MSG-Net](https://github.com/zhanghang1989/PyTorch-Multi-Style-Transfer) \
Test code upload. Train code to uploaded in hififace_train profile\
Code only test in Windows while bash below writed in Linux formats. Requirement to be added later. 

### Download pre-trained Model:
Please download [hififace_opensouce_299999.ckpt](https://drive.google.com/file/d/1tZitaNRDaIDK1MPOaQJJn5CivnEIKMnB/view?usp=sharing) and [ms1mv3_arcface_r100_fp16_backbone.pth](https://1drv.ms/u/s!AswpsDO2toNKq0lWY69vN58GR6mw?e=p9Ov5d)  and store in this floder
```bash
## download bash to be added later
```
And also download model in `model/README.md` and `model/Deep3DFaceRecon_pytorch/README.md`


## Swapping face:
Swap the face in `source_image_path` to `target_image_path`.
```bash
python hififace_inference.py --gpus 0 --model_config config/model.yaml --model_checkpoint_path hififace_opensouce_299999.ckpt \
--output_image_path assets/result/swap_result.png \
--source_image_path assets/inference_samples/03_target.png \
--target_image_path assets/AF_dataset/Pablo_Picasso/111.png
```


## Style Transfer:
Transfer picture to `--style-imag` style.
```bash
python MSG_main.py eval --content-image assets/result/result.png \ 
--style-image assets/21styles/picasso_selfport1907.jpg --model models/21styles.model --content-size 256 \
--output-image assets/result/transfer_result.png
```
Pre-trained style stored in `assets/21styles` \

## HIfiface Training:
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

### Run:
```bash
python hififace_trainer.py --model_config config/model.yaml --train_config config/trainer.yaml -n hififace
```

