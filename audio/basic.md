# 基础

## 概念

### 采样率
对声音信号每秒的采样次数，采样率越高，声音的还原越真实。采样率单位为Hz，常见的采样率有：8000Hz、16000Hz、44100Hz、48000Hz。人类一般能够听到的声音范围：20Hz～20000Hz。根据奈奎斯特采样定理：当采样频率大于信号中最高频率的2倍时，采样后的数字信号能够完整保留原始信号的信息。

### 声道
指声音在录制或播放时，在不同空间位置采集或回放的相互独立音频信号。声道数指在录音时的音源数量，或者在播放时的扬声器数量。

### 声道布局
不同声道数对应不同声道布局。常见的声道布局有单声道(mono)、立体声道(stereo)、四声环绕、5.1声道。
+ 单声道：只有一个声道，优点数据量小，amr_nb和amr_wb默认为单声道，缺点是缺乏对声音位置定位。
+ 立体声道：一般为两个声道，由左声道、右声道组成，改善对声音位置定位的状况。
+ 四声环绕：由前左、前右、后左、后右组成，形成立体环绕。
+ 4.1声道：在四声环绕基础上，增加一个低音。
+ 5.1声道：在4.1基础上，增加一个中场声道，杜比AC3就是采用5.1声道，也就是影院宣传的杜比音效。

### 音质
声音的质量，经过编码压缩后的音频信号保真度，由音量、音高和音色组成。
+ 音量：音频的强度，数值范围0-100，静音时为0，最大值为100。Android中有提供音量增强LoudnessEnhancer，调节声音分贝值。
+ 音高：声音的音调，即音频频率或每秒变化次数。
+ 音色：音频泛音，又称为音品，不同声音表现在波形方面与众不同的特性。

### 封装格式
音频的封装格式，与视频封装格式类似，由特定格式头+媒体信息+音频轨数据组成。常见的封装格式有：mp3、m4a、ogg、amr、wma、wav、flac、aac、ape等。

### 编码协议
音频经过解封装得到的音频轨数据，也是经过编码的。常见的音频编码协议有：mp3、aac、amr_nb、amr_wb、ac3、vorbis、opus、flac、wmav2等。

### 采样数
采样数，即每帧采样的数量。在FFmpeg的AVFrame中，定义为nb_samples。

### 采样位数
采样位数，即每个采样占用多少位。在RIFF(Resource Interchange File Format)资源交换文件格式有个字段bits_per_sample表示采样位数，在FFmpeg也是用这个字段表示采样位数。

### 存储空间
音频的每秒存储空间由：采样率、声道数、每个采样位数。假设采样率为44.1k，声道数为2，采样位数为16。那么，每秒所占存储空间字节数=44100 * 2 * 16 / 8

### 帧时长
音频的帧时长=采样数 / 采样率。假设采样率为44.1k，采样数为1024。那么每帧时长约等于23ms。

### 采样格式
音频的采样格式分为大端存储和小端存储。按照符号划分有：有符号与无符号。按照类型划分有：整型与浮点型。按照存储位数划分有：8位、16位、32位、64位，都是8的倍数。