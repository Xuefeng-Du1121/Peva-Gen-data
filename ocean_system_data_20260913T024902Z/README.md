# Ocean System 海洋数据包

本包仅复制已有、可读取的历史数据，不含模型权重、预测结果、账号凭据或 2026 年九月盲测资料。目录结构保留来源项目相对路径。实际文件、变量、坐标范围、时间范围和 SHA-256 见 manifest.json；未恢复的候选文件见 skipped_cloud_files。

## 数据类别

- `data_platform/data/raw/noaa_gdp/`：NOAA GDP 实测漂流器轨迹的区域、年份子集，CSV 包含位置、速度和部分水帆属性。第二行是单位行，读取时应跳过；缺失属性不得当作已知状态。年度文件与月度文件可能重叠，合并前按漂流器身份与时间去重。
- `data_platform/data/raw/environment/copernicus/`：2018 年 1 月海区洋流与波浪产品子集。多源洋流产品包含 total、Ekman 和潮流分量；total 不应再次与其已包含分量相加。
- `data/demo/`：2024 年 8 月 ERA5 风场再分析与 HYCOM 洋流模型归档子集。
- `runtime-data/demo/`：2024 年 8 月 Copernicus 洋流、Stokes 漂移、潮流与总流，以及 ERA5 风／Stokes 场。为前端演示转换或降采样后的 NetCDF，具体处理见 provenance.json 和各文件属性。Copernicus 总流仅用于校验，不能再加到 current + Stokes + tide 上。

## 使用边界

环境场来自真实公共数据产品，但不等于每个网格点均为现场直接实测。实测漂流轨迹与再分析／模型环境场应分别标识。数据是区域和时段子集，不是完整全球长期数据集；不同文件不一定同期同域，配对前检查 manifest.json 和时间、坐标、深度、单位及缺测值。

本数据包用于数据探索和接口接入，不自动构成新的训练集、独立测试集或预报能力证明。使用 NOAA、ECMWF/ERA5、HYCOM、Copernicus 产品时需保留来源归属，并按对应产品许可和引用要求使用。

校验：在本目录执行 `sha256sum -c SHA256SUMS`。
