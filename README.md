极简 mpv 配置，专为 1080P Anime 优化，适用于 macOS、Linux、Windows

## 目录结构

```
mpv/
├── input.conf          # 快捷键绑定
├── mpv.conf            # 主配置文件
├── README.md
├── .gitignore
├── saved-props.json    # 持久化属性（音量、位置等）
├── fonts/              # UI 字体
│   ├── MaterialIconsRound-Regular.otf
│   └── uosc_textures.ttf
├── script-opts/        # 脚本配置
│   ├── console.conf
│   ├── playlistmanager.conf
│   ├── stats.conf
│   ├── thumbfast.conf
│   └── ytdl_hook.conf
├── scripts/            # Lua 脚本
│   ├── copy_image.lua          # 复制当前画面
│   ├── playlistmanager.lua     # 播放列表管理
│   ├── save_global_props.lua   # 保存全局属性
│   ├── slicing_copy.lua        # 切片复制
│   ├── thumbfast.lua           # 缩略图预览
│   └── uosc/                   # 现代化 UI 框架
│       └── main.lua
├── shaders/            # GLSL 着色器
│   ├── Anime4K_Restore_CNN_L.glsl
│   ├── Anime4K_Restore_CNN_M.glsl
│   ├── Anime4K_Restore_CNN_S.glsl
│   ├── Anime4K_Upscale_CNN_x2_L.glsl
│   ├── Anime4K_Upscale_CNN_x2_M.glsl
│   ├── Anime4K_Upscale_CNN_x2_S.glsl
│   └── Anime4K_Upscale_Original_x2.glsl
└── watch_later/        # 续播数据（gitignore 忽略）
```

## 快捷键速查表

### 播放控制

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `SPACE` | 播放/暂停 | cycle pause |
| `q` | 退出播放器 | quit |
| `l` | A-B 循环点 | 设置/清除 A-B 循环点 |
| `L` | 单曲循环开关 | cycle-values loop-file "inf" "no" |
| `,` | 上一帧 | frame-back-step |
| `.` | 下一帧 | frame-step |
| `←` | 后退 5 秒 | seek -5 |
| `→` | 前进 5 秒 | seek +5 |
| `↓` | 后退 60 秒（精准） | seek -60 exact |
| `↑` | 前进 60 秒（精准） | seek +60 exact |
| `<` | 上一个文件 | playlist-prev |
| `>` / `ENTER` | 下一个文件 | playlist-next |
| `ESC` | 退出全屏 | set fullscreen no |
| `Alt+←` | 上一章节 | add chapter -1 |
| `Alt+→` | 下一章节 | add chapter +1 |
| `Shift+←` | 跳到前一条字幕 | sub-seek -1 |
| `Shift+→` | 跳到下一条字幕 | sub-seek +1 |

### 播放速度

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `1` | 常速 | set speed 1 |
| `2` | 2 倍速 | set speed 2 |
| `3` | 3 倍速 | set speed 3 |
| `4` | 4 倍速 | set speed 4 |
| `j` | 倍速 +0.5 | add speed +0.5 |
| `k` | 倍速 -0.5 | add speed -0.5 |

### 音频

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `m` | 静音切换 | cycle mute |
| `Ctrl+a` | 音轨循环 | cycle audio |
| `-` | 音量减 2% | add volume -2 |
| `=` | 音量加 2% | add volume +2 |

### 视频 / 显示

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `f` | 全屏切换 | cycle fullscreen |
| `t` | 置顶切换 | cycle ontop |
| `Ctrl+h` | 硬解开关 | cycle-values hwdec "no" "auto" |

### 字幕

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `v` | 字幕显隐 | cycle sub-visibility |
| `Ctrl+s` | 字幕轨道循环 | cycle sub |
| `e` | 切换第二字幕轨道 | cycle secondary-sid |
| `u` | 强制/关闭 ASS 样式 | cycle-values sub-ass-override "force" "no" |
| `z` | 字幕上移 1 像素 | add sub-pos -1 |
| `Z` | 字幕下移 1 像素 | add sub-pos +1 |
| `x` | 字幕缩小 10% | add sub-scale -0.1 |
| `X` | 字幕放大 10% | add sub-scale +0.1 |
| `d` | 字幕提前 0.1 秒 | add sub-delay -0.1 |
| `D` | 字幕延后 0.1 秒 | add sub-delay +0.1 |

### 截图

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `s` | 截图（含字幕） | screenshot |
| `S` | 截图（纯画面） | screenshot video |
| `Alt+s` | 截图（窗口含 OSD） | screenshot window |

### 脚本功能

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| `` ` `` | 打开控制台 | script-binding console/enable |
| `i` | 临时显示统计信息 | script-binding stats/display-stats |
| `I` | 统计信息开关 | script-binding stats/display-stats-toggle |
| `p` | 标记切片起点/终点 | script-binding slicing_mark |
| `P` | 清除切片标记 | script-binding clear_slicing_mark |
| `c` | 复制当前画面到目标目录 | script-binding copy-current-image |
| `Shift+ENTER` | 显示播放列表 | script-binding playlistmanager/showplaylist |

### 鼠标操作

| 快捷键 | 功能 | 说明 |
|--------|------|------|
| 左键单击 | 无操作（防误触） | ignore |
| 左键双击 | 全屏切换 | cycle fullscreen |
| 右键单击 | 播放/暂停 | cycle pause |
| 侧键后退 | 上一个文件 | playlist-prev |
| 侧键前进 | 下一个文件 | playlist-next |

### GLSL 着色器

| 快捷键 | 着色器 |
|--------|--------|
| `Alt+1` | 清除所有着色器 |
| `Alt+2` | Anime4K_Restore_CNN_S |
| `Alt+3` | Anime4K_Upscale_CNN_x2_S |
| `Alt+4` | Anime4K_Restore_CNN_M |
| `Alt+5` | Anime4K_Upscale_CNN_x2_M |

> 注释掉的快捷键（如书签菜单 `B` / `b`）需配合对应脚本启用，详见 `input.conf`。
