**电力设备类 输电线路异物检测数据集及铁路输电线路异物检测数据集**
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6d2cdb0822f445ef96b49c0b52495cb2.png)

### ⚡ 铁路输电线路异物检测数据集 信息表
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6596e0ca0b054932b536d88749bb1bee.png)


| **项目** | **详细信息** |
|---------|-------------|
| **数据集名称** | 铁路输电线路异物检测数据集（Foreign Object Detection on Railway Power Lines） |
| **总数据量** | **约 6 GB** |
| **图像总数** | **14,000+ 张**（精确为 ≥14,000） |
| **标注总数** | **40,000+ 个目标实例**（平均每图约 2.86 个异物） |
| **图像来源** | 搜索引擎爬取（真实背景图像） |
| **异物生成方式** | 通过 **图像合成（P图/PS）** 将异物贴合到输电线路上 |
| **任务类型** | 目标检测（Object Detection） |
| **适用场景** | 铁路供电系统安全监控、异物自动识别、智能巡检系统开发 |
| **标注格式** | ✅ **COCO 格式（JSON）**<br>✅ **YOLO 格式（TXT）** |
| **是否可直接训练** | ✅ 是（双格式支持，兼容主流框架） |

---
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/514847fe405f433d8d8a021490b746f5.png)

### 📦 四大类异物目标类别表

| **编号** | **类别英文名** | **中文名称** | **说明** |
|--------|----------------|--------------|--------|
| 0 | Bird Nest | 鸟巢 | 鸟类在输电线塔或绝缘子上筑巢，可能引发短路 |
| 1 | Plastic Bag | 塑料袋 | 大风天气下易飘挂至线路，造成放电或跳闸 |
| 2 | Balloon | 气球 | 节日或庆典释放的气球，轻质且易漂浮缠绕线路 |
| 3 | Floating Debris | 漂浮物 | 泛指其他轻质悬浮物（如布条、泡沫、风筝等） |

> ✅ 所有标注均基于合成图像完成，边界框精准对齐异物轮廓。

---

### 📊 数据集统计摘要

| 统计项 | 数量/说明 |
|--------|----------|
| 图像数量 | ≥14,000 张 |
| 标注实例数 | ≥40,000 个 |
| 平均每图目标数 | ~2.86 个 |
| 图像分辨率 | 多样（因来自搜索引擎，尺寸不一，常见为 1920×1080 或更高） |
| 标注精度 | 高（人工精修合成，边界清晰） |
| 是否真实场景 | ❌ 否（背景真实，异物为合成添加） |
| 是否存在遮挡 | ✅ 是（部分异物被电线杆、绝缘子遮挡） |
| 是否多尺度 | ✅ 是（异物大小变化大，从小型碎片到大型塑料袋） |

---

### 📁 博主建议推荐数据组织结构（COCO + YOLO 双格式）

```bash
railway_foreign_object_dataset/
├── images/
│   ├── train/        # 训练集图像（约 11,200+）
│   └── val/          # 验证集图像（约 2,800+）
├── labels/
│   ├── train/        # YOLO TXT 标注文件
│   └── val/
├── annotations/
│   ├── instances_train.json   # COCO 格式训练集
│   └── instances_val.json     # COCO 格式验证集
├── dataset.yaml       # YOLO 配置文件
└── README.md
```

---

### 🧾 `dataset.yaml` 配置文件示例

```yaml
# dataset.yaml
path: ./railway_foreign_object_dataset
train: ./images/train
val: ./images/val

# 类别数量
nc: 4

# 类别名称（按编号顺序）
names:
  - Bird_Nest
  - Plastic_Bag
  - Balloon
  - Floating_Debri
```

---

### ✅ 数据集核心优势

| 优势 | 说明 |
|------|------|
| ✅ **大规模标注数据** | 1.4万张图像 + 4万+标注，适合深度学习训练 |
| ✅ **双格式支持** | 同时提供 COCO 和 YOLO 格式，适配多种检测框架 |
| ✅ **聚焦铁路安全** | 专为铁路供电系统设计，具有明确应用场景 |
| ✅ **四大关键异物类型** | 覆盖最常见导致跳闸的空中异物 |
| ✅ **高标注质量** | 合成图像确保异物位置准确、边界清晰 |

---

### ⚠️ 使用注意事项

| 注意事项 | 说明 |
|--------|------|
| 🔍 **非完全真实数据** | 异物为 P 图合成，可能存在域偏移（domain shift），建议结合真实数据微调 |
| 🔄 **需做数据增强** | 建议使用旋转、缩放、色彩扰动等增强提升泛化能力 |
| 🎯 **关注小目标检测** | 部分异物较小（如远处气球），建议使用 Mosaic 增强和高分辨率输入 |
| 🧪 **部署前实测验证** | 在真实巡检图像上测试模型性能，防止过拟合合成特征 |

