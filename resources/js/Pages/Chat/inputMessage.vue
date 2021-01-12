<template>
    <div class="relative h-10 m-1">
        <div style="border-top:1px solid #e6e6e6;" class="grid grid-cols-6">
            <input
                 type="text"
                    v-model="message"
                    @keyup.enter="sendMessage()"
                    placeholder="Գրիր Հաղորդագրությունը"
                    class="col-span-5 outline-none p-1"
               />
                <button
                @click="sendMessage()"
                class=" bg-blue-700 hover:bg-green-700 p-1 m-1 rounded text-white">
                send
            </button>
        </div>


    </div>
</template>
<script>
import Input from '../../Jetstream/Input.vue'
export default {
  components: { Input },
        props:['room'],
        data:function(){
            return {
                message:''
            }
        },
        methods:{
            sendMessage(){
                if(this.message == ' '){
                    return;
                }

                axios.post('/chat/room/'+this.room.id+'/message',{
                    message:this.message
                })
                .then(response =>{
                    if(response.status == 201 ){
                        this.message = '';
                        this.$emit('messagesent');
                    }
                })
                .catch(error =>{
                    console.log(error);
                })
            }
        }
}
</script>
