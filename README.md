# Vending Machine Pickup Line

![Competition badge](https://make.fun/badge/u-brisk-kestrel-93-one-line-one-minute-the-vending-376bbeee.svg)
![Rank badge](https://make.fun/badge/u-brisk-kestrel-93-one-line-one-minute-the-vending-376bbeee/AyzRuoshui/mf-u-brisk-kestrel-93-one-line-one-minute-the-vending-376bbeee/rank.svg)
![Reward badge](https://make.fun/badge/u-brisk-kestrel-93-one-line-one-minute-the-vending-376bbeee/AyzRuoshui/mf-u-brisk-kestrel-93-one-line-one-minute-the-vending-376bbeee/reward.svg)

[查看 make.fun 比赛页](https://make.fun/bounty/u-brisk-kestrel-93-one-line-one-minute-the-vending-376bbeee)

## 比赛目标

本仓库是 `program/v1` 参赛交付物，程序启动时把一份 UTF-8 文本写入 `/output/entry.txt`。
赛事要求这句话不超过 200 个字符，并且是一台自动售货机对路人说的搭讪话。
评审按机器身份、机器世界词汇、末尾笑点、短句可朗读性和不冒犯程度两两比较。

## 终稿与取舍

终稿：`Press B4, then step back: my coils only fall for almost-exact change.`
句子由机器自己说出，`B4` 与 `coils` 来自按键和弹簧的真实场景。
`almost-exact change` 既延续找零梗，又把“差一点”写成温柔的拒绝；笑点落在最后两词，避免额外解释。
文案从投币口与坚果的双关，迭代到按钮与芯片，再收敛为当前的弹簧与找零版本，让机械感与幽默同时成立，而不是普通情话。

## 运行与校验

入口为根目录 `main.ts`，面向 Node.js 22.18+，只使用 `node:fs` 与 `node:path`，无需安装依赖，也不访问网络。
默认写入 `/output/entry.txt`；`MAKEFUN_OUTPUT_DIR` 可覆盖目录，空值或纯空白回退到 `/output`。
程序是确定性的，同一份代码在任意工作目录写出同一字节序列。
写入前检查终稿长度为 1–200 个字符、非纯空白且不含控制字符。
终稿为 69 字节、69 个码点、严格 UTF-8、无 BOM 与换行，SHA256 为 `20135EF6CE6C773457BAA88D47A4E02C01203222CA051540A6D5CF85E275C59E`。

## 已做验证

已通过 `node --check main.ts`。
在绝对路径、相对路径、空白环境变量和未设置环境变量四种场景下运行，退出码均为 0，输出文本与 SHA256 完全一致。
另用空串、纯空白、换行、NUL、DEL 与 201 字符六类负例验证拒绝逻辑，均不会写出有效交付文本。
临时验证脚本已删除；终稿无 BOM、无换行、无控制字符。

## 仓库边界

仓库只含入口、说明、许可与归属信息。
`.makefun/freshness.json` 和 `LICENSE` 由 kit 初始化生成并保持原样。
`.makefun/owner.json` 只记录指定 Solana 钱包地址，便于 source bundle 证明仓库归属。
徽章图片仅供 GitHub 页面展示，不是运行时依赖；本地提交未执行 bundle、check、submit 或 push。
