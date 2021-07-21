<template>
  <div>
    
    <div class="col col-8 align-middle mt-5 offset-2">
      <div class="card">
        <div class="card-body">
          <form @submit.prevent="submit(url)">
            <div class="form-group">
              <label for="url">Enter Url</label>
              <textarea type="url" class="form-control" v-model="url" style="height:150px" />
            </div>
            <div class="for-group" v-show="shortUrl">
              <p>
                Short URL:
                <a :href="shortUrl" class="text-primary">{{shortUrl}}</a>
              </p>
            </div>
            <div class="for-group" v-show="errorMsg">
              <p>
                Error:<span>{{errorMsg}}</span>
              </p>
            </div>
            <div class="form-group">
              <button class="btn btn-primary" type="submit">Shorten URl</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: () => {
    return {
      url: "",
      shortUrl: "",
      errorMsg: "",
    };
  },
  methods: {
    submit: async function (url) {
      try {
        const api = "http://localhost:5050/url";
        const response = await axios.post(api, {
          url,
        });
        this.shortUrl = response.data.shortUrl;
      } catch (error) {
        
        this.errorMsg = error.response.data.msg;
      }
    },
  },
};
</script>