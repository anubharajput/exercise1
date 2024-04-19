<script>
export default {
  data() {
    return {
      user: {
        name: 'Anubha Rajput',
        address: '123 Main Street',
        dob: '2000-10-21'
      },
      age: null,
      showAge: null,
      isError: null,
      users: [
        { name: 'Rahul', age: 24, imageUrl:"https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/35af6a41332353.57a1ce913e889.jpg"},
        { name: 'Rohit', age: 20, imageUrl:"https://s3-eu-west-1.amazonaws.com/files2.fd.nl/Erwin/Slider+Daan/stefan-bron-2.jpg"},
        { name: 'Anubha', age: 21, imageUrl:"https://static.nieuwsblad.be/Assets/Images_Upload/2012/10/07/Stefan-004-kl.jpg"},
        { name: 'amit', age: 21, imageUrl:"https://media.licdn.com/dms/image/C4E03AQGAHt1PVFJO6A/profile-displayphoto-shrink_800_800/0/1623249411702?e=2147483647&v=beta&t=PhjGA8rK15XMw5cFPTLz96KWHaYP_beHpHfqgoHj7bM"}
      ],
      validated: true,
    };
  },
  methods: {
    calculateAge() {
      const today = new Date();
      const birthDate = new Date(this.user.dob);
      const diff = today - birthDate;
      const ageDate = new Date(diff);
      this.age = Math.abs(ageDate.getUTCFullYear() - 1970);
    },
    validateAge() {
      if (this.age !== null) {
        if (this.age < 18) {
          this.showAge = false;
          this.isError = true;
        } else {
          this.showAge = true;
          this.isError = false;
        }
      } else {
        this.showAge = "Please calculate age first.";
      }
    }
  },
  mounted() {
    console.log(`The initial Age is ${this.age}.`)
  }
}
</script>
<template>
  <div class="main-container">
    <p><span>Name:</span> {{ user.name }}</p>
    <p><span>Address:</span> {{ user.address }}</p>
    <p><span>DOB:</span>{{ user.dob }}</p>
    <button  v-on:click="calculateAge">Calculate Age</button>
    <p v-show="age!=null"><span>Age:</span>{{ age }}</p>
    <button v-show="age !== null" v-on:click="validateAge">Validate Age</button>
    <p v-show="showAge === true" :class="{'validate':  validated}">'You are OK to use the website.'</p>
    <p v-show="showAge === false" :class="{'error':isError}">You are under age.</p>
    <ul>
      <li v-for="user in users" :key="user.name">
        <div class="li-item"> <span>Name: </span>  {{user.name}}</div>
        <div class="li-item"> <span>Age: </span>   {{ user.age }}</div>
        <img :src="user.imageUrl" alt="" srcset="">
      </li>
    </ul>
  </div>
</template>
<style scoped>
.main-container{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.validate{
  color:green;
}
.error{
  color:red;
}
ul{
  list-style: none;
  display: flex;
  gap:15px;
}
ul li img{
  height: 100px;
  width:100px;
  border-radius: 50px;
}
ul li{
  display: flex;
  flex-direction: column;
  align-items: center;
  gap:10px;
}
ul li .li-item
{
  display: flex;
}
span{
  font-size:1.1rem;
  font-weight: 550;
}
button{
  cursor: pointer;
}
</style>