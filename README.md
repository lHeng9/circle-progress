# circle-progress
vue实现线性进度条和环形进度条

## 选项卡

| 参数         | 说明                                         | 类型    | 可选值        | 默认值 |
| ------------ | -------------------------------------------- | ------- | ------------- | ------ |
| percentage   | 百分比（必填）                               | number  | 0-100         | 0      |
| type         | 进度条类型                                   | string  | line/circle   | line   |
| stroke-width | 进度条的宽度，单位px                         | number  |               | 6      |
| text-inside  | 文字出现在进度条内（只有在type=line时可用）  | boolean |               | false  |
| status       | 进度条当前状态                               | string  | success/false |        |
| color        | 背景色（会覆盖status状态颜色）               | string  |               |        |
| width        | 环形进度条的宽度（只有在type为circle时可用） | number  |               | 126    |
| show-text    | 是否显示进度条文字内容                       | boolean |               | true   |

