# macOS中的环境变量

## 加载顺序

1. `/etc/profile`
2. `/etc/paths`
3. `/etc/bashrc`
4. `~/.bash_profile` 或 `~/.bashrc`
5. `~/.bash_login`

## 加载规则

- 系统启动时加载
`/etc/profile`, `/etc/paths`, `/etc/bashrc`

- 文件存在，则后面的几个文件就会被忽略不读
`~/.bash_profile`

- bash shell打开时载入
`~/.bashrc`

## 修改环境变量

- 全局生效
`/etc/profile`, `/etc/paths`, `/etc/bashrc`

- 单个用户生效: 修改 `~/.bash_profile` 文件(推荐)
Linux: `~/.bashrc`
Mac OS: `~/.bash_profile`

- 终端内临时生效
`export NAME=VALUE`

## 删除环境变量

- 永久删除
从配置文件中删除

- 在终端内临时删除
`unset NAME`

## 查看环境变量

`env`


