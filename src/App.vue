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
      showAge: false,
      isError: null,
      isValid:false,
      users: [
        { userName: 'Rahul', age: 24, imageUrl: "https://mir-s3-cdn-cf.behance.net/project_modules/max_1200/35af6a41332353.57a1ce913e889.jpg" },
        { userName: 'Rohit', age: 20, imageUrl: "https://s3-eu-west-1.amazonaws.com/files2.fd.nl/Erwin/Slider+Daan/stefan-bron-2.jpg" },
        { userName: 'Anubha', age: 21, imageUrl: "https://static.nieuwsblad.be/Assets/Images_Upload/2012/10/07/Stefan-004-kl.jpg" },
        { userName: 'amit', age: 21, imageUrl: "https://media.licdn.com/dms/image/C4E03AQGAHt1PVFJO6A/profile-displayphoto-shrink_800_800/0/1623249411702?e=2147483647&v=beta&t=PhjGA8rK15XMw5cFPTLz96KWHaYP_beHpHfqgoHj7bM" }
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
      this.showAge=null;
    },
    validateAge() {
      this.showAge = true;
      if (this.age !== null) {
        if (this.age < 18) {
          this.isValid = false;
          this.isError = true;
        } else {
          this.isValid= true;
          this.isError = false;
        }
      } else {
        this.showAge = "Please calculate age first.";
      }
    }
  }
}
</script>
<template>
  <div class="main-container">
    <p class="user-data"><span>Name:</span> {{ user.name }}</p>
    <p class="user-data"><span>Address:</span> {{ user.address }}</p>
    <p class="user-data"><span>DOB:</span>{{ user.dob }}</p>
    <button @click="calculateAge">Calculate Age</button>
      <div v-show="age">
        <p><span class="title">Age:</span>{{age}}</p>
        <button @click="validateAge">Validate Age</button>
      </div>
      <div v-show="showAge">
        <p v-if="isValid" class="validate">You Are Ok</p>
        <p v-else :class="{'error':isError}">You Are Underage</p>
      </div>
    <ul>
      <li v-for="user in users" :key="user.name">
        <div class="li-item"> <span>Name: </span> {{ user.userName }}</div>
        <div class="li-item"> <span>Age: </span> {{ user.age }}</div>
        <img :src="user.imageUrl" alt="userName" srcset="">
      </li>
    </ul>
  </div>
</template>
<style scoped>
.main-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.validate {
  color: green;
}

.error {
  color: red;
}

ul {
  list-style: none;
  display: flex;
  gap: 15px;
  margin-top:25px;
}

ul li img {
  height: 100px;
  width: 100px;
  border-radius: 50px;
}

ul li {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

ul li .li-item {
  display: flex;
  gap:10px;
}

span {
  font-size: 1.1rem;
  font-weight: 550;
}

button {
  cursor: pointer;
}
.user-data{
  display: flex;
  gap:10px;
}
</style>