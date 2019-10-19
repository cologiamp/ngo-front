<template>
  <div class="hello">
   <h1>{{ name }}</h1> 
   <div class="row">

    <div class="column" style="background-color:#aaa;">
      <h2>Make a new Donation</h2>
      <select v-model="selected">
        <option v-for="item in ngos" :value="item" :key="item.id">
          {{ item.name }}
        </option>
      </select>
      <p>
        Selected NGO: {{ selected.name }}, Id: {{ selected.id }}
      </p>
      <input type="number" v-model="input.amount" placeholder="Amount to donate" />
      <button v-on:click="sendData()">Send</button>
    </div>
      
    <div class="column" style="background-color:#bbb;">
        <h2>Previous Donated</h2>

        <ul id="example-1">
          <li v-for="item in donations" :key="item.id">
            {{ item.name }}
            <br>
            Amount Donated: {{ item.amount }}
            <br>
            Date: {{ item.created }}
          </li>
        </ul>

        <textarea  v-model="response"></textarea>
    </div>
    
    </div>
        
    </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'NGOs',
  data () {
      return {
          name: 'Make a donation to our NGOs',
          input: {
              ngoId: "",
              amount: ""
          },
          response: "",
          ngos: [],
          donations: [],
          selected: ""
      }
  },
  mounted() {
    //this.ngos = this.getNGOs();
    this.getNGOs();
    //this.getDonations();
    this.getDonations2();
    /*
    axios({ method: "GET", "url": "http://ngodonate.com/api5/action/get/ngos" }).then(result => {
          this.setNgos(result.data.origin);
      }, error => {
          console.error(error);
    });
    */
  },
  methods: {
    getNGOs(){
      fetch('http://ngodonate.com/api5/action/get/ngos')
        .then(response => response.json())
        .then(data => this.ngos = data);
    },
    getDonations2(){
      fetch('http://ngodonate.com/api5/action/get/donations')
        .then(response => response.json())
        .then(data => this.donations = data);
    },
    getDonations(){
      axios({ method: "GET", "url": "http://ngodonate.com/api5/action/get/donations" }).then(result => {
          this.donations = result.data.origin;
      }, error => {
          console.error(error);
      });
    },
    //GET NGOs Names
    /*
    getNGOs() {
      axios({ method: "GET", "url": "http://ngodonate.com/api5/action/get/ngos" }).then(result => {
          this.ngos = result.data.origin;
      }, error => {
          console.error(error);
      });
    },
    */
    //POST DONATION
    sendData() {
      var data = new FormData();
      data.append('ngoId', this.selected.id);
      data.append('amount', this.input.amount);
        axios({ 
          method: "POST",
          "url": "http://ngodonate.com/api5/action/post/donation", 
          "data": data, 
          "headers": { 
            "Content-Type": "application/json" }
          }).then(result => {
            this.response = result.data;
        }, error => {
            console.error(error);
        });
    }


  }


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 20px 20px;
}
a {
  color: #42b983;
}

/* My 2 columns design */
* {
  box-sizing: border-box;
}
/* Create two equal columns that floats next to each other */
.column {
  float: left;
  width: 50%;
  padding: 10px;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
</style>
