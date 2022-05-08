### TimePicker 时间选择器

### 概述 
---
选择或输入标准时间，支持选择范围

#### 基础用法
--- 
设置属性 `type` 为 time 或 `timerange` 分别显示选择单个时间和选择范围时间类型。
设置属性 `placement` 可以更改选择器出现的方向，与 `Poptip` 和 `Tooltip` 配置一致，支持 12 个方向，详见 API


::: demo
```vue
<template>
    <f-row>
        <f-col span="12">
            <f-time-picker type="time" placeholder="选择时间" style="width: 168px"></f-time-picker>
        </f-col>
        <f-col span="12">
            <f-time-picker type="timerange" placement="bottom-end" placeholder="选择时间" style="width: 168px"></f-time-picker>
        </f-col>
    </f-row>
</template>
<script>
    export default {
        
    }
</script>
```
:::


#### 时间格式 
---
设置属性 `format` 可以改变时间的显示格式，详见  `Date`。
注意，`format` 只是改变显示的格式，并非改变 `value` 值。


::: demo
```vue
<template>
    <f-row>
        <f-col span="12">
            <f-time-picker :value="value1" format="HH点mm分ss秒" placeholder="选择时间" style="width: 168px"></f-time-picker>
        </f-col>
        <f-col span="12">
            <f-time-picker :value="value2" format="HH’mm’ss" type="timerange" placement="bottom-end" placeholder="选择时间" style="width: 168px"></f-time-picker>
        </f-col>
    </f-row>
</template>
<script>
    export default {
        data () {
            return {
                value1: '19:01:00',
                value2: ['07:01:00', '18:00:00']
            }
        }
    }
</script>
```
:::


#### 选择时分 
---
组件浮层中的列会随着 `format` 变化，当略去 `format` 中的秒时，浮层中对应的列也会消失。

::: demo
```vue
<template>
    <f-row>
        <f-col span="12">
            <f-time-picker format="HH:mm" placeholder="选择时间" style="width: 112px"></f-time-picker>
        </f-col>
        <f-col span="12">
            <f-time-picker format="HH:mm" type="timerange" placement="bottom-end" placeholder="选择时间" style="width: 168px"></f-time-picker>
        </f-col>
    </f-row>
</template>
<script>
    export default {

    }
</script>
```
:::


#### 不可选时间 
---
可以使用 `disabled-hours` `disabled-minutes` `disabled-seconds` 组合禁止用户选择某个时间。

使用 `hide-disabled-options` 可以直接把不可选择的项隐藏。


::: demo
```vue
<template>
    <f-row>
        <f-col span="12">
            <f-time-picker
                :disabled-hours="[1,5,10]"
                :disabled-minutes="[0,10,20]"
                placeholder="选择时间"
                style="width: 168px"></f-time-picker>
        </f-col>
        <f-col span="12">
            <f-time-picker
                hide-disabled-options
                :disabled-hours="[1,5,10]"
                :disabled-minutes="[0,10,20]"
                placeholder="选择时间"
                style="width: 168px"></f-time-picker>
        </f-col>
    </f-row>
</template>
<script>
    export default {

    }
</script>
```
:::


#### 带有确认操作
设置属性 `confirm`，选择器会有清空和确定按钮。

确认按钮并没有影响时间的正常选择。

::: demo
```vue
<template>
    <f-row>
        <f-col span="12">
            <f-time-picker confirm placeholder="选择时间" style="width: 168px"></f-time-picker>
        </f-col>
        <f-col span="12">
            <f-time-picker confirm type="timerange" placement="bottom-end" placeholder="选择时间" style="width: 168px">
            </f-time-picker>
        </f-col>
    </f-row>
</template>
<script>
    export default {

    }
</script>
```
:::


#### 手动控制组件
----
对于一些定制化的场景，可以使用 `slot` 配合参数 `open` `confirm` 及事件来手动控制组件的显示状态，详见示例和 API。

::: demo
```vue
<template>
    <f-time-picker
        :open="open"
        :value="value3"
        confirm
        @on-change="handleChange"
        @on-clear="handleClear"
        @on-ok="handleOk">
        <a href="javascript:void(0)" @click="handleClick">
            <Icon type="ios-clock-outline"></Icon>
            <template v-if="value3 === ''">选择时间</template>
            <template v-else>{{ value3 }}</template>
        </a>
    </f-time-picker>
</template>
<script>
    export default {
        data () {
            return {
                open: false,
                value3: ''
            }
        },
        methods: {
            handleClick () {
                this.open = !this.open;
            },
            handleChange (time) {
                this.value3 = time;
            },
            handleClear () {
                this.open = false;
            },
            handleOk () {
                this.open = false;
            }
        }
    }
</script>
```
:::


#### 尺寸
---
通过设置属性 `size` 为 `large` 或 `small` 可以调整选择器尺寸为大或小，默认不填为中。


::: demo
```vue
<template>
    <f-row :gutter="16">
        <f-col span="8">
            <f-time-picker size="small" placeholder="选择时间"></f-time-picker>
        </f-col>
        <f-col span="8">
            <f-time-picker placeholder="选择时间"></f-time-picker>
        </f-col>
        <f-col span="8">
            <f-time-picker size="large" placeholder="选择时间"></f-time-picker>
        </f-col>
    </f-row>
</template>
<script>
    export default {

    }
</script>
```
:::



### API #
#### TimePicker props 

| 属性 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| type | 显示类型，可选值为 `time`、`timerange` | String | time |
| value | 时间，可以是 JavaScript 的 Date，例如 **new Date()**，也可以是标准的时间格式，点击右边查看，注意：value 使用 v-model 时，值是 Date 类型，可以配合 \@on-change 使用 | date | \- |
| format | 展示的时间格式 | date | HH:mm:ss |
| placement | 时间选择器出现的位置，可选值为`top` `top-start` `top-end` `bottom` `bottom-start` `bottom-end` `left` `left-start` `left-end` `right` `right-start` `right-end` | String | bottom-start |
| placeholder | 占位文本 | String | 空 |
| confirm | 是否显示底部控制栏 | Boolean | false |
| open | 手动控制时间选择器的显示状态，true 为显示，false 为收起。使用该属性后，选择器不会主动关闭。建议配合 slot 及 confirm 和相关事件一起使用 | Boolean | null |
| size | 尺寸，可选值为`large`和`small`或者不设置 | String | \- |
| disabled | 是否禁用选择器 | Boolean | false |
| clearable | 是否显示清除按钮 | Boolean | true |
| readonly | 完全只读，开启后不会弹出选择器，只在没有设置 open 属性下生效 | Boolean | false |
| editable | 文本框是否可以输入，只在没有使用 slot 时有效 | Boolean | true |


#### TimePicker events

| 事件名 | 说明 | 返回值 |
| --- | --- | --- |
| on-change | 时间发生变化时触发 | 已经格式化后的时间，比如 09:41:00 |
| on-open-change | 弹出浮层和关闭浮层时触发 | true \| false |
| on-ok | 点击确定按钮时触发 | \- |
| on-clear | 在清空日期时触发 | \- |


#### TimePicker slot 
| 名称 | 说明 |
| --- | --- |
| 无 | 自定义选择器的显示内容，建议与 open 等参数一起使用，详见示例 |
