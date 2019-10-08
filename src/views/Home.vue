<template>
  <div class="home">
    <div class="home-title">
      <div class="home-name">
        <img :src="myInfo.path ? myInfo.path : path" class="home-name-img"/>
        <span class="home-name-val">{{myInfo.name}}</span>
      </div>
      <div class="home-right">
         <span class="home-right-val">行走</span>
      </div>
     
    </div>
    <div class="home-canvas">
      <canvas id="mycanvas" :width="size" :height="size"></canvas>
      <div class="home-btn" v-if="isShow">立即捐步</div>
      <div class="home-des" v-if="isShow">今日可兑换公益基金生育53.2万元</div>
       <div class="home-bottom" v-if="isShow">
        <span class="home-bottom-btn">运动卡币</span>
        <span class="home-bottom-btn">运动记录</span>
      </div>
    </div>
    <div class="home-today">
      <span class="home-today-val">今日排行榜</span>
      <div class="home-today-bottom">
        <div class="home-today-left">
          <div class="home-today-info">
            <img :src="myInfo.path ? myInfo.path : path" class="home-today-my-img"/>
            <div class="home-today-my">
              <span class="home-today-my-name">{{myInfo.name}}</span>
              <span class="home-today-my-count">第{{myInfo.count}}名</span>
            </div>
          </div>
          <div class="home-today-count" :class="myInfo.step < 1000 ? 'active' : ''">{{myInfo.step}}步</div>
        </div>
        <div class="home-today-right">
          <span class="home-today-right-count" :class="myInfo.isZan ? 'active' : ''">{{myInfo.zanCount}}</span>
          <img class="home-today-right-icon" :src="myInfo.isZan ? require('./../assets/zan1.png') : require('./../assets/zan.png')"/>
        </div>
      </div>
    </div>
    <div class="home-lists">
      <div class="home-list" :class="item.isSelf ? 'active' : ''" v-for="(item, index) in lists" :key="index">
        <div class="home-list-count">{{item.count}}</div>
        <div class="home-today-left">
          <div class="home-today-info">
            <img :src="item.path" class="home-today-my-img"/>
            <div class="home-today-my">
              <span class="home-today-my-name">{{item.name}}</span>
              <span class="home-today-my-count" v-show="item.isOffer">已捐{{item.money}}元</span>
            </div>
          </div>
          <div class="home-today-count" :class="item.step < 1000 ? 'active' : ''">{{item.step}}步</div>
        </div>
        <div class="home-today-right">
          <span class="home-today-right-count" :class="item.isZan ? 'active': ''">{{item.zanCount}}</span>
          <img class="home-today-right-icon" :src="item.isZan ? require('./../assets/zan1.png') : require('./../assets/zan.png')"/>
        </div>
      </div>
    </div>
    <div class="home-bottom-des">没有更多好友了</div>
    <img src="./../assets/timg.jpeg" id="img" style="position: absolute; transform: translateX(-99999px)"/>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'home',
  data() {
    return {
      size: 240,
      rato: 10,
      i: 0,
      step: 0,
      path: require('./../assets/default.jpeg'),
      myInfo: {},
      isShow: false,
      lists: []
    }
  },
  components: {
  },
  async created() {
    await this.getLists()
  },
  watch: {
    step(newVal, oldVal) {
      if(newVal !== 0) {
        this.rotateCircle()
      }
    }
  },
  methods: {
    getLists() {
      new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1)
        }, 1000)
      }).then(data => {
        this.lists = [{
          count: 1,
          name: 'vine',
          step: 20547,
          isOffer: false,
          money: 0,
          isSelf: false,
          isZan: false,
          zanCount: 0,
          path: 'https://oss-test001.pnlyy.com//miniapp/ba8b-2376-40c8-9710-1555652806519.jpg'
        }, {
          count: 2,
          name: '无风',
          step: 12000,
          isOffer: true,
          money: 0.18,
          isSelf: true,
          isZan: false,
          zanCount: 2,
          path: 'https://oss-test001.pnlyy.com//tmp/wx72c40f1b2b03e842.o6zAJswCK901GC20JWPVE34uHShA.M5hEUSOOQ27Cf9b1a3670f3f490cd4d3d74c99ab169b.jpg'
        }, {
          count: 3,
          name: '无风1',
          step: 14200,
          isOffer: true,
          money: 0.18,
          isZan: false,
          zanCount: 9,
          isSelf: false,
          path: 'https://oss-test001.pnlyy.com//miniapp/031e-03b5-4077-8520-1555652614670.jpg'
        }, {
          count: 4,
          name: '无风2',
          step: 4200,
          isOffer: true,
          money: 0.18,
          isSelf: false,
          isZan: false,
          zanCount: 8,
          path: 'https://oss-test001.pnlyy.com//tmp/wx32f00376fddf6b44.o6zAJswCK901GC20JWPVE34uHShA.V38tLLHT9YXC61cad0382eeb69a93cc08a94ba4d1163.jpeg'
        }, {
          count: 5,
          name: '无风3',
          step: 200,
          isOffer: true,
          money: 0.18,
          isSelf: false,
          isZan: true,
          zanCount: 5,
          path: 'https://oss-test001.pnlyy.com//miniapp/8b2f-b47a-40b7-e561-1555652387432.jpg'
        }]
        this.myInfo = this.lists.find(v => v.isSelf === true);
      })
      
    },
    getData() {
      new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(1500)
        }, 1000)
      }).then(data => {
        this.step = this.myInfo.step
        this.isShow = true
        this.rato = this.step > 5000 ? this.step / 500 : 50;
      })
      
    },
    drawCircle() {
      // 默认灰色的圆
      this.context.beginPath();
      this.context.arc(this.size / 2, this.size / 2, 100 , 0,  Math.PI * 2 );
      this.context.lineWidth = 6 ;
      this.context.strokeStyle = '#f1f1f1';
      this.context.stroke();
    },
    drawCircleColor(i = this.i) {
      this.drawCircle()
      // 蓝色动画圆
      this.context.beginPath();
      let grd = this.context.createLinearGradient(0, 0, 0, 360);
      grd.addColorStop(0,"#4ba8fa");
      grd.addColorStop(0.5,"#69b2f4");
      grd.addColorStop(1,"#4ba8fa");
      let radio = (this.step / this.rato) < 100 ? 100 : (this.step / this.rato) 
      this.context.arc(this.size / 2, this.size / 2, 100 , -Math.PI / 2, -Math.PI / 2 +  Math.PI * 2  * (i / radio ));
      this.context.lineWidth = 10 ;
      this.context.lineCap = "round";
      this.context.strokeStyle = grd;
      this.context.stroke();
      if(this.step === 0) {
        this.drawImg()
      } else {
        clearInterval(this.timer)
        this.drawText()
      }
      
    },
    drawImg () {
        let img = document.getElementById('img')
        let index = 0;
        let _this = this;
        img.onload = function () {
          _this.context.drawImage(img, index * 85 + 10, 95, 90, 100, 85, 85, 70, 80);
        }
        
        // this.timer = setInterval(() => {
        //     index++;
        //     this.context.drawImage(img, index * 100, 95, 90, 100, 85, 85, 65, 80);
        //       if(index >= 4){
        //           index =0;
        //       }
        // },500);
      
    },
    drawText() {
      // 字
      this.context.beginPath();
      this.context.textBaseline = "middle";
      this.context.textAlign = "center";
      this.context.fillStyle = "black";
      this.context.font = "20px Arial blod";
      this.context.fillText('今日步数', this.size / 2 , this.size / 2 - 20);
      this.context.font = "20px Arial";
      this.context.fillStyle = "#a1a1a1";
      this.context.fillText(this.i * this.rato, this.size / 2 , this.size / 2 + 20);
    },
    rotateCircle() {
        let progress = this.step / this.rato ;
        console.log(progress)
        if(this.i > progress) return;
        this.context = this.canvas.getContext('2d')
        
        this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
        this.drawCircleColor();
        if(progress - this.i > 50) {
          this.i += 5;
        } else {
          this.i += 1;
        }
        
        requestAnimationFrame(this.rotateCircle)
    },
  },
  async mounted() {
    this.canvas = document.getElementById("mycanvas");
    let width = this.canvas.width
    let height = this.canvas.height
    this.context = this.canvas.getContext("2d");
    if(window.devicePixelRatio) {
      this.canvas.style.width = width + 'px'
      this.canvas.style.height = height + 'px'
      this.canvas.width = width * window.devicePixelRatio
      this.canvas.height = height * window.devicePixelRatio
       this.context.scale(window.devicePixelRatio, window.devicePixelRatio)
    }
    this.getData()
    this.drawCircleColor();
    
  }
}
</script>
<style lang="less" scoped>
@baseFontSize: 75; //基于视觉稿横屏尺寸/100得出的基准font-size
.px2rem(@name, @px) {
    @{name}: @px / @baseFontSize * 1rem;
}
.home {
  width: 100%;
  min-height: 100%;
  background: #f5f5f5;
  // overflow: auto;
}
.home-title{
  width: 100%;
  .px2rem(height, 90);
  .px2rem(padding-top, 10);
  .px2rem(padding-bottom, 10);
  .px2rem(padding-left, 30);
  .px2rem(padding-right, 30);
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.home-name{
  background: #fff;
  display: flex;
  align-items: center;
  .px2rem(height, 70);
  .px2rem(border-radius, 70);
  .px2rem(padding, 10);
}
.home-name-val{
  .px2rem(margin-left, 10);
}
.home-name-img{
  .px2rem(width, 50);
  .px2rem(height, 50);
  .px2rem(border-radius, 50);
  object-fit: cover;

}
.home-name-val{

}
.home-right{
  background: #fff;
  .px2rem(height, 70);
  .px2rem(line-height, 70);
  .px2rem(width, 120);
  .px2rem(border-radius, 70);
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
.home-right-val{
  background: #4ba8fa;
  .px2rem(height, 50);
  .px2rem(line-height, 50);
  .px2rem(width, 100);
  .px2rem(border-radius, 50);
  .px2rem(font-size, 28);
  color: #fff;
  text-align: center;
}
.home-des{
  text-align: center;
  .px2rem(font-size, 24);
  color: #a5a5a5;
  .px2rem(margin-top, 20);
  .px2rem(margin-bottom, 20);
}
.home-canvas{
  .px2rem(width, 720);
  .px2rem(padding-top, 20);
  // .px2rem(padding-bottom, 20);
  .px2rem( border-radius, 8);
  margin: 0 auto;
  background: #fff;
}
#mycanvas{
  display: block;
  margin: 0 auto;
}
.home-btn{
  .px2rem(width, 600);
  .px2rem(height, 70);
  .px2rem(line-height, 70);
  .px2rem(border-radius, 70);
  .px2rem(margin-top, 20);
  .px2rem(margin-bottom, 10);
  text-align: center;
  .px2rem(font-size, 28);
  color: #fff;
  background: linear-gradient(to right, #69b2f4 0%, #4ba8fa 100%);
  margin-left: auto;
  margin-right: auto;
}
.home-bottom{
  display: flex;
  border-top: 1px solid #f5f5f5;
}
.home-bottom-btn{
  flex: 1;
  .px2rem(padding-top, 20);
  .px2rem(padding-bottom, 20);
  text-align: center;
  color: #4ba8fa;
  border-right: 1px solid #f5f5f5;
}
.home-bottom-btn:nth-of-type(2n) {
  border-right: none;
}
.home-today{
  .px2rem(margin-top, 60);
  .px2rem(margin-bottom, 20);
  background: #fff;
  display: flex;
  flex-direction: column;
}
.home-today-val{
  .px2rem(padding-top, 20);
  .px2rem(padding-bottom, 20);
  .px2rem(padding-left, 20);
  color: #000;
  .px2rem(font-size, 30);
  font-weight: 700;
  border-bottom: 1px solid #f5f5f5;
}
.home-today-bottom{
  display: flex;
  .px2rem(padding-left, 100);
  .px2rem(padding-right, 30);
  .px2rem(padding-top, 20);
  .px2rem(padding-bottom, 20);
  align-items: center;
}
.home-today-left{
  display: flex;
  flex: 1;
  .px2rem(padding-right, 30);
  justify-content: space-between;
  align-items: center;
}
.home-today-info{
  display: flex;
  align-items: center;
}
.home-today-my-img{
  .px2rem(width, 80);
  .px2rem(height, 80);
  .px2rem(border-radius, 80);
  .px2rem(margin-right, 20);
  border: 2px solid #f60;
  object-fit: cover;

}
.home-today-right{
  .px2rem(width, 30);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.home-today-my{
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.home-today-my-name{
  .px2rem(font-size, 28);
  color: #000;
}
.home-today-my-count{
  .px2rem(font-size, 24);
  color: #a5a5a5;
}
.home-today-count{
  color: #f60;
  .px2rem(font-size, 44);
}
.home-today-count.active{
  color: #4ba8fa;
}
.home-today-right-count{
  .px2rem(font-size, 24);
  color: #a5a5a5;
}
.home-today-right-count.active{
  color: #f60;
}
.home-today-right-icon{
  .px2rem(width, 30);
  .px2rem(height, 30);
}
.home-list{
  background: #fff;
  display: flex;
  align-items: center;
  .px2rem(padding-top, 20);
  .px2rem(padding-bottom, 20);
  border-bottom: 1px solid #f5f5f5;
  .home-list-count{
    .px2rem(width, 40);
  }
  .home-today-my-img{
    border: none;
  }
  .home-today-right{
     .px2rem(margin-right, 30);
  }
}
.home-list.active{
  background: #f1f1f1;
}
.home-list:last-child{
  border: none;
}
.home-list-count{
  .px2rem(margin-left, 30);
  .px2rem(margin-right, 30);
  .px2rem(font-size, 40);
  color: #a1a1a1;

}
.home-bottom-des{
  .px2rem(font-size, 24);
  text-align: center;
  color: #a1a1a1;
  .px2rem(line-height, 60);
}
</style>
