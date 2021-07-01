<template>
<h1>hello</h1>
  <h1 v-on:click = 'lol()'>Click to get anectodotes </h1>
      <ol>
        <li 
        v-for="anectode in anectodes"
        :key = anectode.text >
          <p v-bind:class = '{ active: anectode.isActive }'>
          {{ anectode.text }}
          <button v-on:click ='anectode.isActive = !anectode.isActive'>like</button></p>
        </li>
      </ol>
    <button v-on:load="getAnectodts">Gettem</button>
</template>

<script>
export default {
  name: 'App',
  data (){
    return {
      anectodes: [],
    };
  },
  created: function() {
  	this.getAnectodts();
  },
  methods: {
  getAnectodts : function(){
		fetch("https://v2.jokeapi.dev/joke/Any?amount=10", {
      "headers": {
        "accept": "*/*",
        "accept-language": "ru-RU,ru;q=0.9,en-US;q=0.8,en;q=0.7",
        "cache-control": "no-cache",
        "pragma": "no-cache",
        "sec-ch-ua": "\" Not;A Brand\";v=\"99\", \"Google Chrome\";v=\"91\", \"Chromium\";v=\"91\"",
        "sec-ch-ua-mobile": "?0",
        "sec-fetch-dest": "empty",
        "sec-fetch-mode": "cors",
        "sec-fetch-site": "cross-site"
        },
        "referrer": "https://sv443.net/",
        "referrerPolicy": "strict-origin-when-cross-origin",
        "body": null,
        "method": "GET",
        "mode": "cors",
        "credentials": "omit"
			}).then((response) => {
					return response.json();
			}).then((data)=> {
					data = data.jokes;
					for(var i = 0; i < data.length; i++) {
							console.log(data[i])
						this.anectodes.push({
							text: data[i].joke ? data[i].joke : data[i].setup + '\n' + data[i].delivery ,
							id: data[i].id,
							isActive : false
						})
					}
			});
  },
  likeHandeled : function (el){
    el.isActive = !el.isActive;
  }

  }
}
</script>

<style src = './styles.css'></style>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>