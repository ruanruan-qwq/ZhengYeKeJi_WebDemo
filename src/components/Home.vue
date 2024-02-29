<template>
  <a-layout>

    <!-- 侧边栏 -->
    <a-layout-sider class="sider_style">
      <div class="logo">
        <div class="corporation_title">
          <img src="../../public//logo.png" class="header_img">
          <div>上海也正医药有限公司</div>
        </div>
        <!-- 
          theme 主题颜色 - 暗黑
          mode 菜单类型 - 内嵌
          triggerSubMenuAction 子菜单触发方式 - 点击
          items 菜单内容
         -->
        <a-menu theme="dark" triggerSubMenuAction="click" mode="inline" :items="siderItems">
        </a-menu>
      </div>
    </a-layout-sider>

    <a-layout>

      <!-- 页面头部 -->
      <a-layout-header>
        <a-menu theme="dark" mode="horizontal" :items="headerItems">
        </a-menu>
      </a-layout-header>

      <!-- 页面身体 -->
      <a-layout-content class="content_style">

        <a-layout style="padding: 0 24px 24px">
          <a-breadcrumb style="margin: 16px 0">
            <a-breadcrumb-item>首页</a-breadcrumb-item>
            <a-breadcrumb-item>年度协议管理</a-breadcrumb-item>
            <a-breadcrumb-item>二级商协议</a-breadcrumb-item>
            <a-breadcrumb-item>新增二级商协议</a-breadcrumb-item>
          </a-breadcrumb>
          <h2 class="add_agreement">新增二级商协议</h2>
        </a-layout>

        <!-- 1、协议主体 -->
        <a-divider :dashed="true"><b class="b_title_icon">
            <div class="title_icon">1</div>协议主体
          </b></a-divider>
        <div class="protocol_subject">

          <!-- 协议客户 -->
          <div class="acquiesce_style">
            <span>*</span>
            <p>协议客户：</p>
            <a-button>选择客户</a-button>
            <p>上海也正医药有限公司</p>
          </div>

          <!-- 协议状态 -->
          <div class="acquiesce_style">
            <p>协议状态：</p>
            <a-space>
              <a-select ref="select" v-model:value="selectStatus" style="width: 120px">
                <a-select-option value="正常">正常</a-select-option>
                <a-select-option value="不正常">不正常</a-select-option>
              </a-select>
            </a-space>
          </div>

          <!-- 购进指标 -->
          <div class="acquiesce_style">
            <p>购进指标：</p>
            <a-space>
              <a-select ref="select" v-model:value="purchaseTarget" style="width: 120px">
                <a-select-option value="金额">金额</a-select-option>
                <a-select-option value="数量">数量</a-select-option>
              </a-select>
            </a-space>
            <a-space direction="vertical">
              <a-input placeholder="输入金额/数量" />
            </a-space>
          </div>

          <!-- 纯销指标 -->
          <div class="acquiesce_style">
            <p>纯销指标：</p>
            <a-button>金额</a-button>
            <a-space direction="vertical">
              <a-input placeholder="输入金额/数量" />
            </a-space>
          </div>

          <!-- 销售区域 -->
          <div class="acquiesce_style">
            <p>销售区域：</p>
            <a-select ref="select" v-model:value="salesTerritory" style="width: 120px">
              <a-select-option value="全国">全国</a-select-option>
              <a-select-option value="上海">上海</a-select-option>
            </a-select>
          </div>

          <!-- 签订时间 -->
          <div class="acquiesce_style">
            <p>签订时间：</p>
            <a-space direction="vertical" :size="12">
              <a-date-picker show-time placeholder="Select Time" />
            </a-space>
          </div>

          <!-- 购进渠道 -->
          <div class="purchase_channel">
            <div class="acquiesce_style">
              <p>购进渠道：</p>
              <a-select ref="select" v-model:value="designatedChannel" style="width: 120px">
                <a-select-option value="全国">指定渠道</a-select-option>
              </a-select>
              <a-button>请选择渠道</a-button>
            </div>

            <a-table :columns="columns" :data-source="tableData" :pagination="false">
            </a-table>
          </div>

        </div>

        <!-- 2、产品政策 -->
        <a-divider :dashed="true"><b class="b_title_icon">
            <div class="title_icon">2</div>产品政策
          </b></a-divider>
        <div class="product_policy">

          <!-- 产品指标 -->
          <div class="productPolicy">
            <a-button type="primary">添加产品</a-button>
            <p>购进总指标（万元）：<span>￥152.65</span></p>
            <p>指标按季度分解（万元）：<span>【Q1】￥12.5，【Q2】￥12.5，【Q3】￥12.5，【Q4】￥12.5</span></p>
            <p>纯销总指标（万元）：<span>￥152.65</span></p>
          </div>

          <!-- 选择产品 -->
          <div class="select_product">
            <!-- 选择产品 -->
            <div class="acquiesce_style">
              <p>产品：</p>
              <a-button>选择产品</a-button>
              <p>美复胶丸 24粒/盒</p>
            </div>
            <!-- 协议效期 -->
            <div class="acquiesce_style">
              <p>协议效期：</p>
              <a-space direction="vertical" :size="12">
                <a-date-picker show-time placeholder="Select Time" />
              </a-space>
            </div>
            <div class="del_button">
              <a-button danger>删除</a-button>
            </div>
          </div>

          <!-- 产品详情 -->
          <div class="product_details">

            <main>
              <header>
                <p>协议（元）</p>
                <p>票折（元）</p>
                <p>进购指标量（大单位）</p>
                <p>进购指标量（小单位）</p>
                <p>进购金额（万元）</p>
                <p>纯销指标（小单位）</p>
                <p>纯销指标金额（小单位）</p>
              </header>

              <footer>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>
              </footer>
            </main>

            <main>
              <header>
                <p>分销奖励</p>
                <p>科目费用</p>
                <p>零售配送</p>
                <p>费用科目</p>
                <p>医疗配送商</p>
                <p>费用科目</p>
                <p>自定义7</p>
                <p>自定义8</p>
              </header>

              <footer>
                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>

                <a-space>
                  <a-select ref="select" value="单选项" style="width: 182px">
                    <a-select-option value="正常">正常</a-select-option>
                  </a-select>
                </a-space>

                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>

                <a-space>
                  <a-select ref="select" value="多选项1" style="width: 182px">
                    <a-select-option value="正常">正常</a-select-option>
                  </a-select>
                </a-space>

                <a-space direction="vertical">
                  <a-input placeholder="请输入" />
                </a-space>

                <a-space>
                  <a-select ref="select" value="多选项1" style="width: 182px">
                    <a-select-option value="正常">正常</a-select-option>
                  </a-select>
                </a-space>

                <a-space direction="vertical" :size="12">
                  <a-date-picker show-time placeholder="Select Time" />
                </a-space>

                <a-space direction="vertical" :size="12">
                  <a-date-picker show-time placeholder="Select Time" />
                </a-space>
              </footer>
            </main>
          </div>
        </div>

        <!-- 2、补充协议 -->
        <a-divider :dashed="true"><b class="b_title_icon">
            <div class="title_icon">2</div>补充协议
          </b></a-divider>
        <div class="product_policy">
          <!-- 补充协议 -->
          <div class="icon_button_div">
            <a-button>补充协议1</a-button>
            <a-button>补充协议2</a-button>
            <a-button>补充协议3</a-button>
            <a-button type="primary" class="icon_button">新增</a-button>
          </div>

          <div class="supplementary_agreement">
            <main>
              <p>协议内容：</p>
              <section class="del_button2">
                <a-button danger>删除</a-button>
              </section>
            </main>
            <a-space direction="vertical">
              <a-textarea />
            </a-space>
          </div>
        </div>

      </a-layout-content>

      <!-- 页面尾部 -->
      <a-layout-footer class="footer_style">
        <a-button type="primary">保存</a-button>
      </a-layout-footer>
    </a-layout>

  </a-layout>
