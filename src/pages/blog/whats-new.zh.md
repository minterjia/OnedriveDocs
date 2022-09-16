# 更新日志

### Page Front-matter

| 写法 | 解释 |
| --- | --- |
| title | 【必需】页面标题 |
| date | 【必需】页面创建日期 |
| type | 【必需】标籤、分类和友情链接三个页面需要配置 |
| updated | 【可选】页面更新日期 |
| description | 【可选】页面描述 |
| keywords | 【可选】页面关键字 |
| comments | 【可选】显示页面评论模块(默认 true) |
| top_img | 【可选】页面顶部图片 |
| mathjax | 【可选】显示 mathjax(当设置 mathjax 的 per_page: false 时，才需要配置，默认 false) |
| katex | 【可选】显示 katex(当设置 katex 的 per_page: false 时，才需要配置，默认 false) |
| aside | 【可选】显示侧边栏 (默认 true) |
| aplayer | 【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的`音乐` 配置 |
| highlight_shrink | 【可选】配置代码框是否展开(true/false)(默认为设置中 highlight_shrink 的配置) |

### Post Front-matter

| 写法 | 解释 |
| --- | --- |
| title | 【必需】文章标题 |
| date | 【必需】文章创建日期 |
| updated | 【可选】文章更新日期 |
| tags | 【可选】文章标籤 |
| categories | 【可选】文章分类 |
| keywords | 【可选】文章关键字 |
| description | 【可选】文章描述 |
| top_img | 【可选】文章顶部图片 |
| cover | 【可选】文章缩略图(如果没有设置 top_img,文章页顶部将显示缩略图，可设为 false/图片地址/留空) |
| comments | 【可选】显示文章评论模块(默认 true) |
| toc | 【可选】显示文章 TOC(默认为设置中 toc 的 enable 配置) |
| toc_number | 【可选】显示 toc_number(默认为设置中 toc 的 number 配置) |
| copyright | 【可选】显示文章版权模块(默认为设置中 post_copyright 的 enable 配置) |
| copyright_author | 【可选】文章版权模块的`文章作者` |
| copyright_author_href | 【可选】文章版权模块的`文章作者`链接 |
| copyright_url | 【可选】文章版权模块的`文章连结`链接 |
| copyright_info | 【可选】文章版权模块的`版权声明`文字 |
| mathjax | 【可选】显示 mathjax(当设置 mathjax 的 per_page: false 时，才需要配置，默认 false) |
| katex | 【可选】显示 katex(当设置 katex 的 per_page: false 时，才需要配置，默认 false) |
| aplayer | 【可选】在需要的页面加载 aplayer 的 js 和 css,请参考文章下面的`音乐` 配置 |
| highlight_shrink | 【可选】配置代码框是否展开(true/false)(默认为设置中 highlight_shrink 的配置) |
| aside | 【可选】显示侧边栏 (默认 true) |
| hide | 【可选】隐藏文章 |
| sticky | 【可选】文章置顶，值越大越考上 |

