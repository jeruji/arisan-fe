<template>
    <div class="feature-container">
        <div class="text-center">
            <h1>Selamat Datang Kembali, {{ nama }}</h1>
        </div> 
        <div class="margin-top-med">
            &nbsp;
        </div>
        <hr />   
        <div class="row justify-content-center mb-3">
            <div class="form-group col-md-3">
                <h5 class="d-block mb-3">Data diri anda</h5>
                <span class="feature-text d-block">{{ nama }}</span>
                <span class="feature-text d-block">{{ alamat }}</span>
                <span class="feature-text d-block mb-3">{{ email }}</span>
                <button class="d-block btn btn-primary">Update</button>
            </div>
            <div class="form-group col-md-4">
                <h5 class="d-block mb-3">Arisan aktif anda</h5>
                <div v-for="(arisan, index) in arisans" v-bind:key="index">
                    <span class="feature-text d-block mb-3">{{ arisan.arisanTitle }}</span>
                </div>
            </div>
            <div class="form-group col-md-3">
                <h5 class="d-block mb-3">Undangan arisan</h5>
                <div v-for="(invitation, index) in arisanInvitations" v-bind:key="index">
                    <span class="feature-text d-block mb-3">{{ invitation.arisanTitle }}</span>
                </div>
                 <button class="btn btn-primary" type="button" v-bind:style="[moreArisanInvitation == true ? {'display': 'inline-block'} : {'display': 'none'}]">
                    Lihat Selengkapnya
                </button>
            </div>
        </div>
        <hr />
        <div class="row justify-content-center mb-3">
            <div class="form-group col-md-3">
                <h5 class="d-block mb-3">Link cepat</h5>
                <nuxt-link to="/listing/arisan" class="d-block">Daftar arisan terbuka</nuxt-link>
                <nuxt-link to="/memberarea/buatarisan" class="d-block">Buat arisan</nuxt-link>
                <nuxt-link to="/memberarea/buatdompet" class="d-block">Buat dompet</nuxt-link>
            </div>
            <div class="form-group col-md-4">
                <h5 class="d-block mb-3">Dompet bersama aktif anda</h5>
                <div v-for="(dompet, index) in dompets" v-bind:key="index">
                    <span class="feature-text d-block mb-3">{{ dompet.dompetTitle }}</span>
                </div>
            </div>
            <div class="form-group col-md-3">
                <h5 class="d-block mb-3">Undangan dompet bersama</h5>
                <div v-for="(invitation, index) in walletInvitations" v-bind:key="index">
                    <span class="feature-text d-block mb-3">{{ invitation.dompetTitle }}</span>
                </div>
                <button class="btn btn-primary" type="button" v-bind:style="[moreDompetInvitation == true ? {'display': 'inline-block'} : {'display': 'none'}]">
                    Lihat Selengkapnya
                </button>
            </div>
        </div>
        <hr />
        <div class="row justify-content-center mb-3">
            <div class="form-group col-md-3">
                &nbsp;
            </div>
            <div class="form-group col-md-4">
                <h5 class="d-block mb-3">History arisan anda</h5>
                <div v-for="(arisanHistory, index) in arisanHistories" v-bind:key="index">
                    <span class="feature-text d-block mb-3">{{ arisanHistory.arisanTitle }}</span>
                </div>
            </div>
            <div class="form-group col-md-3">
                <h5 class="d-block mb-3">History dompet anda</h5>
                <div v-for="(dompetHistory, index) in dompetHistories" v-bind:key="index">
                    <span class="feature-text d-block mb-3">{{ dompetHistory.dompetTitle }}</span>
                </div>
            </div>
        </div>
    </div>
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
.feature-container {
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
</style>
<script>
import firebase from 'firebase'
import Swal from 'sweetalert2'
import axios from 'axios'
import { server } from '@/static/helper'
export default {
    data() {
        return {
            nama: null,
            alamat: null,
            email: null,
            arisans: [],
            arisanIds: [],
            dompets: [],
            dompetIds: [],
            userId: null,
            arisanInvitations: [],
            arisanInvitationIds: [],
            walletInvitations: [],
            arisanHistories: [],
            dompetHistories: [],
            moreArisanInvitation: false,
            moreDompetInvitation: false
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
                    if(userData[0].hasOwnProperty('fullname')){
                        self.nama = userData[0].fullname
                        self.alamat = userData[0].address
                        self.email = userData[0].email
                        self.userId = userData[0]._id
                    }

                    self.getArisanId()
                    self.getDompetId()
                    self.getArisanInvitationId()
                    self.getDompetInvitationId()
                })
            }
            else{
                self.$router.replace('/login')
            }
        })
    },
    methods: {
        getArisanId(){
            let self = this
            axios.get(server.baseURL+'/arisandetail/arisandetailbyemail/'+this.email)
                .then(data => 
                {
                    let userData = data.data

                    for(let index = 0; index<userData.length; index++){
                        self.arisanIds.push({
                            arisanId: userData[index].arisanId
                        })
                    }
                    self.getArisan()
                })
        },
        getArisan(){
            let self = this

            for(let index = 0; index<this.arisanIds.length; index++){
                axios.get(server.baseURL+'/arisan/arisan/'+self.arisanIds[index].arisanId)
                .then(data => 
                {
                    let userData = data.data
                    self.arisans.push({
                        arisanTitle: 'Arisan '+userData.pembayaran+' per '+userData.durasiPembayaran+' hari'
                    })
                })
            }
        },
        getDompetId(){
            let self = this
            axios.get(server.baseURL+'/dompetdetail/dompetdetailbyemail/'+this.email)
                .then(data => 
                {
                    let userData = data.data

                    for(let index = 0; index<userData.length; index++){
                        self.dompetIds.push({
                            dompetId: userData[index].dompetId
                        })
                    }
                    self.getDompet()
                })
        },
        getDompet(){
            let self = this

            for(let index = 0; index<this.dompetIds.length; index++){
                axios.get(server.baseURL+'/dompet/dompet/'+self.dompetIds[index].dompetId)
                .then(data => 
                {
                    let userData = data.data
                    self.dompets.push({
                        dompetTitle: 'Dompet '+userData.pembayaran+' per orang'
                    })
                })
            }
        },
        getArisanInvitationId(){
            let self = this
            axios.get(server.baseURL+'/arisandetail/arisannotconfirmed/'+this.email)
                .then(data => 
                {
                    let userData = data.data

                    for(let index = 0; index<userData.length; index++){
                        self.arisanInvitationIds.push({
                            arisanId: userData[index].arisanId
                        })
                    }
                    self.getArisanInvitation()
                })
        },
        getArisanInvitation(){
            let self = this

            for(let index = 0; index<this.arisanInvitationIds.length; index++){
                axios.get(server.baseURL+'/arisan/arisan/'+self.arisanInvitationIds[index].arisanId)
                .then(data => 
                {
                    let userData = data.data
                    self.arisanInvitations.push({
                        arisanTitle: 'Arisan '+userData.pembayaran+' per '+userData.durasiPembayaran+' hari'
                    })
                })
            }
        },
        getDompetInvitationId(){
            let self = this
            axios.get(server.baseURL+'/dompetdetail/dompetnotpaid/'+this.email)
                .then(data => 
                {
                    let userData = data.data

                    for(let index = 0; index<userData.length; index++){
                        self.dompetInvitationIds.push({
                            dompetId: userData[index].dompetId
                        })
                    }
                    self.getDompetInvitation()
                })
        },
        getDompetInvitation(){
            let self = this

            for(let index = 0; index<this.dompetInvitationIds.length; index++){
                axios.get(server.baseURL+'/dompet/dompet/'+self.dompetInvitationIds[index].dompetId)
                .then(data => 
                {
                    let userData = data.data
                    self.dompetInvitations.push({
                        dompetTitle: 'Dompet '+userData.pembayaran+' per orang'
                    })
                })
            }
        },
        getDompetHistoryId(){
            
        }
    }
}
</script>