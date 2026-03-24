# Imas-SP-Texture-Patch-CN
> Chinese High-Resolution Texture Pack for *The Idolmaster SP* on PPSSPP.
>
>  PSP 游戏[《偶像大师SP》汉化补丁](http://sp.idolmaster.top/) 配套 PPSSPP高清纹理包

## 📑 目录



## ✨ 项目简介

本项目基于 PPSSPP 的纹理替换功能，通过 Hash 映射将原始低分辨率贴图替换为高清贴图，提升偶像大师SP的游戏体验。

![Preview Texture](https://picui.ogmua.cn/s1/2026/03/24/69c1c927149b7.webp)

### ⚠️ 项目状态

当前纹理包尚未完善，覆盖率仍在持续优化中。由于PSP游戏贴图的特性，PPSSPP需要在不同的场景才能Dump对应的纹理，由于偶像大师SP：

- 游戏场景众多，贴图分散加载
- 同一贴图可能对应多个 Hash（裁剪 / 缩放等原因，可参考：[Texture sizes on the PSP](https://github.com/hrydgard/ppsspp/wiki/Texture-replacement-ini-syntax#texture-sizes-on-the-psp)）

因此**非常依赖游戏众包形式来补全纹理映射关系**，我们非常希望你能在游玩中开启导出纹理，并为本项目[提交Pr](#如何参与)

### 🎮 支持游戏

- ULJS00167 — 完美之日 / Perfect Sun
- ULJS00168 — 惊奇之星 / Wandering Star
- ULJS00169 — 思念之月 / Missing Moon

### 🚀 使用方法 

- 克隆或下载本项目文件

- 启用 PPSSPP 纹理功能：PPSSPP工具→开发者工具，勾选保存新纹理和纹理替换

- 在PPSSPP程序目录`memstick\PSP\`目录下找到`TEXTURES`文件夹，进入（如果没有`TEXTURES`则新建一个）；在`TEXTURES`下建立三个文件夹（`ULJS00167,ULJS00168,ULJS00169`）

- 将本项目中的全部文件和目录整体复制到三个文件夹中，即可分别激活三部游戏的高清纹理侧载

  ![Folder-Sturcture](https://picui.ogmua.cn/s1/2026/03/24/69c1cc12b0499.webp)

<a id="如何参与"></a>

## 🤝 如何参与

> 🚨 当前最缺的是：textures.ini 中的纹理映射关系（Hash → HD Texture）
>
> 👏 同样欢迎补充高清分辨率的UI、背景贴图
>
> 👉 人物、场景3D模型贴图不能进行替换（请忽略这些Dump纹理）
>
> 👉 **哪怕只贡献一个场景，也非常有价值！**

### 🧩 贡献流程

1. 游玩不同剧情/场景，留意未能高清化的对话文字、背景
2. 收集 `new/` 目录中的低分辨率贴图（可以按照修改时间排序快速查找）
3. 找到`bg/`，`font/`对应高清贴图
4. 更新 `textures.ini`（可以添加适量的注释）

#### ✍️ 纹理包目录说明

```
├─textures.ini
├─bg/
│  ├─down/
│  └─up/
└─font/
```

- textures.ini：映射描述文件（为参与项目的主要的修改和提交Pr文件）
- bg/up/：背景贴图上半部分，后缀0（接受补充Pr）
- bg/down/：背景贴图下半部分，后缀1（接受补充Pr）
- font/：高清字模（不接受Pr）

#### 📌 示例1（背景纹理）

游戏中某个场景，背景图片为低分辨率，在`new/`目录中按照修改时间找到对应的`png`图片文件（由于裁剪原因，可能存在两张图片，一张上半部分，一张下半部分）

```
00000000d873987ff1b4081c.png
00000000d873957fa7e64757.png
```

在高清纹理目录的`bg\up\`和`bg\down`中，找到对应的高清贴图为

```
b2d_town_shibuya0_0.png
b2d_town_shibuya0_1.png
```

在`textures.ini`中添加以下行和注释

```
# 涩谷十字路口
00000000d873987ff1b4081c = bg/up/b2d_town_shibuya0_0.png
00000000d873957fa7e64757 = bg/down/b2d_town_shibuya0_1.png
```

#### 📌 示例2（字体纹理）

游戏中某个场景，对话图片为低分辨率，可以在`font/`目录中找到对应的字体贴图，进行添加

### ✅ Pull Request 规范

`textures.ini`以下部分不可修改

```
[options]
version = 1
hash = xxh64             # options available: "quick", xxh32 - more accurate, but much slower, xxh64 - more accurate and quite fast, but slower than xxh32 on 32 bit cpu's
ignoreMipmap = true      # Usually, can just generate them with basisu, no need to dump.
reduceHash = true       # Unsafe and can cause glitches in some cases, but allows to skip garbage data in some textures reducing endless duplicates as a side effect speeds up hashing as well, requires stronger hash like xxh32 or xxh64
ignoreAddress = true    # Reduces duplicates at the cost of making hash less reliable, requires stronger hash like xxh32 or xxh64. Basically automatically sets the address to 0 in the dumped filenames.

[games]
# Used to make it easier to install, and override settings for other regions.
# Files still have to be copied to each TEXTURES folder.
ULJS00169 = textures.ini
ULJS00168 = textures.ini
ULJS00167 = textures.ini
```

- [x] 路径正确
- [x] 分类清晰（bg / font 等）
- [x] 推荐提供简要注释对场景进行说明

### ❗ 提交Pr的方式

- [x] 我们接受Github Pull Request形式提交
- [x] 如果你不熟悉 Git，也可以加入QQ群，以群文件或消息的形式进行贡献

## 💬 社区交流 | Community

QQ 群：591676099

## ⚠️ 免责声明 | Disclaimer

- 仅用于学习与交流
- 不包含游戏本体
- 请合法获取游戏