<template>
  <div class="cardGrid">
    <a v-bind:href =user.html_url style="text-decoration: none; color: inherit;">
      <div>
        <img alt="User Avatar" class="profilePic" v-bind:src="user.avatar_url" width="300px" height="auto">
        <div class="details"> 
          <h3>{{user.name}}</h3>
          <div class="bio">{{user.bio}}</div>
          <div class="location">{{user.location}}</div>
          <div class="iconsrow">
            <svg class="lnr lnr-eye" ><use xlink:href="#lnr-eye"></use></svg>
            {{user.following}}
            <svg class="lnr lnr-user"><use xlink:href="#lnr-user"></use></svg>
            {{user.followers}}
            <svg class="lnr lnr-upload"><use xlink:href="#lnr-upload"></use></svg>
            {{eventNo}}
          </div>
        </div>
      </div>
    </a>
  </div>
    
</template>

<script>
export default {
  name: 'ProfileCard',
  data() {
    return {
      user: {},
      events: []}
    
  },
  computed: {
    eventNo () {
      return this.events.filter(v => v).length;
    }
  },
  mounted: async function () {

        //const user = await this.axios.get(process.env.VUE_APP_USER_URL);
        //this.user = user.data;
        const user = await fetch(process.env.VUE_APP_USER_URL);
        var userData = await user.json();
        this.user = userData;

        const events = await this.axios.get(process.env.VUE_APP_COMMITS_URL);
        this.events = events.data;
        

  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.iconsrow
{
  margin-top: 0.5rem;
  display: block;

}
.iconsrow > *
{
  margin: 0;
  width: 2rem;
  height: 1rem;
  padding: 0;
}


.profilePic {
	clip-path: circle(3rem at center);
	height: 6rem;
	width: auto;
	padding: 0%;
	margin: 0%;
	float: left;
	background-color: aqua;
  }
  
.cardGrid
{
  grid-template-columns: repeat(auto-fit, minmax(10rem, auto));
}
  /*for desktop*/
  @media only screen and (min-width: 768px) {
    
  } 
</style>
