# 插件的配置信息

插件的配置信息, 包括插件名称、颜色、图标等信息。

```typescript
interface Config {
  name: string;
  logo?: string;
  color?: string;
  background?: string | string[];
  headers?: Record<string, string>;
}
```

### name

插件名称, 必填项。

### logo

插件图标, 可选项, 会显示在插件列表里面。

### color

插件的文本颜色, 主要是名称的显示颜色, 示例: `#FFFFFF`。

### background

插件的背景色, 支持渐变色, 示例: `['#4995EC', '#4BA5E9']`。

### headers

插件的请求头, 示例: `{ 'User-Agent': '...' }`。在访问第三方资源的时候会使用指定的头信息, 但是 [`Object`](./object.md) 里面如果包含了 `headers` 字段, 会覆盖这里的配置。