# X3 PDF 批量转 XTC / XTCH

针对 PDF 转换后页面变黑的问题增加蒙版兼容处理，并采用无需先转换整本 PDF 的轻量级快速预览。

部分 PDF 使用了特殊蒙版或透明度效果，经过其他转换工具处理后可能出现整页发黑、局部变黑或图像显示异常。本项目基于 "srokl/xtcjsapp" (https://github.com/srokl/xtcjsapp) 改编，增加蒙版兼容模式，帮助处理这类 PDF。

与需要先加载或处理整本 PDF 才能查看转换效果的工作流程不同，本项目只渲染第一份 PDF 的第一页，再裁切顶部区域进行预览。调整图像处理参数时，还可以复用缓存的灰度图，减少重复渲染。

在线使用： https://zukuxi.github.io/x3-xtc-batch/

主要功能

- 蒙版兼容处理： 针对部分 PDF 转换后页面变黑或显示异常的问题，提供蒙版兼容模式。
- 轻量级快速预览： 只渲染第一份 PDF 的第一页，并截取顶部 528 × 792 像素区域，不需要先转换整本 PDF。
- 缓存复用： 调整抖动、对比度等图像处理参数时，复用已缓存的灰度裁切图，避免重复加载 PDF。
- 批量导入： 支持多选 PDF 文件，也可以从文件夹导入 PDF。
- 灵活合并： 可选择每 1、2、3、4、5、10 或 20 份 PDF 合并输出为一个 XTC / XTCH 文件。
- 单独输出： 每组只有 1 份 PDF 时，每份 PDF 单独输出，并在对应队列项旁显示下载按钮。
- 队列管理： 合并模式下，输出结果统一显示在队列顶部；源 PDF 列表不会重复显示输出或合并状态标签。
- 文件命名： 尽量保留连续编号。例如，"a01.pdf" + "a02.pdf" 可能输出为 "01-02.xtc"。
- 多种输出格式： 支持黑白 XTC 和四级灰度 XTCH。
- 多种图像处理选项： 提供多种抖动算法及对比度设置。
- 双语界面： 支持中文和英文。
- 本地处理： 文件仅在本机浏览器处理，不会上传至转换服务器。

蒙版兼容模式

部分 PDF 使用了特殊蒙版、透明度或图像叠加效果，直接转换时可能出现整页发黑、局部变黑或其他显示异常。

本项目增加了蒙版兼容处理选项。遇到转换结果异常的 PDF 时，可以尝试切换该模式，再查看预览效果。

注意：不同 PDF 的内部结构各不相同，不能保证所有异常文件都能通过该模式修复。建议先检查预览，再转换整份文件。

快速预览：无需先转换整本 PDF

不同于需要先处理整本 PDF 才能查看转换效果的工作流程，本工具采用轻量级预览方式。

- 只渲染第一页： 选择 PDF 后，只渲染第一份 PDF 的第一页，不需要先转换整本文件。
- 直接裁切： 将页面缩放至 528 像素宽，再截取顶部 528 × 792 像素区域作为预览。
- 预览真实处理效果： 预览会应用当前选定的输出灰度模式、抖动算法和对比度。
- 缓存复用： 程序缓存已渲染页面及灰度裁切图。调整图像处理参数时，复用缓存的灰度图，不必重新加载 PDF。
- 蒙版模式单独处理： 切换蒙版兼容模式时，会重新渲染已加载的 PDF 页面，以便检查显示效果。
- 预览不生成文件： 预览不会合并多个 PDF 页面，也不会生成 XTC / XTCH 文件。

这种方式可以先检查页面是否发黑、调整图像效果，再决定是否转换整份 PDF。

PDF 页面拼接与分页

程序按顺序处理每份 PDF 的页面，并将页面缩放至宽度 528 像素。如果缩放后的页面高度超过 792 像素，就会分成多个纵向片段处理。

这些片段会依次填入 528 × 792 的输出页面：

1. 当前片段先填充当前输出页面的剩余空间。
2. 如果片段放不下，剩余部分会继续放到下一张输出页面。
3. 同一份 PDF 的后续片段可以继续填充当前页面的剩余空间。
4. 一份 PDF 处理结束时，如果当前输出页面没有填满，就用白色补齐并输出。
5. 下一份 PDF 始终从新的输出页面开始。不同 PDF 的内容不会拼接到同一张输出页面。

程序采用逐段处理，不会先将整份 PDF 渲染成一张超长画布再切割。

图像处理选项

抖动算法

- Atkinson
- Floyd–Steinberg
- Stucki
- Ostromoukhov
- Zhou–Fang
- Sierra Lite
- Ordered
- Matt Parker
- Stochastic
- 无抖动阈值模式

对比度

- None
- Light
- Medium
- Strong
- Maximum

Stochastic 使用 Hilbert 曲线遍历像素，计算量较大。批量转换大量页面时，建议优先使用 Atkinson 或 Floyd–Steinberg。

依赖库

- PDF.js 5.4.624
- JSZip 3.10.1

以上依赖通过 cdnjs 加载。

网页工具

https://zukuxi.github.io/x3-xtc-batch/

致谢与许可

本项目改编了 "srokl/xtcjsapp" (https://github.com/srokl/xtcjsapp) 中的 XTC / XTCH 编码逻辑。原项目采用 MIT License，具体许可条款请参阅原仓库。

---

# X3 PDF Batch Converter to XTC / XTCH

Adds mask compatibility handling for PDFs that turn black after conversion, plus a lightweight preview that does not require converting the entire PDF first.

Some PDFs use special masks or transparency effects that may cause entire pages or parts of pages to appear black or render incorrectly in other conversion tools. Based on "srokl/xtcjsapp" (https://github.com/srokl/xtcjsapp), this project adds a mask compatibility mode to help handle such PDFs.

Unlike workflows that require processing an entire PDF before showing a preview, this tool renders only the first page of the first PDF and crops its top area for preview. Image-processing settings can reuse the cached grayscale crop, reducing redundant rendering.

Live demo: https://zukuxi.github.io/x3-xtc-batch/

Features

- Mask compatibility mode: Helps address black pages and rendering issues caused by certain PDF masks or transparency effects.
- Lightweight preview: Renders only the first page of the first PDF and crops the top 528 × 792 pixel area. The entire PDF does not need to be converted first.
- Cached rendering: Reuses the cached grayscale crop when dithering, contrast, or other image-processing settings change.
- Batch import: Select multiple PDFs or import PDFs from a folder.
- Flexible merging: Combine every 1, 2, 3, 4, 5, 10, or 20 PDFs into one XTC / XTCH output file.
- Individual output: When the group size is set to 1, each PDF is converted into a separate file, with a download button beside its queue item.
- Organized queue: In merge mode, output results appear together at the top of the queue, without redundant output or merge-status labels on source PDF items.
- Filename handling: Output filenames try to preserve consecutive numbering. For example, "a01.pdf" + "a02.pdf" may produce "01-02.xtc".
- Multiple output formats: Supports black-and-white XTC and four-level grayscale XTCH.
- Image processing: Includes multiple dithering algorithms and contrast settings.
- Bilingual interface: Supports Chinese and English.
- Local processing: Files are processed in your browser and are not uploaded to a conversion server.

Mask Compatibility Mode

Some PDFs use special masks, transparency, or image compositing effects. These may cause black pages, dark regions, or other rendering problems during conversion.

This project provides a mask compatibility option. If a PDF produces an abnormal result, try switching this mode and checking the preview before converting the entire file.

PDF structures vary, so this mode cannot guarantee a fix for every problematic file.

Quick Preview: No Need to Convert the Entire PDF First

Unlike workflows that require processing an entire PDF before showing a conversion preview, this tool uses a lightweight preview approach.

- First page only: After selecting PDFs, only the first page of the first PDF is rendered. The entire document does not need to be converted first.
- Direct cropping: The page is scaled to 528 pixels wide, then the top 528 × 792 pixel area is cropped for preview.
- Preview with current settings: The preview applies the selected output grayscale mode, dithering algorithm, and contrast settings.
- Cached rendering: The rendered page and grayscale crop are cached. Changing image-processing settings reuses the cached grayscale crop instead of reloading the PDF.
- Mask mode handling: Switching mask compatibility mode renders the loaded PDF page again so you can check the result.
- No output file generated: The preview does not combine multiple PDF pages or generate an XTC / XTCH file.

This lets you inspect pages for black-rendering problems and adjust image settings before converting the entire PDF.

Page Packing and Output

PDF pages are processed in order and scaled to a width of 528 pixels. Pages taller than 792 pixels are processed in vertical segments.

Segments are packed sequentially into a 528 × 792 output-page buffer:

1. Each segment fills the remaining space on the current output page.
2. If a segment does not fit, its remaining rows continue on the next output page.
3. Subsequent segments from the same PDF can fill any remaining space.
4. When a PDF finishes, any partially filled output page is padded with white and emitted.
5. The next PDF always starts on a fresh output page. Content from separate PDFs is never stitched together on the same output page.

Processing is incremental; the converter does not create one giant canvas for an entire PDF before slicing it.

Image Processing Options

Dithering Algorithms

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

Contrast

- None
- Light
- Medium
- Strong
- Maximum

Stochastic uses a Hilbert-curve traversal and is more computationally expensive. For large batches, Atkinson or Floyd–Steinberg is recommended.

Dependencies

- PDF.js 5.4.624
- JSZip 3.10.1

Both dependencies are loaded from cdnjs.

Web App

https://zukuxi.github.io/x3-xtc-batch/

Credits and License

This project adapts XTC / XTCH encoding logic from "srokl/xtcjsapp" (https://github.com/srokl/xtcjsapp), which is licensed under the MIT License. Please refer to the original repository for its license terms.