</template>

<script setup>
import { Layout } from 'ant-design-vue';
const { Header, Sider, Content, Footer } = Layout
import { ref, h, reactive } from 'vue';
import {
  MailOutlined,
  CalendarOutlined,
  AppstoreOutlined,
  SettingOutlined,
} from '@ant-design/icons-vue';

function getItem(label, key, icon, children, type) {
  return {
    key,
    icon,
    children,
    label,
    type,
  };
}

const siderItems = reactive([
  getItem('功能功能A', '1', h(MailOutlined), [
    getItem('功能功能A', '11'),
    getItem('功能功能A', '12'),
  ]),
  getItem('功能功能B', '2', h(CalendarOutlined), [
    getItem('功能功能B', '21'),
    getItem('功能功能B', '22'),
  ]),
  getItem('功能功能C', '3', h(AppstoreOutlined), [
    getItem('功能功能C', '31'),
    getItem('功能功能C', '32'),
  ]),
  getItem('功能功能D', '4', h(SettingOutlined), [
    getItem('功能功能D', '41'),
    getItem('功能功能D', '42'),
  ]),
  getItem('功能功能E', '5', h(SettingOutlined), [
    getItem('功能功能E', '51'),
    getItem('功能功能E', '52'),
  ]),
  getItem('功能功能F', '6', h(SettingOutlined), [
    getItem('功能功能F', '61'),
    getItem('功能功能F', '62'),
  ]),
]);

