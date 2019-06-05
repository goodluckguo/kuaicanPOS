<template>
  <div class="pos">
    <el-row>
      <el-col :span="7" id="order-list">
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table stripe border style="width: 100%" :data="tableData">
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="price" label="价格"></el-table-column>
              <el-table-column prop="count" label="地址"></el-table-column>
              <el-table-column label="操作" fixed="right" width="150px">
                <template scope="scope">
                  <el-button type="text" size="medium" @click="delSinfleGoods(scope.row)">删除</el-button>
                  <el-button type="text" size="medium" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <el-row style="margin-top:30px">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAllGoods">删除</el-button>
              <el-button type="success" @click="checkout">结账</el-button>
            </el-row>
            <div class="totalDiv">
              <small>数量</small>
              ：{{totalCount}}
              <small>总价</small>
              ：{{totalMoney}}
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">挂单</el-tab-pane>
          <el-tab-pane label="外卖">外卖</el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="17">
        <div class="often-goods">
          <div class="title">热销商品</div>
          <div class="often-good-list">
            <ul>
              <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                <span>{{goods.goodsName}}</span>
                <span class="o-price">￥{{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <ul class="cookList">
                <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                  <span class="foodImg">
                    <img :src="goods.goodsImg" width="100%">
                  </span>
                  <span class="foodName">{{goods.goodsName}}</span>
                  <span class="foodPrice">￥{{goods.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="饮料"></el-tab-pane>
            <el-tab-pane label="小吃"></el-tab-pane>
            <el-tab-pane label="套餐"></el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </div>
</template>
<script>
export default {
  name: 'Pos',
  data() {
    return {
      tableData: [],
      totalCount: '',
      totalMoney: '',
      oftenGoods: [
        {
          goodsId: 1,
          goodsName: '香辣鸡腿堡',
          price: 18
        },
        {
          goodsId: 2,
          goodsName: '田园鸡腿堡',
          price: 15
        },
        {
          goodsId: 3,
          goodsName: '和风汉堡',
          price: 15
        },
        {
          goodsId: 4,
          goodsName: '快乐全家桶',
          price: 80
        },
        {
          goodsId: 5,
          goodsName: '脆皮炸鸡腿',
          price: 10
        },
        {
          goodsId: 6,
          goodsName: '魔法鸡块',
          price: 20
        },
        {
          goodsId: 7,
          goodsName: '可乐大杯',
          price: 10
        },
        {
          goodsId: 8,
          goodsName: '雪顶咖啡',
          price: 18
        },
        {
          goodsId: 9,
          goodsName: '大块鸡米花',
          price: 15
        },
        {
          goodsId: 20,
          goodsName: '香脆鸡柳',
          price: 17
        }
      ],
      type0Goods: [
        {
          goodsId: 1,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '香辣鸡腿堡',
          price: 18
        },
        {
          goodsId: 2,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '田园鸡腿堡',
          price: 15
        },
        {
          goodsId: 3,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '和风汉堡',
          price: 15
        },
        {
          goodsId: 4,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '快乐全家桶',
          price: 80
        },
        {
          goodsId: 5,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '脆皮炸鸡腿',
          price: 10
        },
        {
          goodsId: 6,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '魔法鸡块',
          price: 20
        },
        {
          goodsId: 7,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '可乐大杯',
          price: 10
        },
        {
          goodsId: 8,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '雪顶咖啡',
          price: 18
        },
        {
          goodsId: 9,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559716120292&di=c810582dcf60ff88759762f0c156daac&imgtype=0&src=http%3A%2F%2Fwww.8887.tv%2Fupload%2F201705%2F08%2F201705081120261198.jpg',
          goodsName: '大块鸡米花',
          price: 15
        },
        {
          goodsId: 20,
          goodsImg:
            'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559657920807&di=96eb8cdd5a6731d893f3b3213e8802ed&imgtype=0&src=http%3A%2F%2Fe.hiphotos.baidu.com%2Fbainuo%2Fcrop%3D0%2C0%2C690%2C418%3Bw%3D470%3Bq%3D80%2Fsign%3Dcb42e3bc5f2c11dfca9ee5635e174ee0%2F71cf3bc79f3df8dc789babcec511728b461028ce.jpg',
          goodsName: '香脆鸡柳',
          price: 17
        }
      ]
    }
  },
  mounted: function() {
    var orderHeight = document.body.clientHeight
    document.getElementById('order-list').style.height = orderHeight + 'px'
  },
  methods: {
    //添加订单列表的方法
    addOrderList(goods) {
      this.totalCount = 0
      this.totalMoney = 0
      let isHave = false

      //判断这个商品是否已经存在
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId == goods.goodsId) {
          isHave = true
          //商品存在
        }
      }
      //根据ishave的值判断商品在订单列表u中是否已经存在
      if (isHave) {
        //在订单列表中筛选出已经存在的商品，改变数量
        let arr = this.tableData.filter(o => o.goodsId == goods.goodsId)
        arr[0].count++
      } else {
        //bu商品不存在的话就将商品推送到列表内
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        }
        this.tableData.push(newGoods)
      }
      //进行数量和价格的计算
      this.getAllMoney()
    },
    delSinfleGoods(goods) {
      console.log(goods)
      this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId)
      this.getAllMoney()
    },
    //汇总金额
    getAllMoney() {
      this.totalCount = 0
      this.totalMoney = 0
      if (this.tableData) {
        this.tableData.forEach(element => {
          this.totalCount += element.count
          this.totalMoney = this.totalMoney + element.count * element.price
        })
      }
    },
    delAllGoods() {
      this.tableData = []
      this.totalCount = 0
      this.totalMoney = 0
    },
    checkout() {
      if (this.tableData != 0) {
        this.tableData = []
        this.totalCount = 0
        this.totalMoney = 0
        this.$message({
          message: '结账成功，感谢你们又为店里做出的贡献',
          type: 'success'
        })
      } else {
        this.$message.error('没有订单需要结算')
      }
    }
  }
}
</script>
<style scoped>
el-tab-pane {
  text-align: center;
}
el-table-column {
  text-align: center;
}
.title {
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  color: hotpink;
  height: 38px;
  line-height: 38px;
}
.often-goods ul li {
  width: 160px;
  list-style: none;
  float: left;
  border: 1px solid deeppink;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
}
.o-price {
  color: #58b7ff;
}
.cookList li {
  list-style: none;
  width: 25%;
  border: 1px solid #e5e9f2;
  height: auot;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
.goods-type {
  clear: both;
}
.totalDiv {
  background-color: #d3dce6;
  border-bottom: #58b7ff;
  padding: 10px;
}
#order-list {
  overflow: auto;
}
</style>
