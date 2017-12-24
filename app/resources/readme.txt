
readme:
0.版本号: V0.7.1-Lenovo_speaker-R
1. deps_libs: duerSDK依赖的动态库
2. headers:头文件
3. resources: 资源文件，放在与duersdk同级目录或可以通过api设置resources资源文件目录
5. output_main.cpp :使用demo
6.init() 接口使用到的appid, appkey需要在度秘开放平台中申请。
7.度秘开放API文档— server端返回结果json
 https://github.com/dueros/dumi_doc


修改记录：
1:2017年3月30日 
	修改output.sh，调整打包目录结构
	修改build.sh，添加美的版本jsoncpp文件修改，解决交叉编译错误
	调整build.sh说明文档名称，从README修改为build.txt
	添加美的编译环境变量设置，语音库等

2:2017年3月31日：
    修改获取密码cuid的方法
    完善长连接获取本地bduss获取登录的流程

V0.7.1 Release logs:
1) 支持登录功能，im 长连接功能
2) 支持语音2合1, 支持度秘server V2协议 
3) 支持语音服务pid,key, server_url可配置( 调用方一般不可以修改这些参数)
4) 支持 resources, sdkconfigs 路径可设置，默认在当前可执行程序同级目录
5) 支持登录的bduss/dumiToken参数动态可设置
6) 度秘server针对之前没有返回值(response)的接口请求进行了处理解决

2017/04/11:
1) 语音speechsdk 升级到v3.0.3 版本，支持http-> https协议升级，支持dnn vad （crash问题修复）
2) Alerts 协议支持，支持Alerts Event 事件上报
3) merge 语音度秘服务预测预取功能
4) click log 日志打点字段修改,添加type = 106 类型的click log
5) Event http request 的response 消息通过 HTTP_RESPONSE 消息返回.
6) Event 上报接口实现逻辑优化，使用string 参数，不再使用char *&, int& len
7) 去除app_command的逻辑，统一走 remote_callback()(针对im长连接)

2017/04/13:
1) HttpRequest::set_url(const char *url)实现优化
2) 语音speechSDK升级到v3.0.3-20170411版本(Lenovo + Ubuntu)

2017/04/17:
1) 语音speechSDK (Lenovo版本) 修复解决drc_init()问题，解决了m3u8m,m4a无法播放的问题
2）Alerts功能，Event, status事件上报

2017/04/18:
1) 设置sdk 内写文件的根路径path
2) 设置speechsdk 写文件的根路径path
3) config.json优化--- 支持:
a) click_log_url 可设置
b) 日志输出到控制台或文件
c) event_server_url Event上报接口可设置
4）tts 音色切换功能(暂时没有调试通过)
5) 预测预取逻辑优化--- 解决服务端只返回部分包数据的情况。confirm_idx > vec_chunk_data.size()

2017/04/19:
1)语音2合1功能，可通过配置文件config.json设置
2) tts音色切换功能测试调试通过; 并且第三方不需要单独设置tts切换，在duerSDK内部已经处理。

2017/04/21
1)预测预取方案，支持配置文件可配置。
2) 更新文档 Linux_duerSDK-V2.0.1.docx
3) im长连接功能优化- login() 之前，先调用一次disconnect()

2017/04/24
1) sync_device_status, 添加device_ssid参数
2) tts音色切换的实现调用放在App层，sdk提供API

2017/04/26
1) 语音speechSDK升级到v3.0.4版本, release logs:
2) 预测预取的confirm 确认接口替换成线上接口： https://xiaodu.baidu.com/ws

2017/04/27
语音speechSDK v3.0.4 更新升级:
This release includes the following changes:
 o 构建脚本优化
 o 集成新的唤醒库(end2end)，添加WP_PARAM_KEY_ENABLE_DNN_WAKEUP开关参数
 o 増加tts透传参数字段BDS_TTS_QUEUE_SENTENCE_PARAM_ID_STRING, value为自定义值,随BDS_TTS_CMD_QUEUE_SENTENCE消息下发
 o BDS_TTS_PARAM_KEY_ONLINE_AUDIO_ENCODING_INT参数开放
 o dnn vad尾点静音等待时间缩短到500ms
 o WP_PARAM_KEY_ENABLE_DNN_WAKEUP添加

This release includes the following bugfixes:
 o WAKEUP开启log无效的问题修复
 o 修复vad 路经为空的异常退出问题
 o dnn vad修复长语音bug


V0.7.6 Release logs:
1) 添加语音度秘预测预取功能 
2) 语音speechSDK升级优化-- 开启dnn vad 远场识别功能，(唤醒词支持小度小度)
3) 支持tts音色切换功能
4) 支持可写日志文件根路径设置，支持可写日志文件名称设置
5) 支持tts合成参数透传
6) im长连接功能优化,im 长连接通信的回调统一走remote_callback()
7) Event,status上报的回调走 HTTP_RESPONSE回调
8) Alerts协议正式接口协议上线
9) 性能打点日志添加--保存在vad_ttsSynthesize.log

2017/05/02
1.语音speechsdk 升级更新到v3.0.5, 同时支持老的唤醒模型和新的唤醒模型,asr failed时，增加error_sn的输出。
  duerSDK可以在sdkconfigs/config.json中配置
