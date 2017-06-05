<template>
    <el-form ref="form" :model="form" label-width="80px"
             style="margin:20px;width:60%;min-width:600px;">
        <el-form-item label="活动名称" required>
            <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="数量" required>
            <el-input-number v-model="form.num1" @change="num1Change" :min="1" :max="10"></el-input-number>
        </el-form-item>
        <el-form-item label="cascader" required>
            <el-cascader v-model="form.cascader" :options="optionsWithDisabled" @change="cascaderChange"></el-cascader>
        </el-form-item>

        <el-form-item label="活动区域" required>
            <el-select v-model="form.region" placeholder="请选择活动区域">
                <el-option v-for="item in regions" :key="item.area" :label="item.name" :value="item.area"></el-option>
            </el-select>
        </el-form-item>
        <el-form-item label="活动时间" required>
            <el-col :span="11">
                <el-date-picker type="date" placeholder="选择日期" v-model="form.date1"
                                style="width: 100%;"></el-date-picker>
            </el-col>
            <el-col class="line" :span="2">-</el-col>
            <el-col :span="11">
                <el-time-picker type="fixed-time" placeholder="选择时间" v-model="form.date2"
                                style="width: 100%;"></el-time-picker>
            </el-col>
        </el-form-item>
        <el-form-item label="即时配送" required>
            <el-switch on-text="是" off-text="否" v-model="form.delivery" @change="deliveryChange"></el-switch>
        </el-form-item>
        <el-form-item label="活动性质" required>
            <el-checkbox-group v-model="form.type" :min="1" :max="2" @change="typeChange">
                <el-checkbox v-for="item in actTypes" :key="item.value" :label="item.value" name="type">{{item.name}}
                </el-checkbox>
            </el-checkbox-group>
        </el-form-item>
        <el-form-item label="特殊资源" required>
            <el-radio-group v-model="form.resource" @change="resourceChange">
                <el-radio v-for="item in resources" :key="item.value" :label="item.value">{{item.name}}</el-radio>
            </el-radio-group>
        </el-form-item>
        <el-form-item label="活动形式" required>
            <el-input type="textarea" v-model="form.desc"></el-input>
        </el-form-item>
        <el-form-item>
            <el-button type="primary" @click="onSubmit(form)">立即创建</el-button>
            <el-button @click.native.prevent>取消</el-button>
        </el-form-item>
    </el-form>
</template>

