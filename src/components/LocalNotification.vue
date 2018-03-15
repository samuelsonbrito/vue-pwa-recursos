<template>
  <div>
      <h1>Notificações Locais</h1>
      <p>Permissão: {{permission}} <a href="" @click.prevent="request()" v-if="permission !== 'granted'">Solicitar</a></p>
      <a href="" @click.prevent="fire('Foi um click','Clicou no botão')">Notificação</a>
  </div>
</template>

<script>
export default {

    data(){
        return {
            permission: null
        }
    },
    methods:{
        request(){
            Notification.requestPermission(()=>{
                this.permission = Notification.permission
            })
        },
        fire(msg, body){
            let options = {
                body: body,
                icon: 'http://cdn1.beeffco.com/files/images/candidates/6f3c62262383666e837fea4e6c50d847.jpg'
            }
            new Notification(msg, options)
        },
        firePersistent(msg, body){
            let options = {
                body: body,
                icon: 'http://cdn1.beeffco.com/files/images/candidates/6f3c62262383666e837fea4e6c50d847.jpg'
            }
            navigator.serviceWorker.getRegistration()
                .then(req => req.showNotification(msg, options))
                .catch(e => console.log('Erro: '+e))
        }        
    },
    mounted(){
        this.permission = Notification.permission
    }
}
</script>
