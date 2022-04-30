# CV_StarGAN-v2

This is the implementation for StarGAN v2, available publicly with a few changes to support the FFHQ dataset. 

StarGAN v2  
Paper - https://arxiv.org/abs/1912.01865  
Code - https://github.com/clovaai/stargan-v2  

## How to run

To run on windows, I have slight changes to the code. Also, this code supports FFHQ dataset.

### Installations and set up
Instructions to run on linux are available at the original repo, for windows use the following commands -
```
git clone https://github.com/saurabhburewar/CV_StarGAN-v2.git
cd CV_StarGAN-v2/

conda create -n stargan python=3.6.7
conda activate stargan
conda install -y pytorch=1.4.0 torchvision=0.5.0 cudatoolkit=10.0 -c pytorch

conda install x264=='1!152.20180717' ffmpeg=4.0.2 -c conda-forge  #for linux
Download "ffmpeg-4.4.1-essentials_build" from https://www.ffmpeg.org/download.html, extract and move it to C: drive and set up the path in environment variables #for windows

pip install opencv-python==4.1.2.30 ffmpeg-python==0.2.0 scikit-image==0.16.2
pip install pillow==7.0.0 scipy==1.2.1 tqdm==4.43.0 munch==2.5.0

bash download.sh ffhq-dataset
```
### Training
```
#for linux
python main.py --mode train --num_domains 2 --w_hpf 1 --lambda_reg 1 --lambda_sty 1 --lambda_ds 1 --lambda_cyc 1 --train_img_dir data/ffhq/train --val_img_dir data/ffhq/val --total_iters 100 

#for windows
python main.py --mode train --num_domains 2 --w_hpf 1 --lambda_reg 1 --lambda_sty 1 --lambda_ds 1 --lambda_cyc 1 --train_img_dir data/ffhq/train --val_img_dir data/ffhq/val --total_iters 100 --num_workers 0  #for windows
```
### Predictions
```
python main.py --mode sample --num_domains 2 --resume_iter 10 --w_hpf 1 --checkpoint_dir expr/checkpoints/ffhq --result_dir expr/results/ffhq --src_dir assets/representative/ffhq/src --ref_dir assets/representative/ffhq/ref
```
### Evaluations
```
python main.py --mode eval --num_domains 2 --w_hpf 1 --resume_iter 1 --train_img_dir data/ffhq/train --val_img_dir data/ffhq/val --checkpoint_dir expr/checkpoints/ffhq --eval_dir expr/eval/ffhq
```
