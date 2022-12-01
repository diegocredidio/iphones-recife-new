<template>
  <section class="containerCalc">
    <app-logo />
    <section class="fields">
      <div class="field">
        <div style="margin: 0 10px">
          <label>Valor no cartão</label>
        </div>
        <div class="field has-addons">
          <!-- <p class="control">
            <a class="button is-static is-large">R$</a>
          </p>-->
          <p class="control is-expanded">
            <input v-model="price" onfocus="this.value=''" class="input is-large" placeholder="R$" />
          </p>
        </div>
      </div>
      <!-- <div class="field" style="padding:0 30px;">
        <input
          id="switchExample"
          type="checkbox"
          name="switchExample"
          class="switch"
          v-model="checked"
        />
        <label for="switchExample">Com Entrada</label>
      </div>-->
      <div class="field">
        <div style="margin: 0 10px">
          <label>Quer dar uma Entrada? Digite o valor</label>
        </div>
        <div class="field has-addons">
          <!-- <p class="control">
            <a class="button is-static is-large">R$</a>
          </p>-->
          <p class="control is-expanded">
            <input
              v-model="entrada"
              onfocus="this.value=''"
              class="input is-large"
              placeholder="R$"
            />
          </p>
        </div>
      </div>
    </section>

    <!-- <section class="hero" style="width:100%; margin-top: 30px;">
      <div class="hero-foot">
        <nav class="tabs is-boxed is-fullwidth is-large">
          <div class="container">
            <ul>
              <li class="tab is-active" onclick="openTab(event,'Credito')">
                <a>Crédito</a>
              </li>
              <li class="tab" onclick="openTab(event,'Debito')">
                <a>Débito</a>
              </li>
            </ul>
          </div>
        </nav>
      </div>
    </section>-->
    <div style="width: 100%;">
      <div id="Credito" class="content-tab">
        <!-- <div>
          <div>12x</div>
          <div>R$ 1.999,99</div>
          <div>Total 10.000,00</div>
        </div>-->
        <section style="width: 100%; margin-top: 30px">
          <div class="table-row table-header">
            <div class="table-col col-small"></div>
            <div class="table-col col-big">Valor Total</div>
          </div>
          <div class="table-row table-content">
            <div class="table-col">Débito a vista</div>
            <div class="table-col col-big">
              {{
              ((totalParcelado + adicionalHiper(n)) / (1 - taxa_debito))
              | currency
              }}
            </div>
          </div>
        </section>

        <section v-if="qtd_parcelas > 12" style="margin: 20px 10px 0px; font-weight: bold; color:red">
          Evite perda de tempo! <br>
          Consulte a operadora do seu cartão para parcelamentos acima de 12x 
        </section>

        <section style="width: 100%; margin-top: 30px">
          <div class="table-row table-header">
            <div class="table-col col-small">Crédito</div>
            <div class="table-col col-big">Valor Parcela</div>
            <div class="table-col col-big">Valor Total</div>
          </div>
          <div class="table-row table-content" v-for="n in qtd_parcelas" v-bind:key="n">
            <div class="table-col col-small">{{ n }}x</div>
            <div class="table-col col-big">
              {{
              ((totalParcelado + adicionalHiper(n)) /
              (1 - taxa_parcela[n - 1]) /
              n)
              | currency
              }}
            </div>
            <div class="table-col col-big">
              {{
              ((totalParcelado + adicionalHiper(n)) /
              (1 - taxa_parcela[n - 1]))
              | currency
              }}
            </div>
          </div>
        </section>
      </div>
    </div>
    <div style="width: 100%;">
      <div id="Debito" class="content-tab" style="display: none">
        <section style="width: 100%; margin-top: 30px">
          <div class="table-row table-header">
            <div class="table-col col-big">Total</div>
          </div>
          <div class="table-row table-content">
            <!-- <div class="table-col col-small">{{ n }}x</div> -->
            <div class="table-col col-big">
              {{
              ((totalParcelado + adicionalHiper(n)) / (1 - taxa_debito))
              | currency
              }}
            </div>
          </div>
        </section>
      </div>
    </div>
  </section>
</template>

<script>
import AppLogo from "~/components/AppLogo.vue";
import { VMoney } from "v-money";
// import { mask } from "vue-the-mask";

export default {
  components: {
    AppLogo
  },

  data() {
    return {
      checked: false,
      isInputActive: false,
      price: "",
      entrada: "0",
      //qtd_parcelas: 12,
      qtd_parcelas: 18,
      taxa_debito: 0.0259,
      taxa_credito: 0.04,
      taxa_parcela: [
        0.04,
        0.05,
        0.06,
        0.07,
        0.08,
        0.085,
        0.09,
        0.10,
        0.11,
        0.115,
        0.12,
        0.13,
        0.14,
        0.145,
        0.15,
        0.16,
        0.17,
        0.18
      ],

      money: {
        decimal: ",",
        thousands: ".",
        prefix: "",
        suffix: "",
        precision: 2,
        masked: false
      }
    };
  },

  computed: {
    totalParcelado: function() {
      var valor1 = this.parseValue(this.price);
      var valor2 = this.parseValue(this.entrada);
      var valorTotal = parseFloat(valor1) - parseFloat(valor2);

      return valorTotal;
    }
  },

  methods: {
    parseValue: function(param) {
      var pattern = /R\$|\./gi;

      return param.replace(pattern, "").replace(",", ".");
    },

    adicionalHiper: function(numero) {
      var valorAdicional = 0;

      if (numero < 13 && this.totalParcelado > 0) {
        valorAdicional = 0;
      }

      return valorAdicional;
    }
  },

  directives: {
    money: VMoney,
    // mask
  }
};
</script>

<style>
.containerCalc {
  min-height: 100vh;
  max-width: 800px;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  text-align: center;
  padding-bottom: 30px;
}
.header {
  font-size: 2em;
  margin: 20px 0;
}
.fields {
  display: flex;
  width: 100%;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  text-align: left;
}
.field {
  width: 100%;
  padding: 10px;
}
.table-row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  text-align: center;
  height: 30px;
}
.table-col {
  padding: 10px 0;
  line-height: 3rem;
}
.table-content:nth-child(even) {
  background: #fff;
}
.table-content:nth-child(odd) {
  background: #f7f7f7;
}
.col-small {
  width: 20%;
}
.col-big {
  width: 40%;
}

.table-header {
  font-weight: bold;
  text-transform: uppercase;
  font-size: 10px;
  border-bottom: 1px solid #ccc;
  height: 20px;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
