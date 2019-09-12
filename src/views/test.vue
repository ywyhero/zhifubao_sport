<template>
  <div class="home">
    <canvas id="mycanvas" :width="c_size" :height="c_size" :style="style"></canvas>
  </div>
</template>

<script>
// @ is an alias to /src
import Highcharts from 'highcharts/highstock';
export default {
  name: 'home',
  data() {
    return {
      size: 400,
      c_size: 400,
      cirX: 200,
      cirY: 200,
      i_radius: 80, // 内圈半径
      o_radius: 80, // 外圈半径
      o_width: 30, // 外圈线宽度
      i_width: 30, // 内圈线宽度
      style: {
          'width': '80px',
          'height': '80px'
      },
    }
  },
  components: {
  },
  created() {
      this.c_size = this.size * 2
      this.style.width = this.size + 'px'
      this.style.height = this.size + 'px'
      this.i_width = this.line
      this.o_width = this.line
      this.i_radius = (this.size - this.o_width) / 2
      this.o_radius = (this.size - this.i_width) / 2
  },
  methods: {
    draw(context, i) {
      // 大圆框
      context.beginPath();
      context.lineWidth = 1 ;
      context.arc(this.size / 2, this.size / 2, 104 , 0, Math.PI * 2);
      context.strokeStyle = "grey";
      context.stroke();
      // 大圆
      context.beginPath();
      var grd = context.createLinearGradient(0,0,80 ,80 );
      grd.addColorStop(1,"blue");
      context.arc(this.size / 2 , this.size / 2 , 100 , 80, Math.PI * 2  * (i / 100) + 80);
      context.lineWidth = 10 ;
      context.lineCap = "round";
      context.strokeStyle = grd;
      context.stroke();
      // 小圆
      context.beginPath();
      context.arc(this.size / 2 , this.size / 2, 95 , 0, Math.PI * 2 );
      context.lineWidth = 1 ;
      context.strokeStyle = "grey";
      context.stroke();
      context.fillStyle = "white";
      context.fill();
      // 字
      context.beginPath();
      context.textBaseline = "middle";
      context.textAlign = "center";
      context.font = "20px Arial";
      context.fillStyle = "black";
      context.fillText(i + "%", this.size / 2 , this.size / 2);
    }
  },
  mounted() {
    let canvas = document.getElementById("mycanvas");
    canvas.width = this.size * 2
    canvas.height= this.size * 2
    let context = canvas.getContext("2d");
    context.scale(2, 2)
    this.cirX = this.size / 2, // 直径的一半
    this.cirY = this.size / 2, // 直径的一半
    this.rad = Math.PI * 2 / 100
    // function 
    // var i = 0;
    // var progress = parseInt(90);
    this.draw(context, 90)
    // var timer = setInterval(function(){
    //   if(i >= progress){
    //     clearInterval(timer);
    //   }
    //   // context.scale(2, 2);
    //   context.clearRect(0, 0, canvas.width, canvas.height);
    //   draw(i);
    //   i++;
    // },30);
  }
}
</script>
