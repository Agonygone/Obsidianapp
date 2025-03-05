```python
import moviepy.editor as mp
import os

if __name__ == "__main__":
	#  指定文件目录
    current_address = r"D:\studying\project\python\flvTomp3\src"
    # 获取指定目录下的所有文件
    file_list = os.listdir(current_address)
    for file_address in file_list:
    	# 获取文件名(不包含后缀.flv)
        file_name = file_address.split('.')[0]
        # 拼接文件的绝对路径(dir+xxx.flv)
        file_address = os.path.join(current_address, file_address)
        print("需要转换的文件 >>>>> " + file_address)
        # 调用moviepy库的方法
        clip = mp.AudioFileClip(file_address)
        # 拼接转换后的文件路径
        file_name = file_name + '.mp3'
        out_address = os.path.join(current_address, file_name)
        print("转换后的文件 >>>>> " + out_address)
        ###  
        clip.write_audiofile(out_address)

```

```python
# 批量MP4——>MP3
from moviepy.editor import *

def changesku(inputpath):
    listdir = os.listdir(inputpath) # 获得所有文件名
    mp4namelist = [name for name in listdir if name.endswith('.mp4')]
    for file in mp4namelist:

        filepath = os.path.join(inputpath, file) # 将根路径与文件名路径组合成绝对路径
        video = VideoFileClip(filepath)
        list_filepath = list(filepath)
        list_filepath[-1] = '3'
        #判断MP3是否已存在
        if list_filepath in listdir:
            continue
        filepath = ''.join(list_filepath)
        print(filepath)
        audio = video.audio
        audio.write_audiofile(filepath)


if __name__ == '__main__':
    vediopath = 'H:\\歌曲\\【曾经家喻户晓的经典老歌】 MV合集（一）'  # 更改这里的位置
    changesku(vediopath)

```