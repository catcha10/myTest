<template>
  <div class="container">

    <h1>Customer List</h1>
    
    <section class="customerList"  >
      <span class="custInfo custName" >{{ customer.name }}</span>
      <span class="custInfo custEmail" >{{ customer.email }}</span>
      <div class="editCust" >
        <EditIcons></EditIcons>
      </div>
      <div class="promotionList wrap-collabsible" >
        <input :id="customer.email" class="toggle" type="checkbox"> 
        <label :for="customer.email" class="lbl-toggle">Promotions <span>({{ customer.promotions.length }})</span></label>
        <div class="collapsible-content">
          <div class="content-inner">
            <ul class="promoList" >
              <li v-for="(promotion, index) in customer.promotions" :key="index">
                <div>
                  <span class="promoTitle" ><nuxt-link to="/" title="Profile"  > {{ promotion.title }} </nuxt-link></span>
                  <span class="promoType">{{ promotion.type }}</span>
                </div>
                <div><span v-if="promotion.discount" class="promoDisc" >- ${{ formatPrice(promotion.discount) }}</span></div>
                <div><span class="promoQty" >{{ promotion.quantity }}</span></div>
                <div class="editCust" >
                  <EditIcons></EditIcons>
                </div>
              </li>
              <li><button type="button" class="btnClass addPromo" >Add new promotion</button></li>
            </ul>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>

<script>

import axios from 'axios'
import EditIcons from '~/components/editIcons'

export default {
  components: { EditIcons },
  methods: {
    formatPrice(value) {
        let val = (value).toFixed(2)
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
    }
  },
  async asyncData ({ params }) {
    const { data } = await axios.get(`https://dev.beepbeep.tech/v1/sample_customer?format=json`)
    return { customer: data }
  },
  head () {
    return {
      title: 'Customer List'
    }
  }
}
</script>

<style lang="scss" scoped >

.container {
  width: 80%;
  margin: auto;
  display: grid;
  grid-gap: 1rem;
}

input[type='checkbox'] {
  display: none;
}

.editCust{
    position:absolute;
    display:inline-block;
    top:25px;
    right:20px;
}

.lbl-toggle {
  display: block;
  font-size: 1rem;
  font-family: helvetica;
  font-style: normal;
  font-weight: 300;
  text-align: left;
  padding: 10px 6px;
  cursor: pointer;
  color: #333;
  transition: all 0.25s ease-out;
}

.lbl-toggle span{
  font-size: 0.85rem;
  font-weight: 300;
}

.lbl-toggle:hover {
  color: #333;
}

.lbl-toggle::before {
  content: ' ';
  display: inline-block;
  border-top: 5px solid transparent;
  border-bottom: 5px solid transparent;
  border-left: 5px solid #666;
  vertical-align: middle;
  margin-right: .7rem;
  transform: translateY(-2px);
  transition: transform .2s ease-out;
  margin-left:2px;
}

.collapsible-content .content-inner {
  background: rgba(185, 203, 219, .2);
  border-bottom: 1px solid rgba(185, 203, 219, .2);
  padding: .5rem 1.5rem;
}

.collapsible-content {
  max-height: 0px;
  overflow: hidden;
  transition: max-height .25s ease-in-out;
}

.toggle:checked + .lbl-toggle + .collapsible-content {
  max-height:none;
}

.toggle:checked + .lbl-toggle::before {
  transform: rotate(90deg) translateX(-3px);
}

.toggle:checked + .lbl-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.customerList{
  background-color:#eee;
  padding:20px;
  position:relative;
}

.custInfo{
  font-size:1rem;
  font-family: helvetica;
  font-style: normal;
  font-weight: 300;
  color:#333;
  padding:10px 30px 10px 28px;
  margin-right:20px;
  position:relative;
  display:inline-block;
}

.custInfo:after{
  content:"";
  position:absolute;
  right:0px;
  top:10px;
  bottom:10px;
  width:1px;
  height:auto;
  background-color:rgba(102,102,102,0.8);
}

.custInfo.custEmail:after{
  display:none;
}

.custInfo:before{
  font-family: 'FontAwesome';
  color:rgba(102,102,102,1);
  position:absolute;
  left: 6px;
  top: 10px;
  font-size:14px;
}

.custInfo.custName:before{
  content: "\f007";
  font-size:16px;
}

.custInfo.custEmail:before{
  content: "\f0e0";
  top:11px;
}

.promoList{
  margin:0px;
  padding:0px;
  list-style:none;
}

.promoList li{
  padding:8px 0;
  font-size:0.875rem;
  font-family: helvetica;
  font-style: normal;
  font-weight: 300;
  border-bottom:1px solid rgba(255,255,255,0.5);
  position:relative;
  padding-bottom:43px;
}

.promoList li:last-child{
  padding-bottom:0px;
}

.promoList li .editCust{
    bottom: 10px;
    left: -7px;
    top: auto;
    right: auto;
}

.promoList li span{
  position:relative;
  padding: 5px 30px;
  display: inline-block;
}

.promoList li span:before{
  content:"";
  position:absolute;
  left:0px;
  color: rgba(102,102,102,0.5);
}

.promoList li span{
  margin-right:25px;
}

.promoList li span.promoTitle:before{
  content:"Title";
}

.promoList li span.promoTitle{
  padding-left:40px;
}

.promoList li span.promoTitle a{
  color: #41B883;
  text-decoration:none;
  font-weight: 500;
}

.promoList li span.promoTitle a:hover,
.promoList li span.promoTitle a:hover {
  text-decoration:underline;
}

.promoList li span.promoDisc:before{
  content:"Discount";
}

.promoList li span.promoDisc{
  padding-left:68px;
}

.promoList li span.promoType:before{
  content:"Type";
}

.promoList li span.promoType{
  padding-left:40px;
}

.promoList li span.promoQty:before{
  content:"Quantity";
}

.promoList li span.promoQty{
  padding-left:65px;
}

.promoList li:last-child{
  border-bottom:none;
}

.btnClass{
  border:none;
  border-radius:4px;
  outline:none;
  padding:5px 15px 5px 34px;
  font-family: helvetica;
  font-style: normal;
  font-weight: 300;
  font-size: 0.875rem;
  background-color:#3a77b2;
  color:#fff;
  position:relative;
  margin:15px 0;
}

.btnClass:hover, .btnClass:focus{
  cursor:pointer;
}

.btnClass:before{
  font-family: 'FontAwesome';
  content: "\f067";
  color:#fff;
  position: absolute;
  left: 15px;
  top: 7px;
}

@media (max-width:768px){
  .container{
    width:100%;
  }
}

@media (max-width:767px){
  .promoList li span.promoTitle,
  .promoList li span.promoType{
    display:block;
  }

  .custInfo{
    display:block;
    max-width:75%;
    margin-right:0px;
  }

  .custInfo:after{
    display:none;
  }
}
</style>
