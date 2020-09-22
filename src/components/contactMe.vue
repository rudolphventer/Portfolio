<template>
<div>
    <h3>{{error}}</h3>
        <p styl>Your Email Address</p>
      <div><input style="width: 80%; text-align: center" class="inputBox" v-model="contact"/></div>
      <p>Your Message</p>
      <div><textarea style="width: 80%" class="inputBox" rows="4" v-model="message"></textarea></div>
      <div><input v-model="check" style="display: none"/></div>
      <button class="myButton" v-on:click="send" style="margin-top: 1rem">
        Send
      </button>
</div>


</template>

<script>
export default {
  name: 'ContactCard',
  data() {
      return{
          message: '',
          contact: '',
          check: '',
          error: 'Contact Me'
      }
      
  },
   methods: {
    validateEmail: function (email)
       {
            var re = /\S+@\S+\.\S+/;
            return re.test(email);   
       },
    send: function () {
        //I use a hidden check field as rudimentary way to prevent bots from abusing the contact field
        if (!this.message) {
        this.error = 'A message is required.';
        return
        }
        if (!this.contact || !this.validateEmail(this.contact)) {
        this.error = 'A valid email address is required.';
        return
        }
        if(this.check == '')
        {
            this.error = 'Thanks for the message!';
            fetch(process.env.VUE_APP_TELEGRAM_API_URL + this.contact + ' sent message: ' + this.message)
            this.message = '';
            this.contact = '';
        }
      
      }
    }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped> 
.myButton {
	box-shadow:inset 0px 1px 0px 0px #ffffff;
	background-color:#ffffff;
	border-radius:2px;
	border:1px solid #dcdcdc;
	display:inline-block;
	cursor:pointer;
	color:#666666;
	font-family:Arial;
	font-size:15px;
	font-weight:bold;
	padding:6px 24px;
	text-decoration:none;
	text-shadow:0px 1px 0px #ffffff;
}
.inputBox{
    box-shadow:inset 0px 1px 0px 0px #ffffff;
	background-color:#ffffff;
	border-radius:2px;
	border:1px solid #dcdcdc;
	display:inline-block;
	color:#666666;
	padding:6px 24px;
}
.status{
    font-size: 120%;
    color: rgb(0, 122, 179);
}
</style>
