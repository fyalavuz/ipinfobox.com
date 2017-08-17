<template>
  <section class="container">
    <div>
      <h1 class="title">
        ipinfo <div class="logo"></div>
      </h1>
      <h2 class="subtitle">
        {{data.ip}}
      </h2>
      <div class="links">
        <table id="locationInfo">
          <tbody>
            <tr>
              <td>Country Code:</td><td>{{data.country_code}}</td><td>Country Name:</td><td>{{data.country_name}}</td>
            </tr>
            <tr>
              <td>Region Code:</td><td>{{data.region_code}}</td><td>Region Name:</td><td>{{data.region_name}}</td>
            </tr>
            <tr>
              <td>Time Zone:</td><td>{{data.time_zone}}</td><td>Zip Code:</td><td>{{data.zip_code}}</td>
            </tr>
            <tr>
              <td>Time Zone:</td><td>{{data.metro_code}}</td>
            </tr>
          </tbody>

        </table>
      </div>
    </div>
  </section>
</template>
<script>

import Logo from '~/components/Logo.vue'
import axios from 'axios'

export default {
  ipAddress: '',
  components: {
    Logo
  },
  data: function () {
    return {
      data: {
        ipAddress: ''
      }
    }
  },
  async asyncData (context) {
    if (context.isServer) {
      context.ip = context.req.client._peername.address
    }

    let { data } = await axios.get(`http://ipinfobox.com/api/${context.ip}`)

    return {
      data: data
    }
  }
}
</script>
<style>
h1 {
  margin-top: 50px;
}

.logo {
    background: url(../assets/images/logo.png);
    width: 250px;
    height: 200px;
    position: absolute;
    right: 0;
    top: -75px;
}

.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
  position: relative;
  padding-right: 100px;
  margin-left: -100px;
}

.subtitle
{
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

table
{
  text-align: left;
  margin: 0 auto;
  width: 550px;
}

tr td:nth-child(odd) {
    font-weight: bold;
    width: 120px;
}

</style>
