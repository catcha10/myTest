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
            
            <table class="tableClass">
              <thead>
                <tr>
                  <th>Title</th>
                  <th>Type</th>
                  <th>Discount</th>
                  <th>Quantity</th>
                  <th>Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(promotion, index) in customer.promotions" :key="index" >
                  <td><nuxt-link to="/" title="Profile"  > {{ promotion.title }} </nuxt-link></td>
                  <td>{{ promotion.type }}</td>
                  <td><span v-if="promotion.discount" >- ${{ formatPrice(promotion.discount) }}</span></td>
                  <td>{{ promotion.quantity }}</td>
                  <td><EditIcons></EditIcons></td>
                </tr>
              </tbody>
            </table>

            <button type="button" class="btnClass addPromo" >Add new promotion</button>

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
  padding: 1.5rem 1.5rem;
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
  background-color:#f8f8f8;
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
/*
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
  font-weight: 400;
  color: #333;
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
  color: rgba(102,102,102,0.7);
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
  color: #3a77b2;
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
}*/

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

.tableClass{
  border-collapse: collapse;
  min-width:55%;
}

table th{
  font-family: helvetica;
  font-style: normal;
  font-weight: 400;
  font-size: 0.875rem;
  color:#fff;
  text-align:left;
  background-color:#3a77b2;
}
th, td{
  padding:12px 20px;
  font-family: helvetica;
  font-style: normal;
  font-weight: 300;
  font-size: 0.875rem;
}
tr td:last-child , tr th:last-child{
  text-align:center;
}
table, tr, th, td{
  border: 1px solid #f8f8f8;
}

td a{
    color: #3a77b2;
    text-decoration: none;
    font-weight: 500;
}

@media (max-width:768px){
  .container{
    width:100%;
  }
  .tableClass{
    min-width:100%;
  }
}

@media (max-width:767px){

  .custInfo{
    display:block;
    max-width:75%;
    margin-right:0px;
  }
  .custInfo:after{
    display:none;
  }
  .collapsible-content .content-inner{
    padding:0.5rem;
  }
  table{
    border:none;
  }
  table thead{
    display:none;
  }
  table tr{
    border:none;
    border-bottom: 1px solid #f8f8f8;
    padding:20px 15px;
  }
  table td{
    border:none;
    display:block;
    padding:9px 8px 9px 85px;;
  }
  table td:last-child{
    text-align:left;
  }
  table td{
    position:relative;
    min-height:18px;
  }
  table td:before{
    content:"";
    position:absolute;
    left:10px;
    top:9px;
    font-family: helvetica;
    font-style: normal;
    font-weight: 300;
    font-size: 0.875rem;
    color: #999;
  }
  table td:first-child{
    margin-top:15px;
  }
  table td:last-child{
    margin-bottom:15px;
  }
  table td:nth-child(1):before{
    content:"Title: ";
  }
  table td:nth-child(2):before{
    content:"Type: ";
  }
  table td:nth-child(3):before{
    content:"Discount: ";
  }
  table td:nth-child(4):before{
    content:"Quantity: ";
  }
  table td:nth-child(5):before{
    content:"Action: ";
  }
  .app-content h1{
    margin:10px 0;
  }
}
</style>