const headerItems = reactive([
  getItem('首页', '1', h(MailOutlined)),
  getItem('主数据', '2', h(CalendarOutlined)),
  getItem('辖区管理', '3', h(AppstoreOutlined)),
  getItem('销讯通', '4', h(SettingOutlined)),
]);

// 协议状态
const selectStatus = ref('正常');
// 购进指标
const purchaseTarget = ref('金额');
// 销售区域
const salesTerritory = ref('全国');
// 购进渠道
const designatedChannel = ref('指定渠道');

// 列表内容 - columns表格的具体配置
const columns = [
  {
    title: '指定渠道编码',
    dataIndex: 'number',
    key: 'number',
  },
  {
    title: '指定渠道名称',
    dataIndex: 'name',
    key: 'name',
  },
  {
    title: '所在省',
    dataIndex: 'address',
    key: 'address',
  },
];
// 数据数组
const tableData = [
  {
    key: '1',
    number: 'BJ000090',
    name: '宁波九州通药业有限公司',
    address: '浙江省',
  },
  {
    key: '2',
    number: 'BJ000192',
    name: '国药控股精华有限公司',
    address: '浙江省',
  },
  {
    key: '3',
    number: 'BJ000283',
    name: '老百姓药业有限公司',
    address: '浙江省',
  },
];


// const contentStyle = {
//   textAlign: 'center',
//   minHeight: 120,
//   // lineHeight: '120px',
//   color: '#fff',
//   backgroundColor: '#108ee9',
// };

const footerStyle = {
  textAlign: 'center',
  color: '#fff',
  backgroundColor: '#7dbcea',
};

</script>


<style scoped lang="scss">
.sider_style {
  // height: 100vh;
  height: 190vh;
  text-align: center;

  .logo {
    line-height: 1px;

    .corporation_title {
      color: #FFFFFFA6;
      box-sizing: content-box;

      img {
        width: 150px;
        margin-top: 10px;
      }

      div {
        font-size: 14px;
        margin: 10px 0 20px 0;
      }
    }
  }
}

.add_agreement {
  color: #000;
  margin: 0;
  text-align: left;
}

.content_style {
  background-color: #8080800f;

  .protocol_subject {
    margin: 0 10px;
    background-color: #fff;
    padding: 10px;
    display: flex;
    flex-wrap: wrap;
    // flex-direction: column;
  }

  .acquiesce_style {
    display: flex;
    align-items: center;
    // flex-basis: 50%;
    flex-basis: calc(50% - 10px);
    ;
    margin: 0 0 10px 10px;

    p {
      transform: translate(0, 30%);
      font-size: 16px;
    }

    span {
      color: red;
    }
  }

  .purchase_channel {
    width: 100%;
  }

}

.productPolicy {
  display: flex;
  // justify-content: space-between;

  p {
    margin: 0 20px;
    transform: translate(0, 20%);
  }

  span {
    font-weight: 600;
  }
}

.select_product {
  display: flex;
  margin: 10px 0;
  background-color: #fff;
  align-items: center;
  height: 50px;
}

.product_details {
  main {
    border: 1px solid #ccc;
    // padding: 5px 10px;
    background-color: #fff;
    margin-bottom: 10px;

    header {
      height: 40px;
      line-height: 40px;
      display: flex;
      justify-content: space-evenly;
      background-color: rgba(128, 128, 128, 15%);
      border-bottom: 1px solid #ccc;


      p {
        width: 180px;
      }
    }

    footer {
      display: flex;
      justify-content: space-around;
      height: 50px;
      line-height: 50px;
    }
  }
}

.supplementary_agreement {
  width: 100%;
  background-color: #fff;
  border: 1px solid #ccc;

  main {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  p {
    padding: 25px;
    margin: 0;
  }



  div {
    width: 100%;
    padding: 0 25px;
    margin-bottom: 30px;
  }
}

.footer_style {
  background-color: #fff;
}

.product_policy {
  margin: 0 10px;
}

.b_title_icon {
  display: flex;
}

.title_icon {
  color: #fff;
  background-color: skyblue;
  border-radius: 50%;
  margin-right: 10px;
  width: 25px;
  height: 25px;
}

.del_button {
  margin-right: 10px;
}

.del_button2,
.icon_button {
  position: absolute;
  right: 20px;
}

.icon_button {
  top: -10px;
  right: 10px;
}

.icon_button_div {
  position: relative;
}
</style>

<style></style>