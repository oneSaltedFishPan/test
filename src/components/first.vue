<template>
  <div>
    <div>
      <span class='cursor'>鼠标移上来查看放大效果吧</span>
    </div>
    <div>
      <span class='cursor'>鼠标移上来查看放大效果吧</span>
    </div>
    <div>
      <span class='cursor'>鼠标移上来查看放大效果吧</span>
    </div>
    <div>
      <span class='cursor'>鼠标移上来查看放大效果吧</span>
    </div>
    <div>
      <span class='cursor'>鼠标移上来查看放大效果吧</span>
    </div>
    <ul class="car-box">
      <li class="car_list" v-for="(list,index) in [1,2,3]" :key="index">
        <div class="car_img item">
          <img
            alt=""
            :src="data.car.carTypeImage"
          >
        </div>
        <div class="item">
          <p class="address">{{data.startAddress.province.name+data.startAddress.city.name+data.startAddress.district.name}}</p>
          <p>载货体积:{{data.car.carLong*data.car.carWidth*data.car.carHeight}} </p>
        </div>
        <div class="item">
          <p> {{data.hoursLength}}h</p>
          <p class="right">→</p>
          <p>{{data.distance}}km </p>
        </div>
        <div class="item">
          <p class="address"> {{data.endAddress.province.name+data.endAddress.city.name+data.endAddress.district.name}}</p>
          <p>载重:{{data.car.carLoad}} </p>
        </div>
        <div class="item">
          <p class="price">一口价：￥{{data.price}}</p>
          <p>累计已发：<span class="use-count">{{data.usageCount}}</span>车 </p>
        </div>
        <div class="item">
          <button class="btn">立即用车</button>
        </div>
      </li>
    </ul>

    <div class="count-down">
        <span :class="movceClass.includes('tens')?'move':''" class="time">{{tens}}</span>
        <span :class="movceClass.includes('units')?'move':''" class="time">{{units}}</span>
    </div>
    <div class="reset">
      <button @click="reset()" class="btn">重置</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "first",
  data() {
    return {
      msg: "",
      data: {
        id: 1,
        lineNo: "10000000000000",
        distance: 0.63,
        hoursLength: 0.37,
        price: 11122.32,
        usageCount: 0,
        startAddress: {
          province: {
            name: "山西省",
            code: "140000",
            level: {
              value: "first",
              desc: "first level"
            },
            postCode: "",
            longitude: "112.549248",
            latitude: "37.857014"
          },
          city: {
            name: "太原市",
            code: "140100",
            level: {
              value: "second",
              desc: "second level"
            },
            postCode: "030082",
            longitude: "112.549248",
            latitude: "37.857014"
          },
          district: {
            name: "晋源区",
            code: "140110",
            level: {
              value: "third",
              desc: "third level"
            },
            postCode: "030025",
            longitude: "112.47985",
            latitude: "37.72479"
          },
          street: null,
          detailAddress: null
        },
        endAddress: {
          province: {
            name: "内蒙古自治区",
            code: "150000",
            level: {
              value: "first",
              desc: "first level"
            },
            postCode: "",
            longitude: "111.670801",
            latitude: "40.818311"
          },
          city: {
            name: "包头市",
            code: "150200",
            level: {
              value: "second",
              desc: "second level"
            },
            postCode: "014025",
            longitude: "109.840405",
            latitude: "40.658168"
          },
          district: {
            name: "东河区",
            code: "150202",
            level: {
              value: "third",
              desc: "third level"
            },
            postCode: "014040",
            longitude: "110.0462",
            latitude: "40.58237"
          },
          street: null,
          detailAddress: null
        },
        car: {
          id: 3,
          typeName: "小微货",
          typeDesc: "≤80km运输，可在日用品、生鲜、建材、小家具、纺织品",
          loadingType: {
            value: "low_bar",
            desc: "低栏"
          },
          carLong: 2.7,
          carLoad: 1500.0,
          carHeight: 1.5,
          carWidth: 1.7,
          loadVolume: 6.88,
          carTypeImage:
            "https://johnniang.me/upload/2020/04/image-998528985f834a628dfa10f84d8291c7.png"
        }
      },
      timer:null,
      timeNumber:60,
      units:0,
      tens:6,
      movceClass:[]
    };
  },
  mounted() {
    this.coutDown()
  },
  methods: {
    reset(){
      clearInterval(this.timer);
      this.tens = 6;
      this.units = 0;
      this.timeNumber = 60;
      this.coutDown();
    },
    coutDown(){
      this.timer = setInterval(() => {
        this.timeNumber--;
        let splitNumber = this.timeNumber.toString().split('');
        
        if(splitNumber.length>=2){
          this.addMove(splitNumber[0],this.tens);
          this.units = splitNumber[1];
          this.tens = splitNumber[0];
        }else{
          this.addMove(0,this.tens);
          this.units = splitNumber[0];
          this.tens = 0;
        }
        if(this.timeNumber == 0){
          alert('倒计时已结束');
          clearInterval(this.timer);
        }
      }, 1000);
    },
    addMove(nowNumber,beforeNumber){
      this.movceClass.push('units');
      if(nowNumber!=beforeNumber){
        this.movceClass.push('tens');
      }
      setTimeout(() => {
        this.movceClass = [];
      }, 500);
    }
  },
};
</script>
<style scoped>
.reset{
  margin-top: 10px;
}
.count-down{
  font-size: 0;
   height: 100px;
   overflow: hidden;
}
.count-down .time{
  margin-right: 10px;
  font-size: 84px;
  color: #fff;
  position:relative;
  top: 0;
  opacity: 1;
  transition: all ease 0.5s;
  display: inline-block;
    width: 70px;
    height: 100px;
    border-radius: 4px;
    box-shadow: 1px 1px 1px rgba(4, 4, 4, 0.35);
    background-image: linear-gradient(bottom, rgb(22, 22, 22) 50%, #2a2a2a 50%);
    background-image: -o-linear-gradient(bottom, rgb(22, 22, 22) 50%, #2a2a2a 50%);
    background-image: -moz-linear-gradient(bottom, rgb(22, 22, 22) 50%, #2a2a2a 50%);
    background-image: -webkit-linear-gradient(bottom, rgb(22, 22, 22) 50%, #2a2a2a 50%);
    background-image: -ms-linear-gradient(bottom, rgb(22, 22, 22) 50%, #2a2a2a 50%);
    background-image: -webkit-gradient( linear, left bottom, left top, color-stop(0.5, rgb(22, 22, 22)), color-stop(0.5, #2a2a2a) );
}
  .count-down .time.move{
   animation:move 0.5s 1;
  -moz-animation:move 0.5s 1; /* Firefox */
  -webkit-animation:move 0.5s 1; /* Safari and Chrome */
  -o-animation:move 0.5s 1; /* Opera */
  }
  @keyframes move{
    0%{
      top: 0;
      opacity: 1;
    }
    50%{
      top: 100%;
      opacity: 0;
    }
    100%{
      top: -100%;
      opacity: 0;
    }
  }
  @-moz-keyframes move{
    0%{
      top: 0;
      opacity: 1;
    }
    50%{
      top: 100%;
      opacity: 0;
    }
    100%{
      top: -100%;
      opacity: 0;
    }
  }
  @-webkit-keyframes move{
    0%{
      top: 0;
      opacity: 1;
    }
    50%{
      top: 100%;
      opacity: 0;
    }
    100%{
      top: -100%;
      opacity: 0;
    }
  }
.cursor {
  transition: all ease 0.5s;
  display: inline-block;
}
.cursor:hover,.car_img:hover img{
  transform: scale(1.5, 1.5);
}
.car_img {
  width: 100px;
  overflow: hidden;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.car_img img {
  height: 120px;
  transition: all ease 0.5s;
}
.btn {
  transition: all ease 0.5s;
  background: #2474b5;
  color: #fff;
  padding: 10px 20px;
  outline: 0 none;
  border: 0 none;
  border-radius: 4px;
}
.btn:hover {
  cursor: pointer;
  opacity: 0.8;
}
.car-box {
  border: 1px solid #ccc;
  border-radius: 4px;
  max-width: 1200px;
  margin: 40px auto;
}
.car_list {
  width: 100%;
  padding: 10px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #ccc;
  transition: all ease 0.2s;
}
.car_list:last-child {
  border: 0 none;
}
.car_list .item {
  flex: 1;
}
.car_list:hover{
  background: #ececec;
}
.right {
  line-height: 20px;
  font-size: 30px;
}
.use-count,
.price {
  color: red;
  font-size: 20px;
}
.address {
  padding: 10px;
  font-size: 18px;
  font-weight: bold;
}
</style>
