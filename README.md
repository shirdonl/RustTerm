# Rust跨平台终端操作库

当Rust语言的终端库只为UNIX系统编写时，您是否曾感到失望？

rustterm提供了清除、输入处理、样式设置、光标移动和终端操作

Windows和UNIX系统。

rusterm的目标是简单且易于调用代码。通过rustterm的简单性，您不必

担心你工作的平台。

这个机箱支持所有的UNIX和Windows终端，直到Windows7（不是所有的终端都经过测试， 
查看 [Tested Terminals](#tested-terminals) 获取更多信息).

Tips:作者《Go Web编程实战派》出版了，促销活动中，想学Go Web编程的朋友，欢迎京东当当购买!
当当（🔥🔥🔥🔥🔥🔥 活动抢购中......）：http://product.dangdang.com/29225055.html
京东（🔥🔥🔥🔥🔥🔥 活动抢购中......）：https://item.jd.com/13200972.html

## 目录 

* [特色](#特色)
    * [已经测试的终端](#已经测试的终端)
* [入门](#入门)
    * [功能标志](#功能标志)
* [贡献](#贡献)    

## 特色

- 跨平台
- 多线程（发送、同步）
- 详细文件
- 依赖关系很少
- 完全控制输出缓冲区
- 光标（功能“Cursor”） 
    - 将光标移动N次（上、下、左、右）
    - 设置/获取光标位置
    - 存储光标位置，稍后恢复
    - 隐藏/显示光标
    - 启用/禁用光标闪烁（并非所有终端都支持此功能）
- 样式化输出（功能“style”）
    - 前景色（16基色）
    - 背景色（16基色）
    - 256（ANSI）颜色支持（仅限Windows 10和UNIX）
    - RGB颜色支持（仅限Windows 10和UNIX）
    - 文本属性，如粗体、斜体、下划线、交叉等。
- 终端（功能“终端”）
    - 清除（所有行，当前行，从光标向下和向上，直到新行）
    - 上下滚动
    - 设置/获取终端大小
    - 退出当前进程
- 输入（功能“Input”）
    - 读字符
    - 读取行
    - 读取密钥输入事件（异步/同步）
    - 读取鼠标输入事件（按下、释放、位置、按钮）
- 屏幕（功能“Screen”）
    - 交替屏幕
    - 原始屏幕


### 已经测试的终端

- Windows Powershell
    - Windows 10 (Pro)
- Windows CMD
    - Windows 10 (Pro)
    - Windows 8.1 (N)
- Ubuntu Desktop Terminal
    - Ubuntu 17.10
- (Arch, Manjaro) KDE Konsole
- Linux Mint


这个机箱支持所有UNIX终端和Windows终端，直到Windows 7；但是，并不是所有的

终端已经过测试。如果您已将此库用于除上述列表之外的终端

问题，然后请随意添加到上面的列表-我真的很感激！ 

## 入门

<details>
<summary>
点击展示Cargo.toml.配置文件
</summary>

```toml
[dependencies]
rustterm = "0.13"
```

</details>
<p></p>

```rust
use std::io::{stdout, Write};

use rustterm::{execute, ExecutableCommand, style::{Attribute, Color, SetForegroundColor, SetBackgroundColor, ResetColor}, Output, Result};

fn main() -> Result<()> {
    // 调用 macro
    execute!(
        stdout(),
        SetForegroundColor(Color::Blue),
        SetBackgroundColor(Color::Red),
        Output("Styled text here."),
        ResetColor
    )?;

    // 或者调用方法
    stdout()
        .execute(SetForegroundColor(Color::Blue))?
        .execute(SetBackgroundColor(Color::Red))?
        .execute(Output("Styled text here."))?
        .execute(ResetColor)?;

    Ok(())
}
```

### 功能标志

默认情况下启用所有功能。您可以禁用默认功能并仅启用其中一些功能。

```toml
[dependencies.rustterm]
version = "0.12"
default-features = false        # Disable default features
features = ["cursor", "screen"] # Enable required features only
```

| Feature | Description |
| :-- | :-- |
| `input` | Sync/Async input readers |
| `cursor` | Cursor manipulation |
| `screen` | Alternate screen & raw mode |
| `terminal` | Size, clear, scroll |
| `style` | Colors, text attributes |


## 作者

* **Shirdon** - *Project Owner & creator*

## 许可证

这个项目，`rusterm`和它的所有子板条箱：`rusterm_screen`，`rusterm_cursor`，`rusterm_style`，

`rusterm_input`、`rusterm_terminal`、`rusterm_winapi`、`rusterm_utils`是MIT

