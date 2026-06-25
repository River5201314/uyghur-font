# UKIJTor-DouyinSans 合并字体

将 **UKIJ Tor**（维吾尔文/阿拉伯文）与 **DouyinSans Bold**（中文/拉丁文）合并为一个 TrueType 字体文件，在单个字体中同时支持**维吾尔文**、**中文**和**英文**，并完整保留阿拉伯文上下文连词特性。

## 在线预览

> 打开 [`预览页`](https://uifont.netlify.app/) 查看三种文字和混合排版的交互式预览效果。

## 字体信息

| 属性 | 值 |
|---|---|
| 字体名称 | UKIJTor-DouyinSans |
| 格式 | TrueType & OpenType (.ttf & .otf) |
| 每Em单位数 | 2048 |
| 总字形数 | 8,817 |
| Unicode 字符数 | 8,411 |
| 支持文字 | 阿拉伯文（维吾尔文）、CJK 统一汉字（中文）、基础拉丁文、拉丁文扩展、西里尔文 |
| GSUB 特性 | `calt`、`fina`、`init`、`isol`、`medi`、`rlig`、`zz01`-`zz08` |
| GDEF | 999 个字形类定义（991 Base + 8 Ligature） |
| GPOS | 阿拉伯文标记定位 |

## 维吾尔语连词特性

本字体完整保留了 UKIJ Tor 的 **全部 OpenType 布局表**，确保维吾尔文文本的正确渲染：

- **上下文替代** (`calt`) - 根据上下文自动替换字形
- **词首形** (`init`) - 单词起始位置的字形形式
- **词中形** (`medi`) - 单词中间位置的字形形式
- **词尾形** (`fina`) - 单词末尾的字形形式
- **独立形** (`isol`) - 独立使用的字形形式
- **必需连字** (`rlig`) - 强制连字替换
- **自定义特性** (`zz01`-`zz08`) - UKIJ 专用排版规则

合并后已验证全部 257 个 GSUB 引用的字形和 999 个 GDEF 字形类定义完整无缺。

## 字体来源

### UKIJ Tor

- **来源**: [ukij/fonts-for-uyghur-arabic-script](https://github.com/ukij/fonts-for-uyghur-arabic-script) - `ukij-tor`（UKIJTor.ttf）
- **作者**: 维吾尔族计算机科学协会 / Tursun Sultan
- **许可证**: [LGPL 许可证](https://www.gnu.org/licenses/lgpl.html) 和 [开放字体许可证](https://scripts.sil.org/OFL)
- **说明**: 一款全面的维吾尔阿拉伯文字体，支持完整的上下文连词特性，包括词首、词中、词尾、独立形以及连字。

### DouyinSans Bold

- **来源**: [bytedance/fonts](https://github.com/bytedance/fonts) - `DouyinSans`（DouyinSansBold）
- **作者**: 北京字跳网络技术有限公司（字节跳动）
- **许可证**: [SIL 开放字体许可证 1.1](https://github.com/bytedance/fonts/blob/main/DouyinSans/OFL.txt)
- **保留字体名**: "Douyin"、"抖音"、"抖音美好"
- **说明**: 抖音品牌创意中心推出的抖音官方字体，包含 6,763 个汉字和 682 个字母数字/标点符号，风格简洁现代。

## 合并方法

使用 [fontTools](https://github.com/fonttools/fonttools) 编程合并：

1. **DouyinSans OTF 转换为 TTF**（通过三次贝塞尔到二次贝塞尔曲线转换）
2. **DouyinSans 缩放**：从 1000 UPM 缩放到 2048 UPM，匹配 UKIJ Tor 的坐标系
3. **以 UKIJ Tor 为基础字体**，保留所有 GSUB/GDEF/GPOS 表及其内部字形引用
4. **追加 DouyinSans 字形**（新增 7,817 个字形，仅 `.notdef` 发生重叠）
5. **合并 Unicode cmap**：拉丁文/CJK/西里尔文重叠字符优先使用 DouyinSans 映射
6. **验证所有 GSUB/GDEF 引用**完整（零缺失）

## 许可协议

本合并字体是两个开源字体的衍生作品，继承各自许可证：

- **维吾尔文/阿拉伯文字形及 OpenType 布局表**：按照 UKIJ Tor 原始许可证，采用 **LGPL** 和 **OFL** 授权。
- **中文/拉丁文/西里尔文字形**：按照 DouyinSans 原始许可证，采用 **SIL 开放字体许可证 1.1** 授权。

**重要说明**：保留字体名 "Douyin"、"抖音"、"抖音美好" 属于字节跳动所有，本合并字体的主名称**未使用**这些保留名称。

使用本字体前，请仔细阅读并遵守 [LGPL](https://www.gnu.org/licenses/lgpl.html) 和 [SIL OFL 1.1](https://scripts.sil.org/OFL)，尤其是在商业用途场景下。

## 文件结构

```
/
├── README.md                    # 项目说明文件
├── index.html                   # 字体在线预览页面
├── merged_ucn_font.ttf          # 合并后的字体文件
└── LICENSE                      # 许可协议详情
```

## 使用方法

### 网页端

```css
@font-face {
    font-family: 'UKIJ-DouyinSans';
    src: url('merged_ucn_font.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
}

body {
    font-family: 'UKIJ-DouyinSans', sans-serif;
}
```

### 桌面端

下载 `merged_ucn_font.ttf` 并安装到系统：
- **Windows**：右键点击 `.ttf` 文件 > "安装"
- **macOS**：双击 `.ttf` 文件 > "安装字体"
- **Linux**：复制到 `~/.local/share/fonts/` 或 `~/.fonts/`

### 示例文本

**维吾尔文**：
```
ئۇيغۇر تىلىدا سۆزلەش
بارلىق ئىنسانلار ئەركىن، ئىززەت-ھۆرمەت ۋە ھوقۇقتا باب-باراۋەر بولۇپ تۇغۇلغان.
```

**中文**：
```
这是一个支持维吾尔文、中文和英文的合并字体。
```

**英文**：
```
The quick brown fox jumps over the lazy dog.
```

## 已知限制

- DouyinSans 原始格式为 CFF/OTF，转换为 TrueType (TTF) 时使用了三次到二次贝塞尔曲线近似，可能与原始字体存在细微轮廓差异。
- `U+06A7`（三下点 Keheh，ڧ）字符在两个源字体中均不存在，合并字体中同样缺失。
- 合并过程中未保留 TrueType 提示指令（hinting），小字号渲染效果可能因系统字体渲染器而异。

## 致谢

- [UKIJ - 维吾尔族计算机科学协会](http://www.ukij.org) 创建和维护 UKIJ 字体族。
- [字节跳动 / 抖音品牌创意中心](https://github.com/bytedance/fonts) 开源抖音美好体。
- [fontTools](https://github.com/fonttools/fonttools) 和 [cu2qu](https://github.com/fonttools/cu2qu) 提供字体处理工具链。
