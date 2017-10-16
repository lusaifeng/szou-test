<template>
  <div id="app">
    <div class="news-list">
      <list :news="news" @edit="editNews"></list>
    </div>
    <div class="btn">
      <button class="new-btn" @click="addNews()">+ Add New</button>
    </div>

    <div class="popup-layer" v-show="isShowPopup == true">
      <div class="popup">
        <h2>{{currentNews.id ? 'Edit' : 'Add'}} Article</h2>
        <form @submit.prevent="submit">
          <div class="block">
            <p>Image</p>
            <input type="text" v-model="currentNews.img" >
          </div>
          <div class="block">
            <p>Title</p>
            <input type="text" v-model="currentNews.title" >
          </div>
          <div class="block">
            <p>Content</p>
            <textarea rows="5" v-model="currentNews.content" ></textarea>
          </div>
          <div class="block text-right">
            <button type="submit" class="save-btn" @click="isShowPopup = false">Save</button>
            <button type="submit" class="cancel-btn" @click="isShowPopup = false">Cancel</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import list from './components/List'
import Vue from 'vue'

export default {
  name: 'app',
  components: {
    list
  },
  data () {
    return {
      currentEditIndex: null,
      currentNews: {
        img: null,
        title: null,
        content: null
      },
      news: [
        {
          id: 1,
          img: '../../static/images/img01.png',
          title: 'Article title goes here to introduce the content',
          content: 'Fusce venenatis orci metus,sed vulputate tellus ornare ut. Nullam vestibulum mauris sapien,vel pulvinar orci pulvinar orci pulvinar quis.Fusce venenatis orci metus,sed vulputate tellus ornare ut. Nullam vestibulum mauris sapien,vel.'
        },
        {
          id:2,
          img: '../../static/images/img01.png',
          title: 'title title 11111',
          content: 'Fusce venenatis orci metus,sed vulputate tellus ornare ut. Nullam vestibulum mauris sapien,vel pulvinar orci pulvinar orci pulvinar quis.Fusce venenatis orci metus,sed vulputate tellus ornare ut. Nullam vestibulum mauris sapien,vel.'
        }
      ],
      isShowPopup: false 
    }
  },
  methods: {
    addNews(){
      this.currentNews = {
        img: null,
        title: null,
        content: null
      }
      this.isShowPopup = true
    },
    editNews(index){
      let data = {}
      Object.assign(data, this.news[index])
      this.currentNews = data
      this.isShowPopup = true
      this.currentEditIndex = index
    },
    submit(){
      if (this.currentNews.id) {
        Vue.set(this.news, this.currentEditIndex, Object.assign({}, this.currentNews))
      } else {
        this.news.unshift(Object.assign({
          id: new Date(),
        }, this.currentNews))
      }
    }
  },
}
</script>

<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 45px;
}
.news-list {
  width: 400px;
  float: left;
}
.new-btn {
  float: left;
  background: #5fb485;
  color: #fff;
  padding: 5px 20px;
  border-radius: 2px;
  border: none;
  font-size: 14px;
  margin-left: 30px;
}
.popup-layer {
  background: rgba(0, 0, 0, .3);
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.popup-layer .popup {
  width: 350px;
  padding: 15px;
  background: #fff;
  border-radius: 2px; 
}
.popup-layer .popup h2 {
  font-size: 18px;
}
.popup-layer .popup p {
  padding: 0;
  margin: 0;
}
.popup-layer .popup .block {
  margin-bottom: 10px;
}
.popup-layer .popup .block input,
.popup-layer .popup .block textarea {
  width: 90%;
  margin-top: 5px;
  line-height: 2rem;
  border-radius: 2px;
  border: 1px #dadada solid;
  padding: 0 10px;
}
.popup-layer .popup .block textarea {
  line-height: 18px;
}
.text-right {
  text-align: right;
}
.popup-layer .popup .block .save-btn {
  background: #328557;
  color: #fff;
  padding: 5px 10px;
  border-radius: 2px;
  font-size: 14px;
  border: none;
}
.popup-layer .popup .block .cancel-btn {
  padding: 5px 10px;
  font-size: 14px;
  border: none;
  background: none;
  color: #777;
}
</style>
