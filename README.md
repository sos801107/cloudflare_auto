```markdown
# 🌐 Cloudflare 优选反代IP自动更新库

欢迎使用本项目！这是一个自动化维护 Cloudflare 优选IP和反代IP的解决方案，专为网络优化需求设计。项目提供自动更新的IP订阅服务，并支持一键部署到 GitHub Pages。

[![Auto Update](https://img.shields.io/badge/自动更新-每30分钟一次-blue?logo=githubactions&logoColor=white)](https://github.com/$YOUR_USERNAME/$YOUR_REPO/actions)
[![优选IP](https://img.shields.io/badge/优选IP-每日更新-green)](https://github.com/$YOUR_USERNAME/$YOUR_REPO)
[![反代IP](https://img.shields.io/badge/反代IP-每30分钟刷新-orange)](https://github.com/$YOUR_USERNAME/$YOUR_REPO)
[![License](https://img.shields.io/badge/license-MIT-purple)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/$YOUR_USERNAME/$YOUR_REPO?style=social)](https://github.com/$YOUR_USERNAME/$YOUR_REPO)

<img src="https://user-images.githubusercontent.com/447801/189489900-9e34cd90-3a6b-47fe-9d9a-96e5d9f6d3b2.png" width="800" alt="项目示意图">

## ✨ 项目特色

- 🔄 **双重更新机制**： 
  - 优选IP（江浙沪地区）每日更新
  - 反代IP每30分钟自动刷新
- 📡 **即用型订阅链接**：
  ```text
  https://$YOUR_USERNAME.github.io/$YOUR_REPO/ip.txt
  https://$YOUR_USERNAME.github.io/$YOUR_REPO/reverse_proxy.txt
  ```
- 🤖 **全自动化管理**：
  - GitHub Actions 定时任务
  - 自动提交更新到仓库
- 🌍 **GitHub Pages 托管**：
  - 无需额外服务器
  - 全球CDN加速分发
- 📊 **性能优化**：
  - 专为江浙沪地区优化
  - 低延迟、高带宽节点

## 🚀 快速开始

### 1. 直接使用订阅地址
直接将以下订阅链接添加到您的工具中：

```text
# 优选IP（每日更新）
https://$YOUR_USERNAME.github.io/$YOUR_REPO/ip.txt

# 反代IP（每30分钟更新）
https://$YOUR_USERNAME.github.io/$YOUR_REPO/reverse_proxy.txt
```

### 2. Fork项目自定义部署
[![Fork按钮](https://user-images.githubusercontent.com/447801/189494098-c0fbbd23-7c14-4d99-ae99-8d3ba2a1d4d5.png)](https://github.com/$YOUR_USERNAME/$YOUR_REPO/fork)

1. 点击右上角 **Fork** 按钮
2. 启用 GitHub Actions：
   - 仓库设置 > Actions > 允许所有Actions
3. 启用 GitHub Pages：
   - 仓库设置 > Pages > 分支选择 `gh-pages` (/root)
4. 修改订阅地址为：
   ```text
   https://你的用户名.github.io/你的仓库名/ip.txt
   https://你的用户名.github.io/你的仓库名/reverse_proxy.txt
   ```

### 3. 工作流配置
核心自动化脚本位于 [.github/workflows/update.yml](.github/workflows/update.yml):

```yaml
name: IP Auto-Update

on:
  schedule:
    - cron: '0,30 * * * *'  # 每30分钟
  workflow_dispatch:

jobs:
  update-proxy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Get Reverse Proxy
        run: |
          curl -s "https://ipdb.api.030101.xyz/?type=bestproxy" > reverse_proxy.txt
      - name: Update Pages
        run: |
          cp ip.txt reverse_proxy.txt docs/
      - name: Commit Changes
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add .
          git commit -m "Auto-Update: $(date +'%Y-%m-%d %H:%M')"
          git push
```

## 📡 订阅文件说明

| 文件名 | 描述 | 更新频率 |
|--------|------|---------|
| `ip.txt` | 江浙沪地区优选IP | 每日一次 |
| `reverse_proxy.txt` | 全球反代IP | 每30分钟 |

文件内容格式：
```text
# 优选IP（示例）
1.0.0.1
1.0.0.2

# 反代IP（示例）
104.16.132.229
104.16.174.111
```

## 🌈 视觉组件使用

### 状态徽章
在README中添加实时状态徽章：

```markdown
![优选IP更新](https://img.shields.io/badge/优选IP-每天更新-green)
![反代IP更新](https://img.shields.io/badge/反代IP-每30分钟刷新-orange)
![最后更新](https://img.shields.io/github/last-commit/$YOUR_USERNAME/$YOUR_REPO?label=最后更新)
```

### GitHub Pages统计
```markdown
![访问统计](https://img.shields.io/badge/dynamic/json?color=blue&label=访问量&query=%24.count&url=https%3A%2F%2Fapi.github.com%2Ftraffic%2Fviews%2F$YOUR_USERNAME%2F$YOUR_REPO)
```

## ⚠️ 注意事项

1. IP列表可能会因网络状况动态变化
2. 优选IP针对江浙沪地区优化，其他地区效果可能不同
3. 请勿滥用API接口，以免触发速率限制

## 🤝 贡献支持

欢迎提交 Issue 或 PR 改进项目：
- 报告无效IP
- 建议新的优选节点区域
- 优化更新算法

> **Star ⭐** 本项目，获取最新IP资源！

[![Star按钮](https://user-images.githubusercontent.com/447801/189494098-c0fbbd23-7c14-4d99-ae99-8d3ba2a1d4d5.png)](https://github.com/$YOUR_USERNAME/$YOUR_REPO)
```

## 🔒 隐私声明

> 本项目仅提供公开网络资源，不含任何用户数据追踪功能。所有IP数据均来自公开API和Cloudflare官方节点。

---

**本项目的存在旨在为开发者提供便捷的网络优化工具，请遵守当地法律法规使用**
```
