<template>
  <v-dialog v-model="dialog" persistent max-width="800px">
    <v-card>
    <v-card v-if="step">
      <v-card-text>
        <v-container>
          <div class="row justify-content-md-center">
            <div class="col-md-5">
              <v-img class="firstStep_img" src="@/assets/step_2.jpg"></v-img>
            </div>
            <div class="col-md-7">
              <v-list-item>
                <v-list-item-content class="block1_rightTitle">
                  <v-list-item-title class="block2_rightTitle"
                    >Merhaba...</v-list-item-title
                  >
                  Mağazanızı oluşturmak için alış ve satış kaynaklarınızı
                  seçebilirsiniz.
                </v-list-item-content>
              </v-list-item>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>Kaynak Mağaza</v-list-item-title>
                  <v-autocomplete
                    v-model="selectedMarketplace"
                    required
                    :items="marketplaces"
                    :error-messages="marketplaceErrors"
                    @input="$v.selectedMarketplace.$touch()"
                    @blur="$v.selectedMarketplace.$touch()"
                    item-text="name"
                    item-value="id"
                  ></v-autocomplete>
                </v-list-item-content>
              </v-list-item>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title>Hedef Mağaza</v-list-item-title>
                  <v-autocomplete
                    v-model="selectedMarketplace2"
                    :items="marketplaces"
                    required
                    :error-messages="marketplace2Errors"
                    @input="$v.selectedMarketplace2.$touch()"
                    @blur="$v.selectedMarketplace2.$touch()"
                    item-text="name"
                    item-value="id"
                  ></v-autocomplete>
                </v-list-item-content>
              </v-list-item>
            </div>
          </div>
        </v-container>
      </v-card-text>
    </v-card>
    <v-card v-if="step2">
      <v-card-text>
        <v-container>
          <div class="row justify-content-md-center">
            <div class="col-md-12">
              <v-tabs class="verticalTabs" vertical>
                <v-tab>
                  <v-icon left> mdi-cogs </v-icon>
                  Temel Ayarlar
                </v-tab>
                <v-tab>
                  <v-icon left> mdi-tune </v-icon>
                  Gelişmiş
                </v-tab>
                <v-tab>
                  <v-icon left> mdi-cog-outline </v-icon>
                  Ultra
                </v-tab>

                <v-tab-item>
                  <v-card flat>
                    <v-card-text>
                      <p>
                        <v-img
                          class="secondStep_img"
                          src="@/assets/step_3.jpg"
                        ></v-img>
                      </p>
                      <p class="header_title">
                        Genel Tedarikçi Ayarları<v-icon left>
                          mdi-information
                        </v-icon>
                      </p>
                      <hr />

                      <div class="input-group taxAgeraveDiv mb-4">
                        <span class="taxAverageSpan w-100"
                          >Ekstra Vergi Ortalaması<v-icon left>
                            mdi-information
                          </v-icon></span
                        >
                        <div>
                          <label>Ekstra Vergi Ortalaması</label>
                          <v-text-field class="taxAverageInput" v-model="taxAverageText" solo prepend-icon="mdi-percent" required
                              :error-messages="taxAverageErrors" @input="$v.taxAverageText.$touch()" 
                              @blur="$v.taxAverageText.$touch()"></v-text-field>
                        </div>
                      </div>

                      <hr class="separator" />

                      <p class="mb-0 lastPharaghrapForStep2">
                        <v-checkbox
                          class="cbx"
                          v-model="checkbox"
                          label="İndirimli fiyatı kullan."
                        ></v-checkbox>
                      </p>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
                <v-tab-item>
                  <v-card flat>
                    <v-card-text>
                      <p>
                        <v-img
                          class="secondStep_img"
                          src="@/assets/step_2.jpg"
                        ></v-img>
                      </p>
                      <p class="header_title">
                        Genel Mağaza Ayarları<v-icon left>
                          mdi-information
                        </v-icon>
                      </p>
                      <hr />

                      <div class="input-group taxAgeraveDiv mb-4">
                        <span class="taxAverageSpan w-100"
                          >Ülke Döviz Kuru (1 USD)<v-icon left>
                            mdi-information
                          </v-icon></span
                        >
                        <label>Ülke Döviz Kuru (1 USD)</label>
                        <div class="mainDiv col-lg-12">
                          <div class="leftDiv col-lg-5">
                            <v-text-field class="currencyTextbox" v-model="currencyInputForCountry" solo prepend-icon="mdi-currency-usd" 
                              :readonly="checkbox2" required
                              :error-messages="currencyInputCountryErrors" @input="$v.currencyInputForCountry.$touch()" 
                              @blur="$v.currencyInputForCountry.$touch()"></v-text-field>
                          </div>
                          <div class="mainDiv col-lg-2">
                            <span>veya</span>
                          </div>
                          <div class="rightDiv col-lg-5">
                            <v-checkbox
                              class="cbx"
                              v-model="checkbox2"
                              label="Otomatik"
                            ></v-checkbox>
                          </div>
                        </div>
                      </div>

                      <hr />

                      <div class="input-group taxAgeraveDiv mb-4">
                        <span class="taxAverageSpan w-100"
                          >Minimum Kâr Oranı veya Tutarı<v-icon left>
                            mdi-information
                          </v-icon></span
                        >
                        <label>Minimum kâr oranı veya tutarı</label>
                        <div>
                          <div class="mainDiv col-lg-12">
                            <div class="leftDiv col-lg-5">
                              <v-text-field class="percentTextbox" v-model="percentInputText" solo prepend-icon="mdi-percent" required
                              :error-messages="percentInputErrors" @input="$v.percentInputText.$touch()" 
                              @blur="$v.percentInputText.$touch()"></v-text-field>
                            </div>
                            <div class="mainDiv col-lg-2">
                              <span class="orSpan2">ve</span>
                            </div>
                            <div class="rightDiv col-lg-5">
                              <v-text-field class="currencyTextbox2" v-model="currencyInputText" solo prepend-icon="mdi-currency-usd" required
                              :error-messages="currencyInputErrors" @input="$v.currencyInputText.$touch()" 
                              @blur="$v.currencyInputText.$touch()"></v-text-field>
                            </div>
                          </div>
                        </div>
                      </div>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
                <v-tab-item>
                  <v-card flat>
                    <v-card-text>
                      <p>
                        Fusce a quam. Phasellus nec sem in justo pellentesque
                        facilisis. Nam eget dui. Proin viverra, ligula sit amet
                        ultrices semper, ligula arcu tristique sapien, a
                        accumsan nisi mauris ac eros. In dui magna, posuere
                        eget, vestibulum et, tempor auctor, justo.
                      </p>

                      <p class="mb-0">
                        Cras sagittis. Phasellus nec sem in justo pellentesque
                        facilisis. Proin sapien ipsum, porta a, auctor quis,
                        euismod ut, mi. Donec quam felis, ultricies nec,
                        pellentesque eu, pretium quis, sem. Nam at tortor in
                        tellus interdum sagittis.
                      </p>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
              </v-tabs>
              <v-tabs class="horizontalTabs" horizontal>
                <v-tab>
                  Temel
                </v-tab>
                <v-tab>
                  Gelişmiş
                </v-tab>
                <v-tab>
                  Ultra
                </v-tab>

                <v-tab-item>
                  <v-card flat>
                    <v-card-text>
                      <p>
                        <v-img
                          class="secondStep_img"
                          src="@/assets/step_3.jpg"
                        ></v-img>
                      </p>
                      <p class="header_title">
                        Genel Tedarikçi Ayarları<v-icon left>
                          mdi-information
                        </v-icon>
                      </p>
                      <hr />

                      <div class="input-group taxAgeraveDiv mb-4">
                        <span class="taxAverageSpan w-100"
                          >Ekstra Vergi Ortalaması<v-icon left>
                            mdi-information
                          </v-icon></span
                        >
                        <div>
                          <label>Ekstra Vergi Ortalaması</label>
                          <v-text-field class="taxAverageInput" v-model="taxAverageText" solo prepend-icon="mdi-percent" required
                              :error-messages="taxAverageErrors" @input="$v.taxAverageText.$touch()" 
                              @blur="$v.taxAverageText.$touch()"></v-text-field>
                        </div>
                      </div>

                      <hr class="separator" />

                      <p class="mb-0 lastPharaghrapForStep2">
                        <v-checkbox
                          class="cbx"
                          v-model="checkbox"
                          label="İndirimli fiyatı kullan."
                        ></v-checkbox>
                      </p>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
                <v-tab-item>
                  <v-card flat>
                    <v-card-text>
                      <p>
                        <v-img
                          class="secondStep_img"
                          src="@/assets/step_2.jpg"
                        ></v-img>
                      </p>
                      <p class="header_title">
                        Genel Mağaza Ayarları<v-icon left>
                          mdi-information
                        </v-icon>
                      </p>
                      <hr />

                      <div class="input-group taxAgeraveDiv mb-4">
                        <span class="taxAverageSpan w-100"
                          >Ülke Döviz Kuru (1 USD)<v-icon left>
                            mdi-information
                          </v-icon></span
                        >
                        <label>Ülke Döviz Kuru (1 USD)</label>
                        <div class="mainDiv col-lg-12">
                          <div class="leftDiv col-lg-5">
                            <v-text-field class="currencyTextbox" v-model="currencyInputForCountry" solo prepend-icon="mdi-currency-usd" 
                              :readonly="checkbox2" required
                              :error-messages="currencyInputCountryErrors" @input="$v.currencyInputForCountry.$touch()" 
                              @blur="$v.currencyInputForCountry.$touch()"></v-text-field>
                          </div>
                          <div class="mainDiv col-lg-2">
                            <span class="taxAverageSpan2">veya</span>
                          </div>
                          <div class="rightDiv col-lg-5">
                            <v-checkbox
                              class="cbx"
                              v-model="checkbox2"
                              label="Otomatik"
                            ></v-checkbox>
                          </div>
                        </div>
                      </div>

                      <hr />

                      <div class="input-group taxAgeraveDiv mb-4">
                        <span class="taxAverageSpan w-100"
                          >Minimum Kâr Oranı veya Tutarı<v-icon left>
                            mdi-information
                          </v-icon></span
                        >
                        <label>Minimum kâr oranı veya tutarı</label>
                        <div>
                          <div class="mainDiv col-lg-12">
                            <div class="leftDiv col-lg-5">
                              <v-text-field class="percentTextbox" v-model="percentInputText" solo prepend-icon="mdi-percent" required
                              :error-messages="percentInputErrors" @input="$v.percentInputText.$touch()" 
                              @blur="$v.percentInputText.$touch()"></v-text-field>
                            </div>
                            <div class="mainDiv col-lg-2">
                              <span class="orSpan2">ve</span>
                            </div>
                            <div class="rightDiv col-lg-5">
                              <v-text-field class="currencyTextbox2" v-model="currencyInputText" solo prepend-icon="mdi-currency-usd" required
                              :error-messages="currencyInputErrors" @input="$v.currencyInputText.$touch()" 
                              @blur="$v.currencyInputText.$touch()"></v-text-field>
                            </div>
                          </div>
                        </div>
                      </div>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
                <v-tab-item>
                  <v-card flat>
                    <v-card-text>
                      <p>
                        Fusce a quam. Phasellus nec sem in justo pellentesque
                        facilisis. Nam eget dui. Proin viverra, ligula sit amet
                        ultrices semper, ligula arcu tristique sapien, a
                        accumsan nisi mauris ac eros. In dui magna, posuere
                        eget, vestibulum et, tempor auctor, justo.
                      </p>

                      <p class="mb-0">
                        Cras sagittis. Phasellus nec sem in justo pellentesque
                        facilisis. Proin sapien ipsum, porta a, auctor quis,
                        euismod ut, mi. Donec quam felis, ultricies nec,
                        pellentesque eu, pretium quis, sem. Nam at tortor in
                        tellus interdum sagittis.
                      </p>
                    </v-card-text>
                  </v-card>
                </v-tab-item>
              </v-tabs>
            </div>
          </div>
        </v-container>
      </v-card-text>
    </v-card>
    <v-card v-if="step3">
      <v-card-text>
        <v-container>
          <div class="row justify-content-md-center">
            <div class="col-md-8">
              <v-list-item>
                <v-list-item-content class="block1_3_rightTitle">
                  <v-list-item-title class="block2_3_rightTitle"
                    ><v-img
                      class="lastStep_img"
                      src="@/assets/step_final.jpg"
                    ></v-img
                  ></v-list-item-title>
                </v-list-item-content>
              </v-list-item>

              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title class="step_final_title"
                    >Kurulum Tamamlandı</v-list-item-title
                  >
                  Lorem Ipsum,dizgi ve baskı endüstrisinde kullanılan mıgır
                  metinlerdir.
                </v-list-item-content>
              </v-list-item>

              <v-list-item>
                <v-list-item-content>
                  <v-btn
                    class="finalBtn"
                    color="blue darken-1"
                    text
                    @click.stop="goFirstStep()"
                  >
                    Ana Ekrana Git ->
                  </v-btn>
                  <span class="finalSpan">6 sn. içinde yönlendirileceksiniz.</span>
                </v-list-item-content>
              </v-list-item>
            </div>
          </div>
        </v-container>
      </v-card-text>
    </v-card>
    <v-card-actions v-if="!step3">
      <v-btn
          class="bigLeftBtn"
          color="blue darken-1"
          text
          @click.stop="lastStep()"
          :disabled="step"
        >
          Önceki Adım
        </v-btn>
        <v-btn class="smallLeftBtn mx-2" fab dark color="indigo" @click.stop="lastStep()">
          <v-icon dark>
            mdi-step-backward
          </v-icon>
        </v-btn>
        <v-btn
          class="bigRightBtn"
          color="blue darken-1"
          text
          @click.stop="nextStep()"
        >
          Sonraki Adım
        </v-btn>
        <v-btn class="smallRightBtn mx-2" fab dark color="indigo" @click.stop="nextStep()">
          <v-icon dark>
            mdi-step-forward
          </v-icon>
        </v-btn>
    </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import { validationMixin } from "vuelidate";
