# ffmpeg配置

## 安装

### 包管理器安装
```bash
sudo apt install -y ffmpeg

ffmpeg --version查看是否安装成功
```

### 源码编译安装
#### 下载源码
```bash
wget http://www.ffmpeg.org/releases/ffmpeg-5.1.2.tar.gz
tar -zxvf ffmpeg-5.1.2.tar.gz
```
#### 安装依赖
```bash
sudo apt-get install -y autoconf automake build-essential git libass-dev libfreetype6-dev libsdl2-dev libtheora-dev libtool libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev pkg-config texinfo wget zlib1g-dev libavformat-dev libavcodec-dev libswresample-dev libswscale-dev libavutil-dev libsdl1.2-dev yasm libsdl2-dev libx264-dev libx265-dev libfdk-aac-dev
```

#### 编译
```bash
chmod 777 configure
chmod 777 ffbuild/*.sh
./configure --enable-shared --prefix=/usr/local/ffmpeg --enable-gpl --enable-libx264 --enable-libx265

sudo make -j8

sudo make install
```

#### 添加安装目录的动态链接库
```bash
sudo vi /etc/ld.so.conf
行末增加/usr/local/ffmpeg/lib/
保存退出

sudo ldconfig
```

#### 添加到PATH
```bash
export PATH=/xxx/xxx/ffmpeg/build/bin/:$PATH

env检查是否生效
```

#### 验证
```bash
ffmpeg --version
```

## 使用
### CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.10)
project(ffmpeg_demo)

# 设置ffmpeg依赖库及头文件所在目录
set(ffmpeg_libs /usr/local/ffmpeg/lib)
set(ffmpeg_headers /usr/local/ffmpeg/include)

#对于find_package找不到的外部依赖库，可以用add_library添加
# SHARED表示添加的是动态库
# IMPORTED表示是引入已经存在的动态库
add_library(avutil     SHARED IMPORTED)
add_library(avcodec    SHARED IMPORTED)
add_library(avformat   SHARED IMPORTED)
add_library(avdevice   SHARED IMPORTED)
add_library(avfilter   SHARED IMPORTED)
add_library(swscale    SHARED IMPORTED)
add_library(swresample SHARED IMPORTED)
add_library(postproc   SHARED IMPORTED)

#指定所添加依赖库的导入路径
set_target_properties(avutil     PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libavutil.so)
set_target_properties(avcodec    PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libavcodec.so)
set_target_properties(avformat   PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libavformat.so)
set_target_properties(avdevice   PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libavdevice.so)
set_target_properties(avfilter   PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libavfilter.so)
set_target_properties(swscale    PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libswscale.so)
set_target_properties(swresample PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libswresample.so)
set_target_properties(postproc   PROPERTIES IMPORTED_LOCATION ${ffmpeg_libs}/libpostproc.so)

# 添加头文件路径到编译器的头文件搜索路径下
include_directories(${ffmpeg_headers})
link_directories(${ffmpeg_libs})

add_executable(ffmpeg_demo main.cpp)
target_link_libraries(${PROJECT_NAME} avutil avcodec avformat avdevice avfilter swscale swresample postproc)
```

### main.cpp
```cpp
#include <iostream>

extern "C" {
#include <libavutil/imgutils.h>
#include <libavutil/mathematics.h>
#include <libavutil/time.h>
#include <libavutil/log.h>
#include <libavutil/timestamp.h>
#include <libavutil/audio_fifo.h>

#include <libavcodec/avcodec.h>
#include <libavformat/avformat.h>
#include <libavfilter/avfilter.h>
#include <libavdevice/avdevice.h>
#include <libswresample/swresample.h>
#include <libswscale/swscale.h>
}

int main()
{
    std::cout << "_configuration : " << avcodec_configuration() << std::endl;
    return 0;
}
```

