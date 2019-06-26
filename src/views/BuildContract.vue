<template>
  <v-container fill-height fluid grid-list-xl>
    <v-layout justify-center wrap>
       Template ID : {{templateID}}
      <v-card-text>
        <h4>Paste your Google Spreadsheet URL...</h4>
        <!-- <p>(<a href="https://docs.google.com/spreadsheets/d/1HFGm_cSH_XeZtxfREusftu-4S1LYZeAVSVjWMmsRHtY/copy" target="_blank">make a copy</a>)</p> -->
        <div class="input-container">
          <div class="data-link-input">
            <!-- <form v-on:submit="validateURL()">
              <input type="text" class="form-control" placeholder="Paste your Google Spreadsheet URL here." v-model="parseURL">
            </form>-->
          </div>
        </div>
      </v-card-text>
      <v-card-text>
        Header Number : {{Template.length}}
        <v-form>
          <v-container grid-list-md>
            <v-layout row wrap>
              <v-flex sm12 md12 v-for="(headindex, i) in Template" :key="i">
                <v-text-field v-model="Template[i].Header" label="Enter A Header: " outline></v-text-field>
                <draggable :v-model="Template[i].Clause" @start="drag=true" @end="drag=false">
                  <v-text-field
                    v-for="(index, k) in Template[i].clauseCount"
                    :key="k"
                    v-model="Template[i].Clause[k]"
                    label="Enter A Clause for this header"
                    outline
                  ></v-text-field>
                </draggable>
                <v-btn color="primary" @click="Template[i].clauseCount++">Add Clause</v-btn>
              </v-flex>
              <v-btn color="primary" @click="addHeader">Add Header</v-btn>
              <v-btn color="primary" @click="insertData">Create Template</v-btn>
              <v-btn color="primary" @click="onSubmit">Go to page 2</v-btn>
            </v-layout>
          </v-container>
        </v-form>
      </v-card-text>
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";
import draggable from "vuedraggable";
export default {
  name: "Home",
  components: {
    draggable
  },
  data: () => ({
    menu1: false,
    date: "",
    datatype: "Saksham",
    selectedDate: "",
    processing: "False",
    cities: ["bangalore", "pakistan"],
    templateID: "1",
    Template: [{ Header: "", Clause: [], clauseCount: 1 }],
    headerdata: {
      Header: { item_id: "", Header: "" },
      Clause: { item_id: {}, Clause: {} }
    },
    tobeSent: {
      item_id: "",
      Type: "",
      description: ""
    }
  }),
  methods: {
    onSubmit() {
      this.$router.push({ name: "DisplayData" });
      console.log(this.Template);
      // {templete: this.Template, }
    },
    setNewDate() {
      console.log("date", this.selectedDate);
      console.log("newDate", this.date);
    },
    addHeader() {
      this.Template.push({ Header: "", Clause: [], clauseCount: 1 });
      console.log(this.Template);

      // this.Template.item.push({sHeader: '', Clause: []})
    },
    async insertData() {
      // if()
      //use ParseInt()
      // this.headerdata.Header.Header = this.Template.Header;
      // this.headerdata.Header.item_id = "H" + this.HeaderCount;
      // this.headerdata.Clause.Clause = this.Template.Clause;
      // for (var index = 1; index <= this.ClauseCount; index++) {
      //   this.headerdata.Clause.item_id[index] =
      //     "H" + this.HeaderCount + "C" + index;
      // }
      // console.log("headerdata", this.headerdata);

      this.Template.forEach((item, i) => {
        var suthar = {
          item1: i + 1,
          item2: null,
          item3: "header",
          item4: "H" + (i + 1),
          item5: "HH" + (i + 1),
          item6: "HHH" + (i + 1),
          item7: item.Header
        };

        axios.post("http://localhost:3000/legalbase/insert", suthar);

        item.Clause.forEach((x, j) => {
          var gupta = {
            item1: `${i + 1}`,
            item2: null,
            item3: "clause",
            item4: `H${i + 1}-C${j + 1}`,
            item5: `HH${i + 1}-C${j + 1}`,
            item6: `HHH${i + 1}-C${j + 1}`,
            item7: x
          };

          axios.post("http://localhost:3000/legalbase/insert", gupta);
        });
      });
    }
  },

  computed: {
    templateNo() {
      return this.templateID;
    },
    computedDateFormattedMomentjs() {
      return this.date;
    }
  }
};
</script>
