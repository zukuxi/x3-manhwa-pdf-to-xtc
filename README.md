
# X3 漫画 PDF 批量转 XTC / XTCH

**中文 | [English](#english)**

将 manhwa 和 webtoon PDF 批量转换为适用于 Xteink X3 电子阅读器的 XTC / XTCH 文件。

## 在线使用

https://zukuxi.github.io/x3-manhwa-pdf-to-xtc/

## 功能特点

- 支持批量导入多个 PDF，也支持选择文件夹。
- 支持将每 1、2、3、4、5、10 或 20 份 PDF 合并为一个输出文件。
- 支持 XTC 黑白格式和 XTCH 四级灰度格式。
- 提供蒙版兼容模式，尝试修复部分 PDF 转换后发黑的问题。
- 快速预览：渲染第一份 PDF 的第一页，缩放后截取顶部 528 × 792 区域。
- 支持多种抖动算法和对比度设置。
- 支持中文和英文界面。
- 文件在浏览器本地处理，不会上传到转换服务器。

## 页面处理规则

1. PDF 页面按宽度缩放至 528 像素。
2. 超过 792 像素的长页面会被纵向切分。
3. 页面片段依次填入 528 × 792 的输出页面。
4. 当前页面剩余空间不足时，未放入的内容会延续到下一页。
5. 每份 PDF 处理结束后，最后一页未填满的区域会补白。
6. 不同 PDF 的内容不会拼接到同一输出页。

## 支持的抖动算法

- Atkinson
- Floyd–Steinberg
- Stucki
- Ostromoukhov
- Zhou–Fang
- Sierra Lite
- Ordered
- Matt Parker
- Stochastic
- No-dither threshold mode

## 蒙版兼容模式

部分 PDF 使用特殊蒙版、透明度或叠加效果，可能导致转换结果发黑。可以尝试启用蒙版兼容模式，但不能保证修复所有 PDF。建议先检查预览效果。

## 技术依赖

- PDF.js 5.4.624
- JSZip 3.10.1

## 致谢与许可

本项目基于 [srokl/xtcjsapp](https://github.com/srokl/xtcjsapp) 改编，沿用其 XTC / XTCH 编码相关逻辑。原项目使用 MIT License。

---

<a id="english"></a>

# X3 Batch Manhwa / Webtoon PDF to XTC / XTCH

Batch convert manhwa and webtoon PDFs into XTC / XTCH files for the Xteink X3 e-reader.

## Web App

https://zukuxi.github.io/x3-manhwa-pdf-to-xtc/

## Features

- Import multiple PDF files or select a folder.
- Merge every 1, 2, 3, 4, 5, 10, or 20 PDFs into one output file.
- Supports monochrome XTC and four-level grayscale XTCH.
- Optional mask compatibility mode for PDFs that appear black after conversion.
- Fast preview using the top 528 × 792 region of the first page of the first PDF.
- Multiple dithering algorithms and contrast settings.
- Chinese and English interface.
- Files are processed locally in your browser and are not uploaded to a conversion server.

## Page Processing Rules

1. Scale each PDF page to a width of 528 pixels.
2. Split pages taller than 792 pixels into vertical segments.
3. Place segments sequentially into 528 × 792 output pages.
4. Continue remaining content on the next output page when the current page has insufficient space.
5. Pad the final incomplete output page with white space at the end of each PDF.
6. Content from different PDFs is never joined on the same output page.

## Supported Dithering Algorithms

- Atkinson
- Floyd–Steinberg
- Stucki
- Ostromoukhov
- Zhou–Fang
- Sierra Lite
- Ordered
- Matt Parker
- Stochastic
- No-dither threshold mode

## Mask Compatibility

Some PDFs use special masks, transparency, or overlay effects that may cause black output. Enable mask compatibility mode to try to handle these files. It cannot guarantee a fix for every PDF, so check the preview first.

## Dependencies

- PDF.js 5.4.624
- JSZip 3.10.1

## Credits and License

Adapted from [srokl/xtcjsapp](https://github.com/srokl/xtcjsapp), reusing its XTC / XTCH encoding logic. The original project is licensed under the MIT License.