2.日志输出更加规范化, 目前只输出4个日志文件：
  1) outputlog.log --- wakeup, asr, nlu输出的日志
  2) Events.log ---- 上报Event事件的日志
  3) duerServiceResult.log ---- 供QA查询识别数据，nlu数据
  4) vad_ttsSynthesize.log ---- 性能日志打点

2015/05/03
1. 语音speechsdk更新:
bdspeechsdk version:3.0.5
This release includes the following changes:
 o 识别在线请求超时时间从8秒延长到12秒
 o 同时集成hmm唤醒库和end2end唤醒库
 o PARAM_MAX_SP_PAUSE由50减少到49
 o CALLBACK_ERROR_SERIAL_NUM识别出错时，返回sn
This release includes the following bugfixes:
 o end2end唤醒库中的打分库crash修复

2.添加im 长连接调试需要的所有日志log
3.添加Events http response日志，输出到Events.log

2017/05/04
1. 设置可写文件路径功能优化
2. outputlog.log 日志文件，每100MB大小保存到一个新文件中。

2017/05/06
1.语音speechSDK 升级更新到V3.0.5.2, 主要release logs:

 o end2end唤醒模型从7M换到3M，提升唤醒库处理速度
 o vad_proxy.set_parameter(PARAM_MIN_SP_DURATION, 70);VAD设置最小门限
 o vad PARAM_HEAD_SIL_DURATION从6s延长到10s
 o tts 増加在线切换离线时，在线的错误信息（请求时间，sn, errorcode, error description）

2.语音speechSDK 升级更新到V3.0.5.3, 代码逻辑无改动，end2end唤醒模型文件回退到7MB模型文件.
3. 发送Events事件上报，在http postbody 中增加"BDUSS", 而不是通过http cookies中添加budss.

2017/05/07
1.语音speechSDK升级到V3.0.5.4，提升语音阈值

2017/05/08
1. 针对Raspberry, asr 识别切换到 wakeup 唤醒的时机优化--
   之前是asr_finish之后，现在是 chunk_end 之后
2. baidu文件夹下的所有日志文件 - baidu.log, duerServiceResult.log, vad_ttsSynthesize.log
每100MB 保存到一个新文件中，文件名 -bakup
3. 添加语音sdk 日志输出到文件中
4. 解决im sync_device_status中device_status字段为空的问题
5. 关闭dnn模型打开hmm
6. 修复语音引擎busy的bug
7. 语音sdk更新到3.0.5.5版本
8. 关闭预测预取

2017/05/09
1. 修改访问请求cookie为乱码的情况
2. 语音sdk更新到3.0.5.5

20170510 
1.im 长链接, 心跳包 timeout 后，sdk 执行
1) disconnect()
2) 5s后执行 login() 的流程

2.tts 合成 audioData 回调中有时会返回data length = -1的数据，
 针对这个做了容错处理，不向上层callback


3.合并lenovo-branch分支代码到主干

2017/05/11
1. im 长连接优化：
获取login token之后，才执行disconnect() 操作。
2. 优化BDuerMessage 内部实现逻辑

2017/05/17
1.添加预测预取后端耗时timeuse,预测预取成功标志(添加打点日志)

2017/05/22
1.修复 预测预取功能，有时没有clicklog打点日志的case
2.修复 vad_end -> duer result, 日志打点不合理的case, duer result的打点时机需要向前移
3.修复 asr_failed后，duerSDK会crash的问题
4.米雪预测预取需求功能实现逻辑优化 

2017/05/26
1.语音speechsdk 升级更新，v3.0.5.acd0976. Release logs:
1) tts进度补齐的空包数据同样返回
2) 在线标签化合成参数添加
3) tts 错误码头文件添加
4) 树梅派hmm唤醒库解决与开源snowboy库的符号冲突问题
5) 唤醒库内存泄漏修复
6) ASR错误 3001，3008，3011，timeout bug修复
7) 其他优化以及修复
2.解决网络请求中一个可能导致死锁的bug
3.init()初始化增加重试机制，最大重试次数3 ,部分解决由于
初始化失败后，度秘服务无法使用的问题。

2017/05/27
1.语音sdk v3.0.5 正式版发布，Release logs除了v3.0.5.acd0976的release logs,
还包括:
1) 返回last_speech_time为13位事件戳字符串string
2) tts 合成内部支持https连接，不需要我们单独设置 
2. 修复BDuerMessage.cpp中保存二进制文件流stream的机制，解决输入pcm音频流后，识别错误的问题。

2017/06/02
1.语音speechsdk 更新到v3.0.5.d089463, Release logs:
1) 修复tts中文无法播报的问题
2. clicklog: 增加type = 4000,4001,4002类型log,废弃type = 105,111,112类型log

2017/06/05
1. 日志文件保存按照事件戳顺序保存命名。

2017/06/14
1.修改im 长连接timeout后，会导致sdk crash 的问题。

20170619
1. 增加接口：获取当前tts 引擎音色（引擎类型）
2. 增加tts 合成失败接口回调

2017/06/22
1. init()注册初始化，总是返回成功，去除内部网络请求逻辑。

2017/07/14
1. 优化设备配对逻辑。

2017/07/15
1. 增加连续唤醒功能

2017/07/17
1. 事件Event上报body中添加 _is_from_avs_or_dcs = 1






