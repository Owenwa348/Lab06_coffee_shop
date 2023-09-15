<script setup>
import{ ref }from "vue"
//import 

//ตัวแปร
const selectedTime = ref("")
const travel =ref("")
const money =ref("")
const travelList =ref([
                      {name:'Mo-Mo-Paradise', adult:659,child:329,Setmenu:{1:"MoMoParadise Gold",2:"MoMoParadise Standard"},
                      img: "https://img.wongnai.com/p/400x0/2021/12/02/0d42a3543e0f465a9288f50bae220739.jpg",ListSetmanu:null,Listtable:null },
                      {name:'AKIYOSHI', adult: 599,child: 299,Setmenu :{1:"STANDARD BUFFET" ,2:"DELUXE BUFFET"},
                      img: "https://f.ptcdn.info/686/063/000/pqlwuv44lDNL45Kw83A-o.jpg",ListSetmanu:null,Listtable:null },
                      {name:'Kagonoya', adult: 549,child: 275,Setmenu :{1:"Kaminabe Pock Shabu",2:"Kaminabe Bacon Shabu",3:"Sukiyaki Pock",4:"Milfille Kutsutoji"},
                      img: "https://www.ryoiireview.com/upload/editor_review/202112/1638852621_db795edc4d74f3f820e8f69d68b718e2.jpg",ListSetmanu:null,Listtable:null },
                      {name:'tajimaya shabu', adult: 530,child: 265 ,Setmenu :{1:"Wagyu Loin&Bara" ,2:"Australian Loin&Bara"},
                      img: "https://hello2day.com/wp-content/uploads/2019/02/tajimaya-thailand-central-world-isetan-1.jpg",ListSetmanu:null,Listtable:null },
                      {name:'masaru shabu & sushi buffet', adult: 690,child: 270 ,Setmenu :{1:"Preimum",2:"Platinum "},
                      img: "https://kiji.life/eats/wp-content/uploads/2020/01/masaru-shabu-fcm_0406-1024x682.jpg",ListSetmanu:null,Listtable:null },
                      {name:'shiroku shabu', adult: 389,child: 389 ,Setmenu :{1:"Standard",2:"Deluxe",3:"Premium "},
                      img: "https://www.ryoiireview.com/upload/editor_review/201606/1466746327_5b53f0b203a2cfa94ce924ab9b910e7d.jpg",ListSetmanu:null,Listtable:null },
                    ])
//เก็บข้อมมูลการจอง
const bookingList = ref([
  // "Mo-Mo-Paradise","AKIYOSHI","Kagonoya","tajimaya shabu","masaru shabu & sushi buffet"
]);

//function
function booking(item){
bookingList.value.push(item);
}


function submit(){
  const forms = document.querySelectorAll('.needs-validation');
  let isValid = true;
  Array.from(forms).forEach(form => {
    if (!form.checkValidity()) {
      form.classList.add('was-validated');
      isValid = false;
    }
  });
  if (isValid) {
    bookingList.value=[];
  }
}



function reset(){
travel.value =" ";
money.value =" ";

travelList.value.forEach(item =>{
  item.ListSetmanu=null;
  item.Listtable=null;
})
bookingList.value =[];
}


(() => {
  'use strict'
  const forms = document.querySelectorAll('.needs-validation')
  Array.from(forms).forEach(form => {
    form.addEventListener('submit', event => {
      if (!form.checkValidity()) {
        event.preventDefault()
        event.stopPropagation()
      }
      form.classList.add('was-validated')
    }, false)
  })
})()



</script>

