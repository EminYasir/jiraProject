<template>
  <div>
    <form @submit.prevent="updateTask">
        <div class="title">
          <label>Başlık</label>
          <input type="text" v-model="title" required>
        </div>
        <div class="detail">
          <label>İş Detayı</label>
          <textarea type="text" v-model="detail" required />
        </div>
        <button type="submit">Güncelle</button>
      </form>
  </div>
</template>

<script>
export default {
    name: 'EditTaskView',
    props: ['id'],
    data() {
        return {
            title: "",
            detail: "",
            completed: false,
            url: `http://localhost:3000/tasks`
        }
    },
    methods: {
        updateTask(){
            fetch(`${this.url}/${this.id}`,{
                method:'PUT',
                headers:{
                    'Content-Type':'application/json',
                },
                body:JSON.stringify({
                    title:this.title,
                    details:this.detail,
                    completed:this.completed
                })
            }).then(() => {
                this.$router.push('/')
            }).catch(err => console.log(err))
        }
    },
    mounted(){
        fetch(`${this.url}/${this.id}`)
        .then(res => res.json())
        .then(data => {
            this.title = data.title;
            this.detail = data.details;
            this.completed = data.completed;
        })
        .catch(err => console.log(err))
    },
    
}
</script>

<style scoped>
form {
  max-width: 600px;
  width: 100%;
  box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 20px;
  background: white;
}

input {
  width: 100%;
  border: none;
  border-bottom: 1px solid gray;
  outline: none;
}

textarea {
  width: 100%;
  border: 1px solid gray;
  outline: none;
  border-radius: 15px;
  height: 100px;
  padding: 10px;
}

label {
  margin: 20px 0 10px 0;
  display: block;
  color: gray;
  font-size: 15px;
  font-weight: 500px;
  letter-spacing: 1px;
  text-transform: uppercase;
}

button {
  padding: 10px 30px;
  border-radius: 15px;
  font-size: 18px;
  background: green;
  color: white;
  border: none;
  cursor: pointer;
  margin: 20px auto;
  display: block;
}
</style>