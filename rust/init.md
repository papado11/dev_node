# init

```shell
# 安装C编译环境
apt install build-essential
# 下载安装rust编译器
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

~/.cargo/config
```toml
[source.crates-io]
replace-with = 'rsproxy-sparse'

[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"

[net]
git-fetch-with-cli = true
```