<script>
    export default {
        data() {
            return {
                regions: [{area: "sh", name: "上海"},
                    {area: "bj", name: "北京"}],
                actTypes: [{value: "ms", name: "美食/餐厅线上活动"},
                    {value: "dt", name: "地推活动"},
                    {value: "xx", name: "线下主题活动"},
                    {value: "pp", name: "单纯品牌曝光"}],
                resources: [{value: "xs", name: "线上品牌商赞助"},
                    {value: "xx", name: "线下场地免费"}],
                form: {
                    name: 's',
                    num1: 2,
                    region: 'sh',
                    date1: '',
                    date2: '',
                    delivery: false,
                    type: ['xx'],
                    resource: 'xx',
                    desc: 'asdfaf',
                    cascader:["zujian", "data", "tag"]
                },
                optionsWithDisabled: [{
                    value: 'zhinan',
                    label: '指南',
                    disabled: true,
                    children: [{
                        value: 'shejiyuanze',
                        label: '设计原则',
                        children: [{
                            value: 'yizhi',
                            label: '一致'
                        }, {
                            value: 'fankui',
                            label: '反馈'
                        }]
                    }, {
                        value: 'daohang',
                        label: '导航',
                        children: [{
                            value: 'cexiangdaohang',
                            label: '侧向导航'
                        }, {
                            value: 'dingbudaohang',
                            label: '顶部导航'
                        }]
                    }]
                }, {
                    value: 'zujian',
                    label: '组件',
                    children: [{
                        value: 'basic',
                        label: 'Basic',
                        children: [{
                            value: 'layout',
                            label: 'Layout 布局'
                        }, {
                            value: 'color',
                            label: 'Color 色彩'
                        }, {
                            value: 'typography',
                            label: 'Typography 字体'
                        }, {
                            value: 'icon',
                            label: 'Icon 图标'
                        }, {
                            value: 'button',
                            label: 'Button 按钮'
                        }]
                    }, {
                        value: 'form',
                        label: 'Form',
                        children: [{
                            value: 'radio',
                            label: 'Radio 单选框'
                        }, {
                            value: 'checkbox',
                            label: 'Checkbox 多选框'
                        }, {
                            value: 'input',
                            label: 'Input 输入框'
                        }, {
                            value: 'input-number',
                            label: 'InputNumber 计数器'
                        }, {
                            value: 'select',
                            label: 'Select 选择器'
                        }, {
                            value: 'cascader',
                            label: 'Cascader 级联选择器'
                        }, {
                            value: 'switch',
                            label: 'Switch 开关'
                        }, {
                            value: 'slider',
                            label: 'Slider 滑块'
                        }, {
                            value: 'time-picker',
                            label: 'TimePicker 时间选择器'
                        }, {
                            value: 'date-picker',
                            label: 'DatePicker 日期选择器'
                        }, {
                            value: 'datetime-picker',
                            label: 'DateTimePicker 日期时间选择器'
                        }, {
                            value: 'upload',
                            label: 'Upload 上传'
                        }, {
                            value: 'rate',
                            label: 'Rate 评分'
                        }, {
                            value: 'form',
                            label: 'Form 表单'
                        }]
                    }, {
                        value: 'data',
                        label: 'Data',
                        children: [{
                            value: 'table',
                            label: 'Table 表格'
                        }, {
                            value: 'tag',
                            label: 'Tag 标签'
                        }, {
                            value: 'progress',
                            label: 'Progress 进度条'
                        }, {
                            value: 'tree',
                            label: 'Tree 树形控件'
                        }, {
                            value: 'pagination',
                            label: 'Pagination 分页'
                        }, {
                            value: 'badge',
                            label: 'Badge 标记'
                        }]
                    }, {
                        value: 'notice',
                        label: 'Notice',
                        children: [{
                            value: 'alert',
                            label: 'Alert 警告'
                        }, {
                            value: 'loading',
                            label: 'Loading 加载'
                        }, {
                            value: 'message',
                            label: 'Message 消息提示'
                        }, {
                            value: 'message-box',
                            label: 'MessageBox 弹框'
                        }, {
                            value: 'notification',
                            label: 'Notification 通知'
                        }]
                    }, {
                        value: 'navigation',
                        label: 'Navigation',
                        children: [{
                            value: 'menu',
                            label: 'NavMenu 导航菜单'
                        }, {
                            value: 'tabs',
                            label: 'Tabs 标签页'
                        }, {
                            value: 'breadcrumb',
                            label: 'Breadcrumb 面包屑'
                        }, {
                            value: 'dropdown',
                            label: 'Dropdown 下拉菜单'
                        }, {
                            value: 'steps',
                            label: 'Steps 步骤条'
                        }]
                    }, {
                        value: 'others',
                        label: 'Others',
                        children: [{
                            value: 'dialog',
                            label: 'Dialog 对话框'
                        }, {
                            value: 'tooltip',
                            label: 'Tooltip 文字提示'
                        }, {
                            value: 'popover',
                            label: 'Popover 弹出框'
                        }, {
                            value: 'card',
                            label: 'Card 卡片'
                        }, {
                            value: 'carousel',
                            label: 'Carousel 走马灯'
                        }, {
                            value: 'collapse',
                            label: 'Collapse 折叠面板'
                        }]
                    }]
                }]
            }
        },
        methods: {
            onSubmit(form) {
                console.log('submit!', form);
            },
            typeChange(event){
                console.log(event)
            },
            resourceChange(value){
                console.log(value)
            },
            deliveryChange(value){
                console.log(value)
            },
            num1Change(value){
                console.log(value)
            },
            cascaderChange(value){
                console.log(value)
            }
        }
    }

</script>