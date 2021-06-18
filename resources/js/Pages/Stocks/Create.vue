<template>
  <div>
    <Layout>
      <div class="flex justify-center w-full">
        <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
          <h2 class="text-lg">Stock Form</h2>
          <form id="stock-form" name="stock-form" v-on:submit.prevent="submit">
            <div class="flex flex-col pt-6">
              <label for="id">ID</label>
              <input type="text" id="id" name="id" v-model="form.id" autocomplete="off"/>
              <div class="text-red-700 text-sm">{{errors.id}}</div>
              {{form.id}}
            </div>
            <div class="flex flex-col pt-6">
              <label for="description">Description</label>
              <input type="text" id="description" name="description" v-model="form.description" autocomplete="off"/>
              <div class="text-red-700 text-sm">{{errors.description}}</div>
            </div>
            <div class="flex flex-col pt-6">
              <label for="stock_category_id">Stock Category ID</label>
              <select name="stock_category_id" id="stock_category_id" v-model="form.stock_category_id">
                  <option value="10275">10275</option>
                  <option value="11504">11504</option>
                  <option value="1182">1182</option>
                  <option value="12574">12574</option>
                  <option value="21981">21981</option>
                  <option value="22125">22125</option>
                  <option value="2418">2418</option>
                  <option value="30512">30512</option>
                  <option value="31722">31722</option>
                  <option value="32222">32222</option>
                  <option value="32745">32745</option>
                  <option value="33746">33746</option>
                  <option value="34320">34320</option>
                  <option value="35562">35562</option>
                  <option value="37354">37354</option>
                  <option value="37484">37484</option>
                  <option value="41204">41204</option>
                  <option value="42399">42399</option>
                  <option value="64072">64072</option>
                  <option value="8976">8976</option>
              </select>
              <div class="text-red-700 text-sm">{{errors.stock_category_id}}</div>
            </div>
            <div class="flex flex-col pt-6">
              <label for="uom">UOM</label>
              <select name="uom" id="uom" v-model="form.uom">
                  <option value="BAG">BAG</option>
                  <option value="BKT">BKT</option>
                  <option value="BND">BND</option>
                  <option value="BOWL">BOWL</option>
                  <option value="BX">BX</option>
                  <option value="CM">CM</option>
                  <option value="CRD">CRD</option>
                  <option value="CS">CS</option>
                  <option value="CTN">CTN</option>
                  <option value="DZ">DZ</option>
                  <option value="EA">EA</option>
                  <option value="FT">FT</option>
                  <option value="GAL">GAL</option>
                  <option value="GROSS">GROSS</option>
                  <option value="IN">IN</option>
                  <option value="KIT">KIT</option>
                  <option value="LOT">LOT</option>
                  <option value="M">M</option>
                  <option value="MM">MM</option>
                  <option value="PC">PC</option>
                  <option value="PK100">PK100</option>
                  <option value="PK50">PK50</option>
                  <option value="PR">PR</option>
                  <option value="RACK">RACK</option>
                  <option value="RL">RL</option>
                  <option value="SET">SET</option>
                  <option value="SET3">SET3</option>
                  <option value="SET4">SET4</option>
                  <option value="SGL">SGL</option>
                  <option value="SHT">SHT</option>
                  <option value="SQFT">SQFT</option>
                  <option value="TUBE">TUBE</option>
                  <option value="YD">YD</option>
              </select>
              <div class="text-red-700 text-sm">{{errors.uom}}</div>
            </div>
            <div class="flex flex-col pt-6">
              <label for="barcode">Barcode</label>
              <input type="text" id="barcode" name="barcode" v-model="form.barcode"/>
              <div class="text-red-700 text-sm">{{errors.barcode}}</div>
            </div>
            <div class="flex flex-col pt-6">
              <label for="discontinued">Discontinued  
              <input type="checkbox" id="yes" true-value="Y" false-value="N" v-model="form.discontinued"/> Yes
              <input type="checkbox" id="no" true-value="N" false-value="Y" v-model="form.discontinued"/> No
              </label>
              <div class="text-red-700 text-sm">{{errors.discontinued}}</div>
            </div>

            <div class="flex flex-col pt-6">
                <button type="submit" class="bg-indigo-800 text-white p-2">Save</button>
            </div>
          </form>
        </div>
      </div>
    </Layout>
  </div>
</template>
<script>
import { ref, reactive } from 'vue';
import Layout from '@/Layouts/Authenticated';
import { Inertia } from '@inertiajs/inertia';

export default{
    components:{
        Layout,
    },

    props:{
      errors:Object,  
    },
    setup(props, context){

        const form = reactive({
            id:null,
            description:null,
            stock_category_id:"10275",
            uom:"BAG",
            barcode:null,
            discontinued:"Y",
        });

        const submit = () => {
            Inertia.post(route("stock.store"), form, {
              onSuccess: () => {
                    // Handle success event
                    form.id = null;
                    form.description = null;
                    form.stock_category_id = "10275";
                    form.uom = "BAG";
                    form.barcode = null;
                    form.discontinued = null;
                    //   this.reset();
                },
            });
        };
        return{
            form,
            submit,
        };
    },

}
</script>