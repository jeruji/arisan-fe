<template>
    <form class="form-container">
        <div class="text-center">
            <h1>Buat Dompet Bersama</h1>
        </div>
        <div class="margin-top-med">
            &nbsp;
        </div>
        <div class="row justify-content-center">
            <div class="form-group col-md-10 text-center">
                <span class="">Rekening tujuan dana akan ditransfer</span>
            </div>
        </div>
        <div :class="displayUbahRekening" class="justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="pemilik-rekening">Nama pemilik rekening</label>
                    <input
                        type="text"
                        v-model="pemilikRekening"
                        name="pemilik-rekening"
                        class="form-control"
                        required=""
                        autofocus=""
                    >
                <span v-bind:style="[pemilikRekeningCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi nama pemilik rekening dengan benar</span>    
            </div>
            <div class="form-group col-md-5">
                <label class="grey-text" for="nama-bank">Nama Bank</label>
                    <input
                        type="text"
                        v-model="namaBank"
                        name="nama-bank"
                        class="form-control"
                        required=""
                        autofocus=""
                    >
                <span v-bind:style="[namaBankCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi nama bank dengan benar</span>
            </div>
        </div>
        <div :class="displayUbahRekening" class="justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="nomor-rekening">Nomor Rekening</label>
                    <input
                        type="text"
                        v-model="nomorRekening"
                        name="nomor-rekening"
                        class="form-control"
                        required=""
                        autofocus=""
                    >
                <span v-bind:style="[nomorRekeningCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi nomor rekening dengan benar</span>    
            </div>
            <div class="form-group col-md-5">
                <label class="grey-text" for="kantor-cabang">Kantor Cabang</label>
                    <input
                        type="text"
                        v-model="kantorCabang"
                        name="kantor-cabang"
                        class="form-control"
                        required=""
                        autofocus=""
                    >
                <span v-bind:style="[kantorCabangCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi nama kantor cabang dengan benar</span>
            </div>
        </div>
        <div :class="displayImgRekening" class="justify-content-center">
            <div class="form-group col-md-10">
                <img :src="imgRekeningLoc" class="img-fluid" />
            </div>
        </div>
        <div :class="displayImgRekening" class="justify-content-center">
            <div class="form-group col-md-5">
                <a @click.prevent="ubahRekening" href="#">Ubah rekening tujuan</a>
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div>
        </div>
        <div :class="displayUbahRekening" class="justify-content-center">
            <div class="form-group col-md-5">
                <a @click.prevent="imgRekening" href="#">Batal</a>
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div>
        </div>
        <hr>
        <div class="row justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="setoran">Besar setoran per orang (hanya angka, dalam rupiah)</label>
                    <input
                        type="text"
                        v-model="setoran"
                        name="setoran"
                        class="form-control"
                        required=""
                        autofocus=""
                    >
                <span v-bind:style="[setoranCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi besar pembayaran dengan benar</span>    
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div>
        </div>
        <hr>
        <div class="row justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="deskripsi">Deskripsi (mis: dompet bersama gathering kantor)</label>
                    <input
                        type="text"
                        v-model="description"
                        name="deskripsi"
                        class="form-control"
                        required=""
                        autofocus=""
                    >
                <span v-bind:style="[descriptionCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi deskripsi dengan benar</span>    
            </div>
            <div class="form-group col-md-5">
                &nbsp;
            </div>
        </div>
        <hr>
        <div class="row justify-content-center">
            <div class="form-group col-md-5">
                <label class="grey-text" for="peserta">Jumlah peserta dompet bersama (hanya angka)</label>
                    <input
                        type="text"
                        v-model="peserta"
                        name="peserta"
                        class="form-control w-50 d-inline-block"
                        required=""
                        autofocus=""
                    >
                <button @click.prevent="addFormInvite" class="btn btn-primary ml-5" type="button">
                    <i class="fas fa-user-plus" /> apply
                </button>    
                <span v-bind:style="[pesertaCondition == true ? {'display': 'block'} : {'display': 'none'}]" class="warning-text">*) Mohon isi jumlah peserta dengan benar</span>
            </div>
            <div class="form-group col-md-5">
                <div>&nbsp;</div>
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
<script>
import Swal from 'sweetalert2'
import axios from 'axios'
import { server } from '@/static/helper'
import firebase from 'firebase'
export default {
    data(){
        return{
            isValidated: true,
            invites:[],
            peserta: null,
            setoran: "",
            description: "",
            displaySubmit: 'd-none',
            displayUbahRekening: 'd-none',
            setoranCondition: false,
            pesertaCondition: false,
            descriptionCondition: false,
            displayImgRekening: 'row',
            pemilikRekening: null,
            namaBank: null,
            nomorRekening: null,
            kantorCabang: null,
            imgRekeningLoc: null,
            pemilikRekeningCondition: false,
            namaBankCondition: false,
            nomorRekeningCondition: false,
            kantorCabangCondition: false,
            creator: []
        }
    },
    created(){
        let self = this
        firebase.auth().onAuthStateChanged(function (user) {
            
            if(user!=null){
                self.authenticatedUser = user
                axios.get(server.baseURL+'/customer/customerByFirebaseId/'+user.uid)
                .then(data => 
                {
                    let userData = data.data
                    self.imgRekeningLoc = server.baseURL+'/customer/customerImage/'+userData[0].bukuRekeningFile
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
                self.$router.push({name: 'login'})
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
            else{
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
        ubahRekening(){
            this.displayImgRekening = 'd-none'
            this.displayUbahRekening = 'row'
        },
        imgRekening(){
            this.displayImgRekening = 'row'
            this.displayUbahRekening = 'd-none'
        },
        formValidation(){
            this.isValidated = true
            
            if(this.displayUbahRekening=='row'){
                if(/^[a-zA-Z]+(([',. -][a-zA-Z ])?[a-zA-Z]*)*$/.test(this.pemilikRekening) == false){
                    this.pemilikRekeningCondition = true
                    this.isValidated = false
                }

                if(/^[a-zA-Z]+(([',. -][a-zA-Z ])?[a-zA-Z]*)*$/.test(this.namaBank) == false){
                    this.namaBankCondition = true
                    this.isValidated = false
                }

                if(/^[0-9]+$/.test(this.nomorRekening) == false){
                    this.nomorRekeningCondition = true
                    this.isValidated = false
                }

                if(/^[a-zA-Z0-9\s,.'-]{3,}$/.test(this.kantorCabang) == false){
                    this.kantorCabangCondition = true
                    this.isValidated = false
                }
            }
            else{
                if(/^[0-9]+$/.test(this.setoran) == false){
                    this.setoranCondition = true
                    this.isValidated = false
                }

                if(this.description.length < 6 || /([^\s])/.test(this.description)==false){
                    console.log('masuk')
                    this.descriptionCondition = true
                    this.isValidated = false
                }
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
                let dompetData = []
                let dompetDetailData = []

                for(let index = 0; index<this.invites.length; index++){

                    if(index==0){
                        dompetDetailData.push({
                            fullname: this.invites[index].nameField,
                            email: this.invites[index].emailField,
                            phone: this.invites[index].phoneField,
                            isCreator: true
                        })
                    }
                    else{
                        dompetDetailData.push({
                            fullname: this.invites[index].nameField,
                            email: this.invites[index].emailField,
                            phone: this.invites[index].phoneField,
                            isCreator: false
                        })
                    } 
                }

                if(this.pemilikRekening!=null&&this.namaBank!=null&&this.nomorRekening!=null&&this.kantorCabang!==null)
                {
                    dompetData = {
                        pemilikRekening: this.pemilikRekening,
                        namaBank: this.namaBank,
                        nomorRekening: this.nomorRekening,
                        kantorCabang: this.kantorCabang,
                        pembayaran: this.setoran,
                        isFinish: false,
                        dompetMember: dompetDetailData
                    }
                }
                else if(this.displayImgRekening == 'row'){
                    dompetData = {
                        imgRekeningLocation: this.imgRekeningLoc,
                        pembayaran: this.setoran,
                        isFinish: false,
                        dompetMember: dompetDetailData
                    }
                }
                this.submitForm(dompetData)
            }
        },
        submitForm(dompetData){
            axios.post(server.baseURL+'/dompet/create', dompetData)
            .then(data => {
                let dompetData = data.data
                this.dompetId = dompetData.dompet._id
                Swal.fire({
                    icon: 'info',
                    title: 'Buat Dompet Sukses',
                    text: 'Link undangan telah dikirim ke email rekan anda ' +
                                        'Silahkan informasikan.'
                })
            })
        },
        submitDompetMember(){
            for(let index = 0; index<this.invites.length; index++){
                let dompetDetailData 

                if(index==0){
                    dompetDetailData = {
                        dompetId: this.dompetId,
                        fullname: this.invites[index].nameField,
                        email: this.invites[index].emailField,
                        phone: this.invites[index].phoneField,
                        isCreator: true
                    }
                }
                else{
                    dompetDetailData = {
                        dompetId: this.dompetId,
                        fullname: this.invites[index].nameField,
                        email: this.invites[index].emailField,
                        phone: this.invites[index].phoneField,
                        isCreator: false
                    }
                } 

                axios.post(server.baseURL+'/dompetdetail/create',dompetDetailData)
                .then(data => 
                {
                    console.log(data.data)
                })
            }
        }
    }
}
</script>
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
.margin-top-sm {
    margin-top: 20px;
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