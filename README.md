# ciliu-fonts

记词侠小程序使用的网络字体托管 repo。

通过 jsdelivr 自动反代 GitHub raw,免费,自带 CDN,国内访问可用。

## 字体清单

| 文件 | 用途 | 体积 | 授权 |
|------|------|------|------|
| `wenkai.<sha>.woff2` | 中文楷体(LXGW WenKai 子集) | ~890 KB | SIL OFL-1.1 |
| `eb-garamond-latin-400.woff2` | 英文衬线(EB Garamond Regular) | ~22 KB | SIL OFL-1.1 |
| `eb-garamond-latin-400-italic.woff2` | 英文衬线(EB Garamond Italic) | ~22 KB | SIL OFL-1.1 |

## CDN 访问 URL

```
https://cdn.jsdelivr.net/gh/qingchejun/ciliu-fonts@main/<file>
https://fastly.jsdelivr.net/gh/qingchejun/ciliu-fonts@main/<file>
https://unpkg.com/@qingchejun/ciliu-fonts@latest/<file>  # unpkg 不支持 gh,仅 npm,这条仅作参考不可用
```

主小程序工程通过 `utils/font.js` 加载,主源 jsdelivr,备源 fastly。

## 更新字体子集

回到主工程:

```bash
python3 tools/build-fonts/build.py
```

该脚本会:
1. 扫描 `pages/`、`utils/`、`cloudfunctions/` 等所有 .wxml/.js/.wxss/.json 中的中文字符
2. 合并 GB2312 一级字库(3755 字)+ CJK 标点 + ASCII
3. 调用 pyftsubset 生成新的子集 `wenkai.<新 sha>.woff2`
4. 输出 sha 值,提示更新 `utils/font.js` 的 `FONT_SHA`

把新 woff2 push 到本 repo,改 sha,缓存自动失效,新字符立即生效。

## 授权说明

- **LXGW WenKai**:SIL Open Font License 1.1,允许商业使用,需保留 OFL.txt 和版权声明
  - 原作者:LXGW 字体计划
  - 项目主页:https://github.com/lxgw/LxgwWenKai
- **EB Garamond**:SIL Open Font License 1.1,允许商业使用
  - 原作者:Georg Duffner / Octavio Pardo
  - 项目主页:https://github.com/georgd/EB-Garamond