import { required } from "vuelidate/lib/validators";
export default {
  mixins: [validationMixin],
  validations() {
    if (this.step) {
      return {
        selectedMarketplace: { required },
        selectedMarketplace2: { required },
      };
    } else if (this.step2) {
      if (!this.checkbox) {
        return {
          percentInputText: { required },
          currencyInputForCountry: { required },
          currencyInputText: { required },
          taxAverageText: { required }
        };
      } else {
        return {
          percentInputText: { required },
          currencyInputText: { required },
          taxAverageText: { required }
        };
      }
    }
  },
  data() {
    return {
      dialog: false,
      step: true,
      step2: false,
      step3: false,
      percentInputText: "",
      currencyInputForCountry: "",
      checkbox: false,
      checkbox2: false,
      currencyInputText: "",
      marketplaces: [
        { id: 1, name: "UAE Marketplace" },
        { id: 2, name: "US Marketplace" },
        { id: 3, name: "FR Marketplace" },
        { id: 4, name: "GB Marketplace" },
      ],
      taxAverageText: "",
      selectedMarketplace: null,
      selectedMarketplace2: null,
    };
  },
  mounted() {
    this.dialog = true;
  },
  computed: {
    marketplaceErrors() {
      const errors = [];
      if (!this.$v.selectedMarketplace.$dirty) return errors;
      !this.$v.selectedMarketplace.required &&
        errors.push("Kaynak Mağaza alanı zorunludur.");
      return errors;
    },
    marketplace2Errors() {
      const errors = [];
      if (!this.$v.selectedMarketplace2.$dirty) return errors;
      !this.$v.selectedMarketplace2.required &&
        errors.push("Hedef Mağaza alanı zorunludur.");
      return errors;
    },
    taxAverageErrors() {
      const errors = [];
      if (!this.$v.taxAverageText.$dirty) return errors;
      !this.$v.taxAverageText.required && errors.push("Vergi Ortalaması alanı zorunludur.");
      return errors;
    },
    percentInputErrors() {
      const errors = [];
      if (!this.$v.percentInputText.$dirty) return errors;
      !this.$v.percentInputText.required &&
        errors.push("Minimim Kâr Oranı alanı zorunludur.");
      return errors;
    },
    currencyInputErrors() {
      const errors = [];
      if (!this.$v.currencyInputText.$dirty) return errors;
      !this.$v.currencyInputText.required &&
        errors.push("Minimim Kâr Tutarı alanı zorunludur.");
      return errors;
    },
    currencyInputCountryErrors() {
      const errors = [];
      if (!this.$v.currencyInputForCountry.$dirty) return errors;
      !this.$v.currencyInputForCountry.required &&
        errors.push("Ülke Döviz Kuru alanı zorunludur.");
      return errors;
    },
  },
  methods: {
    lastStep() {
      if (this.step3) {
        this.step2 = true;
        this.step3 = false;
      } else if (this.step2) {
        this.step = true;
        this.step2 = false;
      }
    },
    nextStep() {
      //#region For Step 2

      if (this.step) {
        this.$v.$touch();
        if (!this.$v.$invalid) {
          this.step2 = true;
          this.step = false;
        }
      }

      //#region For Step 3
      else if (this.step2) {
        this.$v.$touch();
        if (!this.$v.$invalid) {
          this.step3 = true;
          this.step2 = false;
          setTimeout(() => {
            this.step = true;
            this.step3 = false;
            this.selectedMarketplace = null;
            this.selectedMarketplace2 = null;
            this.currencyInputForCountry = "";
            this.currencyInputText = "";
            this.percentInputText = "";
            this.taxAverageText = "";
          }, 6000);
        }
      }
    },
    goFirstStep() {
        this.step = true;
        this.step3 = false;
    },
  },
};
</script>
