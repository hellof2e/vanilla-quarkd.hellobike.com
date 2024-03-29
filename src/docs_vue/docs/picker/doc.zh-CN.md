# Picker 选择器

### 介绍

提供多个选项集合供用户选择，支持单列选择和多列选择，级联选择请使用 CascadePicker

### 安装使用

```html
<!-- 引入 -->
<script type="module">
  import "quarkd/lib/picker"
</script>
<!-- 使用 -->
<quark-picker
  open
  title="请选择时间"
  onclose="close"
  onconfirm="confirm"
  onchange="change"
/>
```


### 基础用法

```html
<div @click="click">open</div>
<quark-picker
  title="请选择时间"
  open
  onclose="close"
  onconfirm="confirm"
  onchange="change"
/>
```

```js
picker.open = true;
picker.open = flase;
// 原生属性操作
picker.setAttribute('open', '')
picker.removeAttribute('open')
```

### 自定义头部

```html
<quark-picker open bottomhidden>
  <div slot="header">
    <span class="cancel" @click="close">取消</span>
    <span class="picker-title">请选择城市</span>
    <span class="ensure" @click="confirm">确定</span>
  </div>
</quark-picker>
```

```js
picker.setColumns([
  {
    defaultIndex: 0,
    values: ['星期一', '星期二', '星期三', '星期四', '星期五']
  },
  {
    defaultIndex: 1,
    values: ['上午', '下午']
  }
])

picker.getValues()

picker.onchange = function({ detail }) {
  // detail.value
}

picker.addEventListener('change', function(ev){
  console.log(this.open);
  console.log(ev.target.checked);
})
```

## API

### Props

| 参数         | 说明                                       | 类型      | 默认值    |
| ------------ | ------------------------------------------ | --------- | --------- |
| open         | picker 是否显示                            | `boolean` | `require` |
| title        | 标题                                       | `string ` |           |
| confirmtext  | 确定按钮的文字                             | `string`  | `确认`    |
| bottomhidden | 是否隐藏底部按钮（通常配合自定义头部使用） | `boolean` | `false`   |

### Events

| 名称    | 说明                 | 类型                                             |
| ------- | -------------------- | ------------------------------------------------ |
| close   | 点击遮罩或者取消按钮 | `() => void`                                     |
| confirm | 确定按钮点击回调     | `（e: {detail:{value: SelectColumn[]}}）=> void` |
| change  | picker 改变回调      | `（e: {detail:{value: SelectColumn[]}}）=> void` |

### Slot

| 名称        | 说明       |
| ----------- | ---------- |
| name=header | 自定义头部 |

### 方法

| 名称       | 说明                                           | 类型                                |
| ---------- | ---------------------------------------------- | ----------------------------------- |
| setColumns | 用于设置选择器数据                             | `(columns: PickerColumn[]) => void` |
| getValues  | 获取选择器选中的数据，通常配合自定义头部时使用 | `（）=> SelectColumn[]`             |

### 类型定义

```js
type PickerColumn = {
  values: string[];
  defaultIndex: number;
};

type SelectColumn = {
  value: string
  index: number
};
```

## 样式变量

组件提供了以下[CSS 变量](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_custom_properties)，可用于自定义样式，使用方法请参考[主题定制](#/zh-CN/guide/theme)。

| 名称                         | 说明     | 默认值                            |
| ---------------------------- | -------- | --------------------------------- |
| `--picker-title-font-size`   | 标题字号 | `18px`                            |
| `--picker-title-color`       | 标题颜色 | `#242729`                         |
| `--picker-title-font-weight` | 标题字重 | `500`                             |
| `--picker-title-font-family` | 标题字体 | `PingFangSC-Medium, PingFang SC ` |