---

### 🎯 典型应用场景

| 应用场景 | 功能实现 |
|--------|----------|
| **铁路智能巡检** | 无人机/摄像头自动识别输电线异物 |
| **供电安全保障** | 实时预警鸟巢、塑料袋等隐患，防止跳闸事故 |
| **AI辅助运维** | 减少人工巡检成本，提高响应速度 |
| **模型预研与测试** | 作为基准数据集用于异物检测算法对比 |

---

使用 **YOLOv8** 进行高效训练。

由于图像为“P图合成”，需注意：
- 可能存在背景不自然、光照/尺寸不合理等问题
- 建议在训练中加入强数据增强以提升泛化能力

---

## ✅ 一、数据集结构与 `data.yaml` 配置

### 1. 推荐目录结构

```
railway_foreign_object/
├── images/
│   ├── train/      # ~11200 张 (80%)
│   └── val/        # ~2800 张 (20%)
├── labels/
│   ├── train/
│   └── val/
└── data.yaml       # 数据集配置文件
```

> 📌 建议按 **8:2 划分训练集和验证集**

---

### 2. 创建 `data.yaml`

```yaml
# data.yaml
train: ./railway_foreign_object/images/train
val: ./railway_foreign_object/images/val

# 类别数量
nc: 4

# 类别名称（必须与标签中 class_id 一致）
names:
  - bird_nest          # 鸟巢
  - plastic_bag        # 塑料袋
  - balloon            # 气球
  - floating_debris    # 漂浮物
```

> ⚠️ 注意：
> - 所有 `.txt` 文件必须与图像同名。
> - 每行格式为：`class_id x_center y_center w h`（归一化到 [0,1]）
> - 确保你的 YOLO 标签中的 `class_id` 从 `0` 开始连续编号

---

## ✅ 二、环境准备（推荐 Anaconda）

```bash
# 创建虚拟环境
conda create -n railway_det python=3.9
conda activate railway_det

# 安装 PyTorch（根据你的 CUDA 版本选择）
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# 安装 YOLOv8 和依赖
pip install ultralytics opencv-python matplotlib tqdm pandas

# 验证CUDA是否可用
python -c "import torch; print(torch.cuda.is_available())"  # 应输出 True
```

---

## ✅ 三、自动划分数据集脚本（如果尚未划分）

```python
# split_railway_dataset.py
import os
import random
import shutil
from pathlib import Path

def split_dataset(image_dir, label_dir, output_dir, train_ratio=0.8):
    image_dir = Path(image_dir)
    label_dir = Path(label_dir)
    output_dir = Path(output_dir)

    # 支持 jpg, png, jpeg
    images = list(image_dir.glob("*.jpg")) + \
             list(image_dir.glob("*.png")) + \
             list(image_dir.glob("*.jpeg"))

    random.shuffle(images)

    train_size = int(len(images) * train_ratio)
    train_images = images[:train_size]
    val_images = images[train_size:]

    # 创建目录
    for folder in ['images/train', 'images/val', 'labels/train', 'labels/val']:
        (output_dir / folder).mkdir(parents=True, exist_ok=True)

    # 复制图像和标签
    for img in train_images:
        shutil.copy(img, output_dir / 'images' / 'train' / img.name)
        label = label_dir / f"{img.stem}.txt"
        if label.exists():
            shutil.copy(label, output_dir / 'labels' / 'train' / label.name)

    for img in val_images:
        shutil.copy(img, output_dir / 'images' / 'val' / img.name)
        label = label_dir / f"{img.stem}.txt"
        if label.exists():
            shutil.copy(label, output_dir / 'labels' / 'val' / label.name)

    print(f"✅ 铁路异物数据集划分完成！")
    print(f"   训练集: {len(train_images)} 张")
    print(f"   验证集: {len(val_images)} 张")

# 使用示例
split_dataset(
    image_dir='raw/images',
    label_dir='raw/labels_yolo',
    output_dir='railway_foreign_object'
)
```

---

## ✅ 四、完整 YOLOv8 训练代码（支持多GPU）

