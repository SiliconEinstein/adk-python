使用可编辑模式 (editable mode) 进行安装。

这样做的好处是，你的安装实际上是一个指向你本地代码的“快捷方式”。你在 fork 的库里做的任何修改，都会立即在你使用的项目中生效，无需重新安装。

下面是详细的步骤和说明。

推荐方法：使用可编辑模式 (pip install -e)
假设你的目录结构如下：

/workspace/
    ├── my-forked-lib/      # 这是你 fork 并修改的库
    │   ├── pyproject.toml  # 或者 setup.py
    │   ├── src/
    │   └── ...
    │
    └── my-other-project/   # 这是你要使用该库的另一个项目
        ├── main.py
        └── ...
步骤详解
准备工作：虚拟环境 (强烈推荐)
为了不污染全局的 Python 环境，并确保项目依赖隔离，请在你的 my-other-project 中创建一个虚拟环境。

Bash

# 进入你的项目目录
cd /workspace/my-other-project

# 创建虚拟环境 (例如，命名为 venv)
python -m venv venv

# 激活虚拟环境
# Windows:
.\venv\Scripts\activate
# macOS / Linux:
source venv/bin/activate

# 激活后，你的命令行提示符前应该会有一个 (venv) 标志
安装你修改的库
现在，在已激活虚拟环境的终端中，使用 pip 以可编辑模式安装你 fork 的库。你需要提供 my-forked-lib 的相对或绝对路径。

Bash

# -e 表示 --editable
# "." 表示当前目录，所以我们需要指定到那个库的路径
pip install -e /workspace/my-forked-lib
或者，如果你在 my-other-project 目录下，可以使用相对路径：

Bash

pip install -e ../my-forked-lib
注意：这个命令能成功的前提是，my-forked-lib 必须是一个合法的 Python 包，即根目录下包含 pyproject.toml 或 setup.py 文件。现代 Python 项目通常使用 pyproject.toml。

验证安装
安装完成后，你可以通过 pip list 来查看。你会看到 my-forked-lib 出现在列表中，并且它的位置会指向你的本地源码路径。

Bash

(venv) $ pip list
Package         Version   Location
--------------- --------- -----------------------
my-forked-lib   0.1.0     /workspace/my-forked-lib
pip             ...       ...
...
在项目中使用
现在，你可以在 my-other-project 的代码中正常 import 并使用它了。

/workspace/my-other-project/main.py

Python

# 假设你修改的库名叫 my_forked_lib
import my_forked_lib

# 调用你新增或修改的功能
my_forked_lib.some_new_function()
当你后续在 /workspace/my-forked-lib 的代码中做了任何修改并保存后，直接运行 main.py 就能看到最新的效果，完全不需要重新执行 pip install。