🎉 此项目的更新内容将在此页持续记录，详情请参考 [What's new? #325](https://github.com/spencerwooo/onedrive-vercel-index/discussions/325)。

#### 2022/2/14 💞

- 除了受密码保护的文件夹，以及文件直链 API 路径外，其他所有 API 路径均使用 Vercel 边缘缓存（有效期 1 分钟）：

  ```
  Cache-Control: max-age=0, s-maxage=60, stale-while-revalidate
  ```

- 文件直链 API 由 `/api?path=<file>&raw=true` 更改为 `/api/raw?path=<file>`，无缓存。
- 文件直链 API 接受 URL 参数 `&odpt=<hashed_token>` 用于受密码保护文件的鉴权。

#### 2022/2/10

- 🚀 性能提升：
  - 缩略图现在在文件完成加载后单独进行请求。因为减少了 OneDrive API 的请求量，所以提升了些许文件夹列表加载速度。
  - **启用 Vercel 边缘缓存。** 我们使用了 Vercel 的边缘函数缓存以及 `stale-while-revalidate` 功能，你将体验到飞快的文件列表加载速度。 **边缘缓存一分钟内有效。** 参考：[🚀 Edge caching #407](https://github.com/spencerwooo/onedrive-vercel-index/discussions/407)
- 👨‍💻 代码高亮： 我们不再使用 `Prism.js` 依赖，代码高亮现在由 `react-syntax-highlighter` 处理。（内部使用 `highlight.js`，对不同语言的高亮支持是异步导入的，所以高亮会在代码加载完成后显示。）

  |                              Light                              |                             Dark                              |
  | :-------------------------------------------------------------: | :-----------------------------------------------------------: |
  | ![Light code syntax highlight](./_images/light-code-syntax.png) | ![Dark code syntax highlight](./_images/dark-code-syntax.png) |

- 🎸 音频预览（音乐播放器）现在能显示音频封面了！

  ![Audio Player](./_images/audio-player.png)

#### 2022/2/8

- 🇨🇳/🇬🇧 - 项目已汉化 🥱
- 🎥 已支持 `.flv` 格式的视频
- 🔗 加强复制的链接的可读性

  ```diff
  - before: /api?path=/%F0%9F%8E%BB%20Genshin%20playlist/%E3%80%90%E5%8E%9F%E7%A5%9E%E3%80%91%E8%83%A1%E6%A1%83%EF%BC%9A%E5%95%8A%E5%AF%B9%E5%AF%B9%E5%AF%B9%E5%AF%B9.mp4&raw=true
  + after:  /api?path=/🎻%20Genshin%20playlist/【原神】胡桃：啊对对对对.mp4&raw=true
  ```

- 📅 你现在可以在 `site.config.js` 的 `datetimeFormat` 自定义日期格式了。

#### 2022/2/5

- 💠 正式支持布局切换，新增带缩略图预览的网格布局。

  ![Grid layout](./_images/grid-layout-images.png)

- 🗑 我们不再使用高性能消耗较高的 `react-viewer`。

#### 2022/2/2

- 🎥 我们删除了 `react-player` 而使用可靠的 `react-dplayer` 与 `react-audio-player` 来播放视频与音频。
- 🎇 我们现在还能为视频显示缩略图：

  |                                  Before                                  |                                After                                |
  | :----------------------------------------------------------------------: | :-----------------------------------------------------------------: |
  | ![Old version doesn't render thumbnails](./_images/old-no-thumbnail.png) | ![New version renders thumbnails](./_images/new-with-thumbnail.png) |

- 💬 我们添加了对 WebVTT 字幕的支持，你只需要将 `.vtt` 后缀的与视频文件名相同的字幕文件放置在同一个文件夹下即可。

  |                                 Before                                  |                                    After                                     |
  | :---------------------------------------------------------------------: | :--------------------------------------------------------------------------: |
  | ![Old version doesn't respect subtitles](./_images/old-no-subtitle.png) | ![New version tries to reference subtitles](./_images/new-with-subtitle.png) |

- ⚡️ 我们将包管理器从 `npm` 更换为 `pnpm` 以减少部署时间。你需要在 Vercel 中修改以下设置：

  ![Migrate from npm to pnpm](./_images/pnpm-commands.png)

  - Build command: `pnpm build`
  - Install command: `pnpm install`

#### 2022/1/29

- ❗**重要** - 配置文件已从 `.json` 更换为 `.config.js` ，并添加了注释。同时为了隐私着想，现在你还可以将 `userPrincipleName` 在 Vercel 的环境变量里定义。
- CORS 头现在出现在 OneDrive 的 ~~`?raw=true`~~ `/api/raw` 文件直链路由中。

#### 2022/1/22

- 🔍 [Supporting search for all versions of OneDrive #295](https://github.com/spencerwooo/onedrive-vercel-index/discussions/295)

#### 2022/1/11

- 📚 [New documentation site live #264](https://github.com/spencerwooo/onedrive-vercel-index/discussions/264)

#### 2022/1/10

- 🚫 为遵循 Vercel 服务条款，代理下载已被移除。 [Proxied download not working - 无法使用代理下载 #251](https://github.com/spencerwooo/onedrive-vercel-index/discussions/251)

#### 2022/1/1

- 🚀 我们在部署时不再需要额外的获取 token/secret 的步骤。 [New version update: No extra deployment setup is required anymore! #215](https://github.com/spencerwooo/onedrive-vercel-index/discussions/215)
