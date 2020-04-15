<template>
    <form class="form-container">
        <div class="text-center">
            <h1>Buat Arisan</h1>
        </div>
        <div class="margin-top-med">
            &nbsp;
        </div>
        <div class="row justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="durasi-penarikan">Durasi Penarikan (dalam hari, minimal 7 hari)</label>
                <input
                type="number"
                v-model="durasiPenarikan"
                name="durasi-penarikan"
                min="7"
                max="365"
                class="form-control"
                required=""
                autofocus=""
                >
                <span v-bind:style="[penarikanCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi durasi penarikan dengan benar</span>
            </div>

            <div class="form-group col-md-5">
                <label class="grey-text" for="durasi-pembayaran">Durasi Pembayaran (dalam hari, minimal 7 hari)</label>
                <input
                type="number"
                v-model="durasiPembayaran"
                name="durasi-pembayaran"
                min="7"
                max="365"
                class="form-control"
                required=""
                autofocus=""
                >
                <span v-bind:style="[pembayaranCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi durasi pembayaran dengan benar</span>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="besar-pembayaran">Besar Pembayaran Per Durasi (angka dan dalam rupiah)</label>
                <input
                type="number"
                v-model="besarPembayaran"
                name="besar-pembayaran"
                class="form-control"
                required=""
                autofocus=""
                >
                <span v-bind:style="[jlhPembayaranCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi besar pembayaran dengan benar</span>
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div>  
        </div>
        <div class="row justify-content-center">
            <div class="form-group col-md-5">
                    <label class="grey-text" for="peserta">Jumlah peserta arisan (hanya angka, minimal 2)</label>
                        <input
                            type="text"
                            v-model="peserta"
                            name="peserta"
                            class="form-control w-50 d-inline-block"
                            required=""
                            autofocus=""
                        > 
                          
                    <button @click.prevent="addFormInvite" class="btn btn-primary ml-5" type="button" name="applyBtn">
                        <i class="fas fa-user-plus" /> apply
                    </button>
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div> 
        </div>
        
        <div v-for="(invite, index) in invites" v-bind:key="index"> 
        <hr>
            <div class="row justify-content-center">
                <div class="form-group col-md-5">
                    <label class="grey-text" :for="invite.nameFieldLabel">Nama</label>
                    <input
                        type="text"
                        v-model="invite.nameField"
                        :name="invite.nameFieldLabel"
                        class="form-control"
                        required=""
                        autofocus=""
                        :readonly="index==0"
                    >
                    <span v-bind:style="[invite.nameCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi nama dengan benar</span>
                </div>
                <div class="form-group col-md-5">
                    <label class="grey-text" :for="invite.emailFieldLabel">Email</label>
                    <input
                        type="email"
                        v-model="invite.emailField"
                        :name="invite.emailfieldLabel"
                        class="form-control"
                        required=""
                        autofocus=""
                        :readonly="index==0"
                    >
                    <span v-bind:style="[invite.emailCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi email dengan benar</span>
                </div>
            </div>
            <div class="row justify-content-center">
                <div class="form-group col-md-5">
                    <label class="grey-text" :for="invite.phoneFieldLabel">Nomor HP</label>
                    <input
                        type="text"
                        v-model="invite.phoneField"
                        :name="invite.phoneFieldLabel"
                        class="form-control"
                        required=""
                        autofocus=""
                        :readonly="index==0"
                    >
                    <span v-bind:style="[invite.phoneCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi nomor HP dengan benar</span>
                </div>
                <div class="form-group col-md-5">
                    <div>&nbsp;</div>
                    <button @click.prevent="deleteFormInvite(index)" class="btn btn-danger" type="button">
                        <i class="fas fa-trash" /> Hapus
                    </button>
                </div>
            </div>
        </div>
        <hr>
        <div :class="displaySubmit" class="justify-content-center">
            <div class="form-group col-md-5">
                <button @click.prevent="formValidation()" class="btn btn-primary" type="button">
                    <i class="fas fa-paper-plane" /> Submit
                </button>
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div>
        </div>
    </form>
