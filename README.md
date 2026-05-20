# Kelivo 改版保护提醒

这个 [`README.md`](README.md) 已被改为本项目的改版记录和保护提醒，不再保留原版项目介绍、下载链接、宣传内容或贡献说明。

后续同步原版代码、合并新版源码、做重构或批量覆盖文件时，必须先阅读本文件，确认下面五项内容不能被误删、误改或回退。

## 1. [`README.md`](README.md) 本身

- 本文件只用于记录改版保护提醒。
- 不要再从原版 Kelivo 覆盖回官方介绍版 [`README.md`](README.md)。
- 如果再次同步参考源码，必须保留本文件当前用途。
- 可以补充新的改版保护项，但不要删除已有保护项，除非明确确认该改动已废弃。

## 2. 单条聊天记录身份切换

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

## 3. 新建或复制助手时插到顶部的设置项

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

## 4. 改版版本号规则

这是主项目保留的自定义发布规则之一。

规则目标：

- 本项目不再直接使用上游原版版本号。
- 同步上游源码后，必须在上游版本号后追加本项目改版序号。
- 当前对外改版版本号固定显示为 `1.1.13.2`，不能回退为上游 `1.1.13` 或 `1.1.13+39`。
- [`pubspec.yaml`](pubspec.yaml) 必须使用 Flutter 合法版本格式，当前写作 `1.1.13+902`，其中 `1.1.13` 对应上游版本，`902` 对应本项目改版构建号。

保护范围：

- 项目版本声明：[`pubspec.yaml`](pubspec.yaml)
- 本保护提醒：[`README.md`](README.md)

同步或重构时的检查点：

- [`pubspec.yaml`](pubspec.yaml) 中的 `version` 不能被原版源码覆盖回上游版本号。
- 对外版本号应体现“上游版本 + 改版序号”，当前对外显示为 `1.1.13.2`。
- [`pubspec.yaml`](pubspec.yaml) 中的 Flutter 合法版本当前应保持为 `1.1.13+902`。
- 如未来继续同步上游版本，必须先确认新的改版版本号规则，再更新 [`README.md`](README.md) 和 [`pubspec.yaml`](pubspec.yaml)。

## 5. Android 只构建 APK

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

## 同步原版代码前的最低检查

每次从参考源码或上游版本同步前，至少检查：

1. [`README.md`](README.md) 是否仍是当前保护提醒版本。
2. 单条聊天记录身份切换是否仍存在。
3. 新建或复制助手插到顶部设置项是否仍存在。
4. [`pubspec.yaml`](pubspec.yaml) 是否仍使用本项目改版版本号，而不是上游原版版本号。
5. Android 构建和发布流程是否仍只生成 APK，且没有引入 AAB。
6. 如果同步覆盖了 ARB 文件，必须重新补齐四个语言文件并运行本地化生成。
7. 如果同步覆盖了 Dart 代码，必须重新运行格式化、分析和测试。