```python
# train.py
from ultralytics import YOLO
import torch

# 设置设备（自动检测 GPU）
device = 'cuda' if torch.cuda.is_available() else 'cpu'
print(f"Using device: {device}")

# 加载预训练模型（推荐使用 yolov8m 或 yolov8l 提升小目标检测性能）
model = YOLO('yolov8m.pt')  # 可选: yolov8s.pt, yolov8l.pt, yolov8x.pt

# 开始训练
results = model.train(
    data='railway_foreign_object/data.yaml',   # 数据配置文件
    imgsz=640,                                 # 输入尺寸（若异物较小可尝试 800）
    epochs=150,                                # 训练轮数
    batch=32,                                  # 批次大小（根据显存调整）
    name='yolov8m_railway_foreign',
    project='runs/railway',
    device=device,
    workers=8,                                 # 数据加载线程
    optimizer='AdamW',                         # 更稳定优化器
    lr0=0.001,                                 # 初始学习率
    momentum=0.937,
    weight_decay=0.0005,
    patience=30,                               # 早停：30轮无提升则停止
    save_period=10,                            # 每10轮保存一次
    exist_ok=True,
    augment=True,                              # 启用Mosaic/HSV增强
    mosaic=1.0,                                # Mosaic概率
    mixup=0.1,                                 # MixUp增强
    copy_paste=0.1,                            # Copy-Paste增强（对合成数据特别有效）
    close_mosaic=20,                           # 最后20轮关闭Mosaic
    amp=True,                                  # 混合精度训练
    val=True                                   # 每轮验证
)

print("✅ 铁路输电线路异物检测模型训练完成！")
```

---

## ✅ 五、关键参数说明（针对“P图合成”数据优化）

| 参数 | 推荐值 | 说明 |
|------|--------|------|
| `imgsz` | `640` 或 `800` | 若异物小建议 `800` |
| `batch` | `16~64` | 显存越大越好 |
| `epochs` | `100~200` | 充分训练避免欠拟合 |
| `optimizer` | `AdamW` | 比SGD更稳定 |
| `lr0` | `0.001` | 初始学习率 |
| `augment` | `True` | 启用增强对抗过拟合 |
| `mosaic`, `mixup`, `copy_paste` | `1.0, 0.1, 0.1` | 强增强组合，提升泛化性 |
| `close_mosaic` | `20` | 后期关闭提升稳定性 |

> 💡 **特别提示**：由于是 P 图合成数据，强烈建议开启 `copy_paste` 增强，它会随机粘贴物体到新背景，模拟真实场景。

---

## ✅ 六、模型验证（评估性能）

```python
from ultralytics import YOLO

# 加载最佳模型
model = YOLO('runs/railway/yolov8m_railway_foreign/weights/best.pt')

# 在验证集上评估
metrics = model.val(
    data='railway_foreign_object/data.yaml',
    batch=32,
    imgsz=640,
    device='cuda',
    project='val_results',
    name='railway_val',
    save_json=True
)

# 输出关键指标
print(f"mAP@0.5:       {metrics.box.map:.4f}")
print(f"mAP@0.5:0.95:  {metrics.box.map50_95:.4f}")
print(f"Precision:     {metrics.box.precision:.4f}")
print(f"Recall:        {metrics.box.recall:.4f}")
print(f"F1 Score:      {metrics.box.f1.mean():.4f}")
print(f"FPS:           {metrics.speed['inference']:.2f}")
```

---

## ✅ 七、推理代码（图像、视频、摄像头）

### 1. 单张图像推理

```python
results = model.predict(
    source='test_foreign.jpg',
    conf=0.3,
    iou=0.5,
    show=False,
    save=True,
    project='inference_output',
    name='demo'
)

# 可视化结果
for r in results:
    im_array = r.plot()
    im = im_array[:, :, ::-1]  # BGR to RGB
    cv2.imshow('Foreign Object Detection', im)
    cv2.waitKey(0)
cv2.destroyAllWindows()
```

### 2. 视频或实时流推理

```python
# 视频文件
model.predict(source='drone_video.mp4', show=True, save=True)

# 实时摄像头
model.predict(source=0, show=True, conf=0.4)
```

### 3. 批量推理整个文件夹

```python
model.predict(
    source='railway_foreign_object/images/val',
    save=True,
    project='batch_infer',
    name='val_results'
)
```

---

## ✅ 八、模型导出（用于部署）

```python
# 导出为 ONNX（通用部署）
model.export(format='onnx', dynamic=True, opset=13)

# 导出为 TensorRT（NVIDIA GPU 高性能）
# model.export(format='engine', device=0)

# 导出为 TorchScript
model.export(format='torchscript')
```

---

## ✅ 九、可视化训练过程

训练完成后查看：
- `runs/railway/yolov8m_railway_foreign/results.png` → mAP、loss 曲线
- `confusion_matrix.png` → 分类准确性
- `val_batch*.jpg` → 检测效果示例

启动 TensorBoard：
```bash
tensorboard --logdir runs/railway
```

以上文字及代码仅供参考。

---