</template>
<style scoped>
@import url('https://fonts.googleapis.com/css?family=Trocchi&display=swap');
h1 {
    color: #7c795d;
    font-family: 'Trocchi', serif;
    font-size: 30px;
    font-weight: normal;
    line-height: 48px;
    margin: 0;
}
.form-container {
    background-color: #f3f3f3;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    -webkit-transition: all 0.3s cubic-bezier(.25,.8,.25,1);
    transition: all 0.3s cubic-bezier(.25,.8,.25,1);
    width: 80%;
    margin-left: auto;
    margin-right: auto;
    margin-top: 50px;
    margin-bottom: 50px;
}
.margin-top-med {
    margin-top: 40px;
}
.warning-text{
    color: red;
    font-size: 12px;
    margin-top: 5px;
    margin-bottom: 5px;
}
@media screen and (max-width: 786px) {
    h1{
        font-size: 20px;
        line-height: 30px;
    }
    .form-container {
        width: 90%;
        padding: 20px;
    }
    .margin-bottom-med {
        margin-bottom: 0;
    }
}
</style>
<script>
import Swal from 'sweetalert2'
import axios from 'axios'
import { server } from '@/static/helper'
import firebase from 'firebase'
export default {
    data() {
        return {
            durasiPenarikan: 7,
            durasiPembayaran: 7,
            besarPembayaran: null,
            penarikanCondition: false,
            pembayaranCondition: false,
            jlhPembayaranCondition: false,
            displaySubmit: 'd-none',
            isValidated: true,
            invites: [],
            peserta: null,
            arisanId: null,
            authenticatedUser: null,
            creator: []
        }
    },
    created() {
        let self = this
        firebase.auth().onAuthStateChanged(function (user) {
            
            if(user!=null){
                self.authenticatedUser = user
                axios.get(server.baseURL+'/customer/customerByFirebaseId/'+user.uid)
                .then(data => 
                {
                    let userData = data.data
                    if(userData[0].hasOwnProperty('fullname')){
                        self.creator.push({
                            fullname: userData[0].fullname,
                            phone: userData[0].phone,
                            email: userData[0].email 
                        })
                    }
                })
            }
            else{
                self.$router.push('/login')
            }
        })    
    },
    watch: {
        invites() {
            if(this.invites.length>=1){
                this.displaySubmit = 'row'
            }
            else{
                this.displaySubmit = 'd-none'
            }
        }
    },
    methods: {
        addFormInvite(){

            if(this.peserta<2){
                Swal.fire({
                    icon: 'info',
                    title: 'Tambah lagi peserta',
                    text: 'Peserta minimal 2 (dua) ' +
                                        'Silahkan tambahkan.'
                })
            }
            else {
                this.invites = []
                let index = 0

                while(index<this.peserta){
                    if(index == 0){
                        this.invites.push({
                            nameFieldLabel: 'nama',
                            nameField: this.creator[0].fullname,
                            nameCondition: false,
                            emailFieldLabel: 'email',
                            emailField: this.creator[0].email,
                            emailCondition: false,
                            phoneFieldLabel: 'phoneNumber',
                            phoneField: this.creator[0].phone,
                            phoneCondition: false
                        })
                    }
                    else{
                        this.invites.push({
                            nameFieldLabel: 'nama',
                            nameField: '',
                            nameCondition: false,
                            emailFieldLabel: 'email',
                            emailField: '',
                            emailCondition: false,
                            phoneFieldLabel: 'phoneNumber',
                            phoneField: '',
                            phoneCondition: false
                        })
                    }
                    index++
                }
            }  
        },
        deleteFormInvite(index){
            this.invites.splice(index, 1)
        },
        formValidation(){
            this.isValidated = true

            if(/^[0-9]+$/.test(this.durasiPenarikan) == false || this.durasiPenarikan < 7){
                this.penarikanCondition = true
                this.isValidated = false
            }

            if(/^[0-9]+$/.test(this.durasiPembayaran) == false || this.durasiPenarikan < 7){
                this.pembayaranCondition = true
                this.isValidated = false
            }

            if(/^[0-9]+$/.test(this.besarPembayaran) == false){
                this.jlhPembayaranCondition = true
                this.isValidated = false
            }

            for(let index = 0; index<this.invites.length; index++){
                if(/^[a-zA-Z]+(([',. -][a-zA-Z ])?[a-zA-Z]*)*$/.test(this.invites[index].nameField) == false){
                    this.invites[index].nameCondition = true
                    this.isValidated = false
                }
                else{
                    this.invites[index].nameCondition = false
                }

                if(/^\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/.test(this.invites[index].emailField) == false){
                    this.invites[index].emailCondition = true
                    this.isValidated = false
                }
                else{
                    this.invites[index].emailCondition = false
                }

                if(/^(^\+62\s?|^0)(\d{3,4}-?){2}\d{3,4}$/.test(this.invites[index].phoneField) == false){
                    this.invites[index].phoneCondition = true
                    this.isValidated = false
                }
                else{
                    this.invites[index].phoneCondition = false
                }
            }

            if(this.isValidated){
                const arisanData = {
                    durasiPenarikan: this.durasiPenarikan,
                    durasiPembayaran: this.durasiPembayaran,
                    pembayaran: this.besarPembayaran,
                }
                this.submitForm(arisanData)
            }
        },
        submitForm(arisanData){
            axios.post(server.baseURL+'/arisan/create', arisanData)
            .then(data => {
                let arisanData = data.data
                this.arisanId = arisanData.arisan._id
                this.submitArisanMember()
                Swal.fire({
                    icon: 'info',
                    title: 'Buat Arisan Sukses',
                    text: 'Link undangan telah dikirim ke email rekan anda ' +
                                        'Silahkan informasikan.'
                })
            })
        },
        submitArisanMember(){
            for(let index = 0; index<this.invites.length; index++){
                const arisanDetailData = {
                    arisanId: this.arisanId,
                    fullname: this.invites[index].nameField,
                    email: this.invites[index].emailField,
                    phone: this.invites[index].phoneField,
                    isCreator: index == 0 ? true : false,
                    isAccepted: index == 0 ? true : false 
                }

                axios.post(server.baseURL+'/arisandetail/create',arisanDetailData)
                .then(data => 
                {
                    console.log(data.data)
                })
            }
        }
    }
}
</script>