<template>
  <div>
    <h1 class="" >กินอะไรดี??</h1>
    <!-- <input type="radio" value="a" v-model ="travel">สรรสัร
    <input type="radio" value="b" v-model ="travel">นั่งดื่ม
    <br> -->

    <div class="container text-center">
      <div class="row">
        <div class="col" v-for="(i,indix) in travelList" :key="indix"> 
          <div class="card text-bg-info h-100" style = "width:23.5rem">
            <div class="card-body">
              <img :src="i.img" class="card-img-top" alt="">
              <h5 class="text-uppercase">{{ i.name }}</h5>
              <p class="card-text-dark bg-white">ราคาสำหรับผู้ใหญ่ {{ i.adult }} บาท</p>
              <p class="card-text-dark bg-white">ราคาสำหรับเด็ก{{ i.child }} บาท</p>
              <p class="card-text-dark bg-white">เซตอาหาร</p>
              <select v-model="i.ListSetmanu" class="form-select-indicator-color" aria-label="Default select example" required="">
                <option value="" disabled selected>โปรดเลือก</option> 
                <option v-for="(menu) in i.Setmenu" :value="menu"> {{ menu }}</option>

              </select>
              <p class="card-text">จำนวนที่นั้ง</p>
              <select v-model="i.Listtable" class="form-select-indicator-color" aria-label="Default select example" required="">
                <option value="" disabled selected>จำนวน</option> 
                <option value="1">1 ที่</option>
                <option value="2">2 ที่</option>
                <option value="3">3 ที่</option>
                <option value="3">4 ที่</option>
                <option value="3">5 ที่</option>
                <option value="3">6 ที่</option>
              </select>
              <br>
              <a class="btn btn-primary" @click="booking(i)" >จองโต๊ะ</a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <br>
    <table class="table" v-if="bookingList.length > 0"> 
      <thead>
        <tr class="table-primary">
          <th scope="col">ลำดับ</th>
          <th scope="col">ชื่อร้าน</th>
          <th scope="col">ราคาสำหรับผู้ใหญ่</th>
          <th scope="col">ราคาสำหรับเด็ก</th>
          <th scope="col">เซตอาหาร</th>
          <th scope="col">จำนวนโต็ะ</th>
        </tr>
      </thead>
      <tbody class="table-group-divider">
          <tr v-for="(item, index) in bookingList" :key="index">
            <th class="table-primary" scope="row">{{ index+1 }}</th>
            <td>{{ item.name }}</td>
            <td>{{ item.adult }}</td>
            <td>{{ item.child }}</td>
            <td>{{ item.ListSetmanu }}</td>
            <td>{{ item.Listtable }} ที่</td>
          </tr>
      </tbody>
    </table>
    <br>
    <form class="row g-3 needs-validation" v-if="bookingList.length > 0">
      <div class="col-md-4">
        <label for="fname" class="form-label">ชื่อ</label>
        <input type="text" class="form-control" id="fname" required>
      </div>
      <div class="col-md-4">
        <label for="lname" class="form-label">นามสกุล</label>
        <input type="text" class="form-control" id="lname" required >
      </div>
      <div class="col-md-4">
        <label for="phone number" class="form-label">เบอโทร</label>
        <div class="input-group has-validation">
          <input type="tel" class="form-control" id="phone number" required>
        </div>
      </div>
      <div class="col-md-6">
        <label for="address" class="form-label">เมือง</label>
        <input type="text" class="form-control" id="address" required>
      </div>
      <div class="col-md-3">
        <label for="time" class="form-label">เวลา</label>
        <select v-model="selectedTime" class="form-select" id="time" required>
          <option selected disabled value="">เวลา</option>
          <option value="1">9:00 - 12:00 น. </option>
          <option value="2">13:00 - 16:00 น. </option>
          <option value="3">17:00 - 22:00 น. </option>
        </select>
      </div>
      <div class="col-md-3">
        <label for="Day" class="form-label">วันที่</label>
        <input type="date" class="form-control" id="Day" required>
      </div>
      <div class="col-12">
        <button @click="submit" class="button" fdprocessedid="py7jnc">ตกลง</button>
        <button @click="reset" class="button1" fdprocessedid="py7jnc">ล้างข้อมูล</button>
      </div>
    </form>
 


  </div>

</template>

    <!-- <div  v-for="(i,indix) in travelList" :key="indix" >
      {{ indix+1 }}
      ชื่อ {{ i.name }}
      ราคา {{ i.adult }} บาท
      ขนาด {{ i.child }} บาท
      รูป แผนที่
    </div>-->
    <!-- <br>
    <input type="numder" v-model="money">
    <br>
    <p v-if="money == 0">กรุณาใส่จำนวนเงิน</p>
    <p v-else-if="money >= 0 && money <100">นอนวัด </p>
    <p v-else-if="money >= 100 && money <1000">อยู่บ้านนอน</p>
    <p v-else-if="money >= 1000 && money <1000000">ขึ้นรถไปเที่ยว</p>
    <p v-else>ขับเครื่องบินส่วนตัวไป</p>
    <br>
    <button v-if="money >= 100 ">เดินทาง</button>
    <br> -->



    <!-- <div v-if="travel=='a'">ภูเขา
    <img src="src/assets/The_Elder_Scrolls_V_Skyrim_dragon-189506.jpg!d" alt=""></div>
    <div v-else>ทะเล
      <img src="src/assets/2020-07-28_23.26.37.jpg" alt="">
    </div> -->
        <!-- <div class="dropdown" data-bs-theme="light">
      <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonLight" data-bs-toggle="dropdown" aria-expanded="false">
    จุดจองโต็ะ
      </button>
      <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonLight">
        <li><a class="dropdown-item active" href="#">ด้านหน้า</a></li>
        <li><a class="dropdown-item" href="#">ตรงกลาง</a></li>
        <li><a class="dropdown-item" href="#">ด้านหลัง</a></li>
        <li><a class="dropdown-item" href="#">Something else here</a></li>
      </ul>
    </div>
    <div class="dropdown" data-bs-theme="dark">
      <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButtonDark" data-bs-toggle="dropdown" aria-expanded="false">
     Dark dropdown
      </button>
      <ul class="dropdown-menu" aria-labelledby="dropdownMenuButtonDark">
        <li><a class="dropdown-item active" href="#">Action</a></li>
        <li><a class="dropdown-item" href="#">Action</a></li>
        <li><a class="dropdown-item" href="#">Another action</a></li>
        <li><a class="dropdown-item" href="#">Something else here</a></li>
        <li><hr class="dropdown-divider"></li>
        <li><a class="dropdown-item" href="#">Separated link</a></li>
      </ul>
    </div>-->