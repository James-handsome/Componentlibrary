### Checkbox 多选框

#### 概述
-----
基本组件-多选框。主要用于一组可选项多项选择，或者单独用于标记切换某种状态。

### 代码示例
----

#### 单独使用
----
使用`v-model` 可以双向绑定数据。

::: demo
```vue
<template>
    <f-checkbox v-model="single">f-checkbox</f-checkbox>
</template>
<script>
    export default {
        data () {
            return {
                single: false
            }
        }
    }
</script>
```
::: 


#### 组合使用
----
使用`f-checkbox-group`配合数组来生成组合。在组合使用时，`f-checkbox` 使用 `label` 来自动判断选中状态。每个 `f-checkbox` 的内容可以自定义，如不填写则默认使用 `label` 的值
::: demo
```vue
<template>
    <f-checkbox-group v-model="fruit">
        <f-checkbox label="香蕉"></f-checkbox>
        <f-checkbox label="苹果"></f-checkbox>
        <f-checkbox label="西瓜"></f-checkbox>
    </f-checkbox-group>
</template>
<script>
    export default {
        data () {
            return {
                fruit: ['苹果']
            }
        }
    }
</script>
```
::: 

#### 不可用
----
通过设置`disabled`属性来禁用多选框。

::: demo
```vue
<template>
    <f-checkbox v-model="disabledSingle" disabled>f-checkbox</f-checkbox>
    <f-checkbox-group v-model="disabledGroup">
        <f-checkbox label="香蕉" disabled></f-checkbox>
        <f-checkbox label="苹果" disabled></f-checkbox>
        <f-checkbox label="西瓜"></f-checkbox>
    </f-checkbox-group>
</template>
<script>
    export default {
        data () {
            return {
                disabledSingle: true,
                disabledGroup: ['苹果']
            }
        }
    }
</script>
```
::: 

#### 与其它组件通信
----
与其它组件进行数据联动。

::: demo
```vue
<template>
    <f-checkbox v-model="checked" :disabled="disabled">
        <span v-if="checked">选中</span>
        <span v-else>取消</span>
         - 
        <span v-if="!disabled">可用</span>
        <span v-else>不可用</span>
    </f-checkbox>
    <br>
    <f-button type="primary" @click="checked = !checked">
        <span v-if="!checked">选中</span>
        <span v-else>取消</span>
    </f-button>
    <f-button type="primary" @click="disabled = !disabled">
        <span v-if="disabled">可用</span>
        <span v-else>不可用</span>
    </f-button>
</template>
<script>
    export default {
        data () {
            return {
                checked: true,
                disabled: false
            }
        }
    }
</script>
```
::: 

#### 全选
----

在实现全选效果时，你可能会用到 `indeterminate` 属性。示例代码只是一种写法，业务中可以用更多的方法，比如计算属性。
::: demo
```vue
<template>
    <div style="border-bottom: 1px solid #e9e9e9;padding-bottom:6px;margin-bottom:6px;">
        <f-checkbox
            :indeterminate="indeterminate"
            :value="checkAll"
            @click.prevent.native="handleCheckAll">全选</f-checkbox>
    </div>
    <f-checkbox-group v-model="checkAllGroup" @on-change="checkAllGroupChange">
        <f-checkbox label="香蕉"></f-checkbox>
        <f-checkbox label="苹果"></f-checkbox>
        <f-checkbox label="西瓜"></f-checkbox>
    </f-checkbox-group>
</template>
<script>
    export default {
        data () {
            return {
                indeterminate: true,
                checkAll: false,
                checkAllGroup: ['香蕉', '西瓜']
            }
        },
        methods: {
            handleCheckAll () {
                if (this.indeterminate) {
                    this.checkAll = false;
                } else {
                    this.checkAll = !this.checkAll;
                }
                this.indeterminate = false;

                if (this.checkAll) {
                    this.checkAllGroup = ['香蕉', '苹果', '西瓜'];
                } else {
                    this.checkAllGroup = [];
                }
            },
            checkAllGroupChange (data) {
                if (data.length === 3) {
                    this.indeterminate = false;
                    this.checkAll = true;
                } else if (data.length > 0) {
                    this.indeterminate = true;
                    this.checkAll = false;
                } else {
                    this.indeterminate = false;
                    this.checkAll = false;
                }
            }
        }
    }
</script>
```
::: 



### API

#### Checkbox props 

|属性	          |说明                                                                     |	类型 |	默认值 |
| ------------  |         --------                                                        | -----| -----   |
|value	        |只在单独使用时有效。可以使用 `v-model` 双向绑定数据	                       |Boolean|	false | 
|label	        |只在组合使用时有效。指定当前选项的 value 值，组合会自动判断是否选中	      |String - Number - Boolean |	- |
|disabled   	  |是否禁用当前项	                                                           |Boolean|	false |
|indeterminate	|设置  `indeterminate` 状态，只负责样式控制	                                 |Boolean|	false |

#### Checkbox events
|事件名 |	说明	|返回值 |
| ----  | ----  | ----  |
|on-change	| 只在单独使用时有效。在选项状态发生改变时触发，通过修改外部的数据改变时不会触发 |	true - false |


#### CheckboxGroup props
|属性	|说明	|类型	| 默认值 |
| --- | --- | --- | ----   |
|value|	指定选中项目的集合，可以使用 `v-model` 双向绑定数据	 | Array |	[] |


#### CheckboxGroup events
|事件名	| 说明	| 返回值 |
| ---   | ----  | ----   |
|on-change | 	在选项状态发生改变时触发，返回已选中的数组。通过修改外部的数据改变时不会触发| event |

