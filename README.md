# Pseudo-RGB FFB6D. 

## This is an implementation of FFB6D, with pseudo-RGB images as input.
To preview the MD file, press ctrl+k+v

### Run our FFB6D docker 
```bash 
sudo nvidia-docker run --gpus all --ipc=host --shm-size 50G --ulimit memlock=-1 --name swin-ffb -it --rm -v /raid/home/zl755:/workspace zhujunli/ffb6d:latest
```
or 
```bash 
sudo docker exec -it swin-ffb /bin/bash
```



### Generate LindMod Normal Angles Images 
To generate synthetic normal angles images: 
1. Open raster_triangle folder.
2. Link the Linemod to the current folder. 
```bash 
ln -s path_to_Linemod_preprocessed ./Linemod_preprocessed
```
Don't have to do it every time. 
3. Render renders_nrm/ data. For example, for phone class.
```bash 
python3 rgbd_renderer.py --cls phone --render_num 10000
```
4. Render fuse_nrm/ data. For example, for phone class.
```bash 
python3 fuse.py --cls phone --fuse_num 10000
```
To generate real/ normal angles images: Run the codes within the folder: datasets/linemod
```bash 
python -m create_angle_npy.py --cls_num your_cls_num --train_list 'train.txt' --test_list 'test.txt'
```

### Train and inference the model on YCBV dataset
0. Download codes from git.
1. Create and go into the docker container.
2. Go into the ffb6d folder, e.g.:
```bash 
cd /workspace/REPO/pose_estimation/ffb6d
```
3. To train the model, run: 
```bash 
sh scripts/train_ycb.sh
```
4. To infer the model, run:
```bash 
sh scripts/test_ycb.sh
```