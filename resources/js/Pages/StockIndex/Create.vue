<template>
  <div>
    <Layout>
      <div class="flex justify-center w-full">
        <div class="bg-white flex flex-col w-1/3 mt-20 p-6">
          <h2 class="text-lg">Stock Form</h2>
          <form id="stock-form" name="stock-form" v-on:submit.prevent="submit">
            <div class="flex flex-col pt-6">
              <label for="id">ID</label>
              <input
                type="text"
                id="id"
                name="id"
                v-model="form.id"
                autocomplete="off"
              />
              <div class="text-red-700 text-sm">
                {{ errors.id }}
              </div>
              {{ form.id }}
            </div>

            <div class="flex flex-col pt-6">
              <label for="description">Description</label>
              <input
                type="text"
                id="description"
                name="description"
                v-model="form.description"
                autocomplete="off"
              />
              <div class="text-red-700 text-sm">
                {{ errors.description }}
              </div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="scid">Stock Category Id</label>
              <select
                name="stock_category_id"
                id="stock_category_id"
                v-model="form.stock_category_id"
              >
                <option value="38001"> 38001</option>
              </select>

              <div class="text-red-700 text-sm">
                {{ errors.stock_category_id }}
              </div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="uom">Uom</label>
              <input type="text" id="uom" name="uom" v-model="form.uom" />
              <div class="text-red-700 text-sm">
                {{ errors.uom }}
              </div>
            </div>

            <div class="flex flex-col pt-6">
              <label for="uom">Barcode</label>
              <input
                type="text"
                id="barcode"
                name="barcode"
                v-model="form.barcode"
              />
              <div class="text-red-700 text-sm">
                {{ errors.barcode }}
              </div>
            </div>

            <!-- <div class="flex flex-col pt-6">
              <label for="discontinued">Discontinued</label>
              <input
                type="text"
                id="discontinued"
                name="discontinued"
                v-model="form.discontinued"
              />
              <div class="text-red-700 text-sm">
                {{ errors.discontinued }}
              </div>
            </div> -->

            <div class="flex flex-col pt-6">
              <span for="discontinued">Discontinued</span>
              <div class="mt-2">
                <label class="inline-flex items-center">
                  <input
                    id="discontinued"
                    type="checkbox"
                    class="form-checkbox"
                    name="yes"
                    v-model="form.discontinued"
                    value="Y"
                  />
                  <span class="ml-2">Yes</span>
                </label>
                <label class="inline-flex items-center ml-6">
                  <input
                    id="discontinued"
                    type="checkbox"
                    class="form-checkbox"
                    name="no"
                    v-model="form.discontinued"
                    value="N"
                  />
                  <span class="ml-2">No</span>
                </label>
              </div>
              <div class="text-red-700 text-sm">{{ errors.discontinued }}</div>
            </div>

            <div class="flex flex-col pt-6">
              <button type="submit" class="bg-indigo-800 text-white p-2">
                Save
              </button>
            </div>
          </form>
        </div>
      </div>
    </Layout>
  </div>
</template>

<script>
import { ref, reactive } from "vue";
import Layout from "@/Layouts/Authenticated";
import { Inertia } from "@inertiajs/inertia";

export default {
  components: {
    Layout,
  },

  props: {
    errors: Object,
  },

  setup(props, context) {
    const form = reactive({
      id: null,
      description: null,
      stock_category_id: null,
      uom: null,
      barcode: null,
      discontinued: "Y",
    });

    const submit = () => {
      Inertia.post(route("stock.store"), form, {
        onSuccess: () => {
          // Handle success event
          form.id = null;
          form.description = null;
          form.stock_category_id = null;
          form.uom = null;
          form.barcode = null;
          form.discontinued = null;
          //   this.reset();
        },
      });
    };

    return {
      form,
      submit,
    };
  },
};
</script>
