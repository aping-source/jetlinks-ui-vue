 ERR_PNPM_ENOENT  ENOENT: no such file or directory, rename 'E:\application\source\jetlinks\jetlinks-ui-vue\node_modules\.pnpm\vue3-sfc-loader@0.9.5_lodash@4.17.21_vue@3.5.16_typescript@5.8.3_\node_modules\@babel\code-frame' -> 'E:\application\source\jetlinks\jetlinks-ui-vue\node_modules\.pnpm\vue3-sfc-loader@0.9.5_lodash@4.17.21_vue@3.5.16_typescript@5.8.3_\node_modules\@babel\.ignored_code-frame'

pnpm要求项目必须存放在NTFS格式的磁盘上，如果项目位于exFAT/FAT32格式的磁盘（如U盘或移动硬盘），会导致重命名操作失败2。建议将项目迁移到本地NTFS格式的磁盘分区
1. 强制 pnpm 使用"复制"模式（推荐）
pnpm config set node-linker copy