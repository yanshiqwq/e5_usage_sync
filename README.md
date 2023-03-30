# E5 Usage Sync

> 本程序、示例配置文件以及本文档均大量使用ChatGPT编写（

---

这是一个简单的 Python 程序，用于获取多个 OneDrive 帐户的空间使用情况，并将其汇总输出到 Markdown 格式的文件中（其他纯文本格式也可以）

该程序适用于需要监控多个 OneDrive 帐户使用情况的场景

## 功能

- 获取多个 OneDrive 帐户的使用情况；
- 将不同帐户的使用情况汇总输出到 Markdown 格式的文件中；
- 可以通过命令行参数指定配置文件、输出文件和输入文件路径。

## 使用说明

1. 克隆代码仓库到本地
2. 安装程序所需的 Python 包，可使用以下命令：

```bash
pip install -r requirements.txt
```

3. 根据实际情况修改 `config.yml` 文件中的配置项，包括 `client_id`、`client_secret` 和 `refresh_tokens`；
4. 运行以下命令开始获取 OneDrive 帐户使用情况：

```bash
python e5_usage_sync.py --config config.yml --input template.md --output output.md
```

其中 `config.yml` 为配置文件路径，`output.md` 为输出文件路径，`template.md` 为输入文件路径。默认情况下，程序将从当前目录下读取 `config.yml` 文件，并将结果输出到 `output.md` 文件中，使用 `template.md` 文件作为输出文件的模板。

## 配置说明

`config.yml` 文件包含以下配置项：

- `client_id`：应用程序的客户端 ID，可在 Azure Portal 中获取；
- `client_secret`：应用程序的客户端密钥，可在 Azure Portal 中获取；
- `refresh_tokens`：包含多个 OneDrive 帐户的 `refresh_token` 和名称。

示例配置文件 `config.example.yml`：

```yaml
client_id: YOUR_CLIENT_ID
client_secret: YOUR_CLIENT_SECRET
refresh_tokens:
  - name: OneDrive1
    token: OD1_REFRESH_TOKEN
  - name: OneDrive2
    token: OD2_REFRESH_TOKEN
  - name: OneDrive3
    token: OD3_REFRESH_TOKEN
```

## 输出文件说明

程序将使用输入文件中的占位符替换为实际的 OneDrive 使用情况，然后将处理后的内容写入输出文件。占位符的格式为 `[NAME_odusage]`，其中 `NAME` 表示 OneDrive 帐户的名称。

示例输入文件：

```markdown
# OneDrive 使用情况

| 帐户 | 使用情况 |
| ---- | -------- |
| OneDrive1 | [OneDrive1_odusage] |
| OneDrive2 | [OneDrive2_odusage] |
| OneDrive3 | [OneDrive3_odusage] |
```

示例输出文件：

```markdown
# OneDrive 使用情况

| 帐户 | 使用情况 |
| ---- | -------- |
| OneDrive1 | 3.53 TB |
| OneDrive2 | 921.62 GB |
| OneDrive3 | 318.2 MB |
```

## 依赖项

- `requests`
- `json`
- `humanize`
- `yaml`
- `logging`
- `argparse`

## 许可证

本程序采用 BSD 许可证