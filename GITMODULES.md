`.gitmodules` 文件用于管理 Git 子模块（Submodules），它记录了父仓库依赖的子模块信息（URL、路径等）。以下是详细用法：

---

### **1. 创建 .gitmodules**
当添加子模块时自动生成：
```bash
git submodule add https://github.com/username/repo.git path/to/submodule
```
命令会：
1. 创建 `.gitmodules` 文件（若不存在）
2. 将子模块信息写入该文件
3. 克隆子模块到指定路径

---

### **2. .gitmodules 文件示例**
```ini
[submodule "path/to/submodule"]
    path = path/to/submodule
    url = https://github.com/username/repo.git
    branch = main  # 可选（默认跟踪子模块的默认分支）
```

---

### **3. 克隆含子模块的仓库**
```bash
# 首次克隆（递归初始化子模块）
git clone --recurse-submodules https://github.com/your-project.git

# 若已克隆未初始化子模块：
git submodule init   # 初始化配置文件
git submodule update # 拉取子模块代码
```

---

### **4. 更新子模块**
- **更新到父仓库记录的提交**（不自动拉取最新）：
  ```bash
  git submodule update
  ```
- **更新子模块到远程最新**：
  ```bash
  git submodule update --remote
  ```

---

### **5. 修改子模块**
1. 进入子模块目录：
   ```bash
   cd path/to/submodule
   ```
2. 修改代码后提交（需在子模块内独立提交）：
   ```bash
   git add .
   git commit -m "Update submodule"
   git push
   ```
3. 返回父仓库，记录新提交的哈希：
   ```bash
   git add path/to/submodule
   git commit -m "Update submodule reference"
   ```

---

### **6. 删除子模块**
手动步骤：
1. 删除 `.gitmodules` 中的对应条目
2. 暂存变更：
   ```bash
   git add .gitmodules
   ```
3. 删除子模块目录：
   ```bash
   git rm --cached path/to/submodule
   rm -rf path/to/submodule
   ```
4. 删除 `.git/config` 中的子模块配置（可选）
5. 提交变更：
   ```bash
   git commit -m "Remove submodule"
   ```

---

### **常见问题**
- **子模块未初始化？**  
  运行 `git submodule init && git submodule update`。

- **修改子模块后父仓库未检测到变更？**  
  子模块是独立的仓库，需在子模块内提交后，再在父仓库提交哈希引用。

- **克隆时跳过子模块？**  
  使用 `git clone --no-recurse-submodules`。

---

### **总结**
| 操作               | 命令                                      |
|--------------------|------------------------------------------|
| 添加子模块         | `git submodule add <URL> <path>`         |
| 克隆含子模块的仓库 | `git clone --recurse-submodules <URL>`   |
| 更新子模块         | `git submodule update --remote`          |
| 进入子模块         | `cd path/to/submodule`                   |

通过 `.gitmodules`，Git 可以精确跟踪子模块的版本，确保项目依赖的一致性。