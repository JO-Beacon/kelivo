# Kelivo 改版保护提醒

这个 [`README.md`](README.md) 已被改为本项目的改版记录和保护提醒，不再保留 [原版](https://github.com/Chevey339/kelivo) 项目介绍、下载链接、宣传内容或贡献说明。

后续同步 [原版](https://github.com/Chevey339/kelivo) 代码、合并新版源码、做重构或批量覆盖文件时，必须先阅读本文件，确认下面五项内容不能被误删、误改或回退。

## 1. Git 远端推送边界

- 永远不要给 `upstream` 推送任何东西。
- 标签、分支和发布相关内容只能推送到本仓库维护远端 `origin`。
- 执行任何 `git push` 前，必须先确认目标远端不是 `upstream`。

## 2. [`README.md`](README.md) 本身

- 本文件只用于记录改版保护提醒。
- 不要再从 [原版](https://github.com/Chevey339/kelivo)  Kelivo 覆盖回官方介绍版 [`README.md`](README.md)。
- 如果再次同步参考源码，必须保留本文件当前用途。
- 可以补充新的改版保护项，但不要删除已有保护项，除非明确确认该改动已废弃。

## 3. 单条聊天记录身份切换

这是主项目保留的自定义功能之一。

功能目标：

- 在单条聊天消息的更多操作菜单中，允许把一条消息的身份在“用户”和“模型”之间切换。
- 用户消息可以切换为模型消息。
- 模型消息可以切换为用户消息。
- 切换只影响当前这一条消息，不应该批量改动整段对话。

保护范围：

- 菜单入口：[`lib/features/chat/widgets/message_more_sheet.dart`](lib/features/chat/widgets/message_more_sheet.dart)
- 消息列表回调：[`lib/features/home/widgets/message_list_view.dart`](lib/features/home/widgets/message_list_view.dart)
- 页面控制器入口：[`lib/features/home/controllers/home_page_controller.dart`](lib/features/home/controllers/home_page_controller.dart)
- 聊天控制器更新：[`lib/features/home/controllers/chat_controller.dart`](lib/features/home/controllers/chat_controller.dart)
- 底层消息保存：[`lib/core/services/chat/chat_service.dart`](lib/core/services/chat/chat_service.dart)
- 本地化文案：[`lib/l10n/app_en.arb`](lib/l10n/app_en.arb)、[`lib/l10n/app_zh.arb`](lib/l10n/app_zh.arb)、[`lib/l10n/app_zh_Hans.arb`](lib/l10n/app_zh_Hans.arb)、[`lib/l10n/app_zh_Hant.arb`](lib/l10n/app_zh_Hant.arb)

同步或重构时的检查点：

- 更多菜单里仍然能看到“切换为用户”和“切换为模型”。
- 切换后消息角色会真实保存，而不是只改界面显示。
- `role` 更新链路不能被回退成只能更新 `content`。
- 新增或修改本地化 key 时，四个 ARB 文件必须保持同步。

## 4. 新建或复制助手时插到顶部的设置项

这是主项目保留的自定义功能之一。

功能目标：

- 设置里有一个开关，用来控制“新建助手”和“复制助手”放到助手列表顶部。
- 开关关闭时，保持默认行为。
- 开关打开时，新建或复制出来的助手插入列表顶部。
- 移动端和桌面端都必须生效。

保护范围：

- 设置持久化：[`lib/core/providers/settings_provider.dart`](lib/core/providers/settings_provider.dart)
- 助手新增/复制逻辑：[`lib/core/providers/assistant_provider.dart`](lib/core/providers/assistant_provider.dart)
- 移动端助手页面：[`lib/features/assistant/pages/assistant_settings_page.dart`](lib/features/assistant/pages/assistant_settings_page.dart)
- 桌面端助手设置页：[`lib/desktop/setting/assistants_pane.dart`](lib/desktop/setting/assistants_pane.dart)
- 移动端显示设置：[`lib/features/settings/pages/display_settings_page.dart`](lib/features/settings/pages/display_settings_page.dart)
- 桌面端显示设置：[`lib/desktop/setting/display_pane.dart`](lib/desktop/setting/display_pane.dart)
- 本地化文案：[`lib/l10n/app_en.arb`](lib/l10n/app_en.arb)、[`lib/l10n/app_zh.arb`](lib/l10n/app_zh.arb)、[`lib/l10n/app_zh_Hans.arb`](lib/l10n/app_zh_Hans.arb)、[`lib/l10n/app_zh_Hant.arb`](lib/l10n/app_zh_Hant.arb)

同步或重构时的检查点：

- 设置项不能消失。
- 设置值必须持久化，重启应用后不能丢。
- 移动端新建助手要读取这个设置。
- 移动端复制助手要读取这个设置。
- 桌面端新建助手要读取这个设置。
- 桌面端复制助手要读取这个设置。
- `addAssistant` 和 `duplicateAssistant` 的插入位置参数不能被删掉。
- 新增或修改本地化 key 时，四个 ARB 文件必须保持同步。

## 5. 改版版本号规则

这是主项目保留的自定义发布规则之一。

规则目标：

- 本项目不再直接使用上游 [原版](https://github.com/Chevey339/kelivo) 版本号。
- 同步上游源码后，必须在上游版本号后追加本项目改版序号。
- 当前对外改版版本号固定显示为 `1.1.15.1`，不能回退为上游 `1.1.15` 或更早版本。
- [`pubspec.yaml`](pubspec.yaml) 必须使用 Flutter 合法版本格式，当前写作 `1.1.15+1`，其中 `1.1.15` 对应上游版本，`1` 对应本项目改版构建号。

保护范围：

- 项目版本声明：[`pubspec.yaml`](pubspec.yaml)
- 本保护提醒：[`README.md`](README.md)

同步或重构时的检查点：

- [`pubspec.yaml`](pubspec.yaml) 中的 `version` 不能被 [原版](https://github.com/Chevey339/kelivo) 源码覆盖回上游版本号。
- 对外版本号应体现“上游版本 + 改版序号”，当前对外显示为 `1.1.15.1`。
- [`pubspec.yaml`](pubspec.yaml) 中的 Flutter 合法版本当前应保持为 `1.1.15+1`。
- 如未来继续同步上游版本，必须先确认新的改版版本号规则，再更新 [`README.md`](README.md) 和 [`pubspec.yaml`](pubspec.yaml)。

## 6. Android 只构建 APK

这是主项目保留的自定义发布规则之一。

规则目标：

- Android 发布产物只构建 APK。
- 永远不要构建、发布或上传 AAB。
- 本地和 CI 都应使用 `flutter build apk`，不能使用 `flutter build appbundle`。

保护范围：

- Android 构建命令和发布流程：[`android/`](android/)、[`.github/workflows`](.github/workflows)
- 本保护提醒：[`README.md`](README.md)

同步或重构时的检查点：

- 构建 Android 时只能生成 APK 产物。
- 如发现 `flutter build appbundle`、`.aab` 发布上传、或任何 AAB 专用流程，必须删除或改为 APK 流程。
- 当前推荐命令为 `flutter build apk --release --split-per-abi`。

## 7. 本地依赖与工作区边界

这是主项目保留的同步边界之一。

规则目标：

- Markdown 渲染依赖必须使用 [原版](https://github.com/Chevey339/kelivo)  1.1.13 随源码带来的本地路径依赖，而不是回退到 pub.dev 版本。
- [`pubspec.yaml`](pubspec.yaml) 中的 `gpt_markdown` 必须指向 [`dependencies/gpt_markdown`](dependencies/gpt_markdown)。
- 当前工作区包含参考源码目录 [`参考文件/`](参考文件/)，它只用于对比同步，不能被 Dart analyzer 扫描。
- 本地安装器脚本、参考源码副本和本地快捷方式不能被误提交。

保护范围：

- 本地 Markdown 依赖：[`dependencies/gpt_markdown`](dependencies/gpt_markdown)
- 依赖声明：[`pubspec.yaml`](pubspec.yaml)
- 分析排除：[`analysis_options.yaml`](analysis_options.yaml)
- 忽略规则：[`.gitignore`](.gitignore)

同步或重构时的检查点：

- 不要把 `gpt_markdown` 回退成 pub.dev 版本约束。
- 不要删除 [`dependencies/gpt_markdown`](dependencies/gpt_markdown) 本地依赖目录。
- [`analysis_options.yaml`](analysis_options.yaml) 必须继续排除 `参考文件/**`，避免分析参考源码副本。
- [`.gitignore`](.gitignore) 必须继续忽略 `installer.iss`、`参考文件/` 和本地快捷方式。

白话风险提醒：

1. 以后别把 [`gpt_markdown`](pubspec.yaml) 改回网上下载版。
2. 以后别把 [`dependencies/gpt_markdown`](dependencies/gpt_markdown) 里的相对导入覆盖回包名导入。
3. 以后别删 [`analysis_options.yaml`](analysis_options.yaml) 里排除 `参考文件/**` 的规则。
4. 以后别删 [`.gitignore`](.gitignore) 里忽略本地文件的规则。

## 8. 长会话版本消息渲染顺序修复

这是主项目保留的 BUG 修复之一。

问题现象：

- 打开已有长会话，或在长会话里向上/向下滚动加载历史时，界面可能看起来随机插入了旧上下文。
- 这个问题主要出现在含有编辑、重新生成、分支版本消息的会话里。
- 模型实际收到的上下文通常是正常的，问题发生在聊天记录展示层。

原因简述：

- 编辑或重新生成消息时，新版本可能会被追加到会话尾部。
- 长会话懒加载只会加载当前窗口附近的一段消息。
- 如果当前窗口只加载到了“旧消息的新版本”，但没有加载到它原本所属的消息组位置，界面就可能把它误显示到当前上下文中。

修复策略：

- 第一层是展示层兼容：不迁移、不重写用户旧存档。
- [`ChatController.collapseVersions()`](lib/features/home/controllers/chat_controller.dart) 折叠版本消息时，必须按持久化会话里的原始消息位置稳定排序。
- 当前懒加载窗口只应显示原始组锚点也在当前窗口内的版本组，避免旧消息的新版本被误插入到当前可见上下文。
- 第二层是新写入源头修复：[`ChatService.appendMessageVersion()`](lib/core/services/chat/chat_service.dart) 和 [`ChatService.addMessage()`](lib/core/services/chat/chat_service.dart) 对 `groupId + version > 0` 的新版本消息，必须插回同组消息附近，而不是继续追加到会话尾部。
- 普通新消息仍追加到尾部；找不到同组锚点时也应回退追加到尾部，避免破坏写入流程。
- 旧存档彻底重排不属于应用自动迁移范围。如需清理旧 `chats.json`，必须使用完全独立的修复工具并保留备份。
- 删除版本分支后必须按懒加载开关同步当前消息列表：懒加载关闭时，[`ChatController.reloadMessages()`](lib/features/home/controllers/chat_controller.dart) 必须重新读取完整会话；懒加载开启时，仍保持当前有界窗口，不能意外全量展开历史。
- 单版本删除和删除全部版本都会经过 [`HomeViewModel._deleteMessageVersions()`](lib/features/home/controllers/home_view_model.dart)，最终统一调用 [`ChatController.reloadMessages()`](lib/features/home/controllers/chat_controller.dart)，不能绕开这条同步链路。

第二阶段独立工具：

- 独立工具目录：[`repair_chat_archive/`](repair_chat_archive/)
- 主程序：[`repair_chat_archive/repair_chat_archive.py`](repair_chat_archive/repair_chat_archive.py)
- 工具说明：[`repair_chat_archive/README.md`](repair_chat_archive/README.md)
- 测试文件：[`repair_chat_archive/tests/test_repair_chat_archive.py`](repair_chat_archive/tests/test_repair_chat_archive.py)
- 运行方式：进入 [`repair_chat_archive/`](repair_chat_archive/) 后执行 `uv run python repair_chat_archive.py path/to/chats.json`。
- 默认输出：`chats.fixed.json`。
- 默认备份：`chats.backup.json`。
- 该工具只使用 Python 标准库，不导入 Kelivo 的 [`lib/`](lib/) 代码，不依赖 Flutter / Dart，不修改 Kelivo 本地数据库。
- 该工具只重排 `Conversation.messageIds`，不修改消息正文、消息 ID、版本号、时间戳、会话 ID、`versionSelections` 或备份 schema。
- 遇到重复 `messageIds`、缺失消息、找不到非版本锚点、JSON 结构异常时，必须保守跳过并打印报告，不能强行改坏用户存档。

保护范围：

- 展示层折叠逻辑：[`lib/features/home/controllers/chat_controller.dart`](lib/features/home/controllers/chat_controller.dart)
- 长会话懒加载与版本消息回归测试：[`test/features/home/controllers/chat_controller_lazy_history_test.dart`](test/features/home/controllers/chat_controller_lazy_history_test.dart)
- 底层版本写入顺序：[`lib/core/services/chat/chat_service.dart`](lib/core/services/chat/chat_service.dart)
- 底层版本写入顺序测试：[`test/core/services/chat/chat_service_temporary_conversation_test.dart`](test/core/services/chat/chat_service_temporary_conversation_test.dart)
- 第二阶段独立旧存档修复工具：[`repair_chat_archive/`](repair_chat_archive/)

同步或重构时的检查点：

- 长会话尾部窗口不能显示原始组锚点不在窗口内的旧消息编辑版本。
- 完整会话折叠结果仍要把选中的编辑版本放回原始消息位置。
- 编辑旧消息产生的新版本，不能被写到会话尾部。
- 重新生成旧助手消息产生的新版本，不能被写到会话尾部。
- 普通新消息仍应写到会话尾部，不能被错误插入旧消息组。
- 找不到同组锚点的版本消息应安全回退追加到尾部。
- 模型请求上下文和 UI 展示顺序不能混为一谈。
- 不要在应用启动、打开会话或导入备份时静默重排旧存档。
- 关闭懒加载后删除旧分支，聊天列表必须立即保留删除后的完整会话，不能只显示删除前局部窗口，也不能依赖切换会话后才恢复。
- 开启懒加载后删除旧分支，聊天列表必须继续保持有界窗口，不能为了修复删除同步而回退成全量渲染长会话。
- 修改相关 Dart 逻辑后，至少运行 [`test/features/home/controllers/chat_controller_lazy_history_test.dart`](test/features/home/controllers/chat_controller_lazy_history_test.dart) 和 [`test/core/services/chat/chat_service_temporary_conversation_test.dart`](test/core/services/chat/chat_service_temporary_conversation_test.dart)。
- 修改独立 Python 工具后，进入 [`repair_chat_archive/`](repair_chat_archive/) 运行 `uv run --with pytest pytest` 和 `python -m py_compile repair_chat_archive.py tests\\test_repair_chat_archive.py`。

## 同步 [原版](https://github.com/Chevey339/kelivo) 代码前的最低检查

每次从参考源码或上游版本同步前，至少检查：

1. [`README.md`](README.md) 是否仍是当前保护提醒版本。
2. 单条聊天记录身份切换是否仍存在。
3. 新建或复制助手插到顶部设置项是否仍存在。
4. [`pubspec.yaml`](pubspec.yaml) 是否仍使用本项目改版版本号，而不是上游 [原版](https://github.com/Chevey339/kelivo) 版本号。
5. Android 构建和发布流程是否仍只生成 APK，且没有引入 AAB。
6. 创建分支时的克隆数据完整性是否仍保留，消息身份、版本组、元数据、工具事件和 thought signature 不能丢。
7. 创建分支时的源消息选择是否仍按目标消息原始下标连续截取，不能回退为按 `groupId` 集合筛选。
8. [`gpt_markdown`](dependencies/gpt_markdown) 是否仍使用本地路径依赖，不能回退为 pub.dev 版本约束。
9. 长会话版本消息修复是否仍保留，包括 [`ChatController.collapseVersions()`](lib/features/home/controllers/chat_controller.dart) 的稳定排序与窗口过滤逻辑、[`ChatController.reloadMessages()`](lib/features/home/controllers/chat_controller.dart) 删除分支后的懒加载开关分流、[`ChatService`](lib/core/services/chat/chat_service.dart) 对新版本消息插回同组附近的写入逻辑，以及 [`repair_chat_archive/`](repair_chat_archive/) 独立旧存档修复工具。
10. [`analysis_options.yaml`](analysis_options.yaml) 是否仍排除 `参考文件/**`。
11. [`.gitignore`](.gitignore) 是否仍忽略本地安装器、参考源码副本和本地快捷方式。
12. 如果同步覆盖了 ARB 文件，必须重新补齐四个语言文件并运行本地化生成。
13. 如果同步覆盖了 Dart 代码，必须重新运行格式化、分析和测试。
