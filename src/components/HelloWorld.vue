<template>
  <div class="container">
    <br>
    <div class="col-md-12 row">
        <b-carousel id="carousel1"
                  style="text-shadow: 1px 1px 2px #333;"
                  controls
                  indicators
                  background="#ababab"
                  :interval="4000"
                  img-width="1024"
                  img-height="480"
                  v-model="slide"
                  @sliding-start="onSlideStart"
                  @sliding-end="onSlideEnd"
      >

      <!-- Text slides with image -->
      <b-carousel-slide
                        img-src="https://drive.google.com/uc?export=download&id=1eK41gDEVBLZGyjnCsmfST1NG5M5MrL6K">
                      <h1>Tugas Besar Machine Learning</h1>
      </b-carousel-slide>
      <b-carousel-slide img-src="https://drive.google.com/uc?export=download&id=1JD2UY6MBFL3C76pvwA3qKLYIN-s6H3ca">
                      <h1>Universitas Atma Jaya Yogyakarta</h1>
      </b-carousel-slide>
      <b-carousel-slide img-src="https://drive.google.com/uc?export=download&id=12vM0xmpj4giHDt0br8mG5B2gop0ZMXlt">
                      <h1>Semester Genap 2017-2018</h1>
      </b-carousel-slide>
      <b-carousel-slide img-src="https://drive.google.com/uc?export=download&id=1OP4k71RixTWejUIekgyllCYYtIdgsLz1">
                      <h1>Klasifikasi Hewan Menggunakan Random Forest</h1>
      </b-carousel-slide>
      <b-carousel-slide img-src="https://drive.google.com/uc?export=download&id=1d1MruUlWcokrcJLWh_EK6QSWkIIxSmFf">
                      <h1>Universitas Atma Jaya Yogyakarta</h1>
      </b-carousel-slide>

    </b-carousel> 
    </div>
    <br>
    <div class="col-md-12 row">
      <b-card title="Masukkan Data Hewan" class="col-md-12">
        <br>
        <div class="row">
            <form class="col-md-6 row">
              <div class="col-md-8"><p>Hewan Ini Hidup di Air?</p></div>
              <div class="col-md-2">
                <b-form-group>
                <b-form-radio-group id="btnradios2"
                        buttons
                        button-variant="outline-info"
                        size="md"
                        v-model="data.aquatic"
                        :options="yesOrNo"
                        name="radioBtnOutline" />
                </b-form-group>
              </div>
              </form>
              <form class="col-md-6 row">
              <div class="col-md-8"><p>Hewan Ini Bertulang Belakang?</p></div>
              <div class="col-md-2">
                <b-form-group>
                <b-form-radio-group id="btnradios2"
                        buttons
                        button-variant="outline-info"
                        size="md"
                        v-model="data.backbone"
                        :options="yesOrNo"
                        name="radioBtnOutline" />
                </b-form-group>
              </div>
              </form>
            </div>
            <div class="row">
            <form class="col-md-6 row">
              <div class="col-md-8"><p>Hewan Ini Bernafas?</p></div>
              <div class="col-md-2">
                <b-form-group>
                <b-form-radio-group id="btnradios2"
                        buttons
                        button-variant="outline-info"
                        size="md"
                        v-model="data.breathes"
                        :options="yesOrNo"
                        name="radioBtnOutline" />
                </b-form-group>
              </div>
              </form>
              <form class="col-md-6 row">
              <div class="col-md-8"><p>Hewan Ini Bergigi?</p></div>
              <div class="col-md-2">
                <b-form-group>
                <b-form-radio-group id="btnradios2"
                        buttons
                        button-variant="outline-info"
                        size="md"
                        v-model="data.toothed"
                        :options="yesOrNo"
                        name="radioBtnOutline" />
                </b-form-group>
              </div>
              </form>
            </div>
            <div class="row">
              <form class="col-md-6 row">
              <div class="col-md-8"><p>Jumlah Kaki Hewan Ini?</p></div>
              <div class="col-md-2">
                        <!-- <input v-model="legs" type="number" min="0" class="form-control"
                                > -->
                  <b-form-select v-model="data.legs" :options="numbers" class="mb-3" />
              </div>
              </form>
              <div class="col-md-6 row">
                  <div class="col-md-3">
                    <b-button variant="warning" @click="resetData()">Reset Nilai</b-button>
                  </div>
                  <div class="col-md-3">
                    <b-button variant="primary" @click="klasifikasi()">Prediksi</b-button>
                  </div>
                </div>
              </form>
            </div>
      </b-card>
    </div>
    <br>
    <div>
      <div class="col-md-12 row">
        <b-card title="Hasil Prediksi" class="col-md-12">
          <p v-if="response=='0'">Tidak Ada Hasil Prediksi</p>
          <div v-else>
            <p >Hewan Ini Tergolong Kelas : {{response.message}}</p>
            <p>Hewan Kelompok {{response.message}} dalam DataSet Ini Adalah : </p>
            <div class="col-md-12 row">
              <p v-if="response.message=='Mammal'" v-for="mam in mammal" :key="mam" class="col-md-2">b{{mam}}</p>
              <p v-if="response.message=='Bird'" v-for="mam in bird" :key="mam" class="col-md-2">b{{mam}}</p>
              <p v-if="response.message=='Reptile'" v-for="mam in reptile" :key="mam" class="col-md-2">b{{mam}}</p>
              <p v-if="response.message=='Fish'" v-for="mam in fish" :key="mam" class="col-md-2">b{{mam}}</p>
              <p v-if="response.message=='Amphibian'" v-for="mam in amphibian" :key="mam" class="col-md-2">b{{mam}}</p>
              <p v-if="response.message=='Bug'" v-for="mam in bug" :key="mam" class="col-md-2">b{{mam}}</p>
              <p v-if="response.message=='Invertebrate'" v-for="mam in invertebrate" :key="mam" class="col-md-2">b{{mam}}</p>
              
            </div>
          </div>
        </b-card>
      </div>
    </div>
    <br>
    <div>
      <div class="col-md-12 row">
        <b-card title="Tentang Kami" class="col-md-12">
          <br>
          <div class="col-md-12 row">
            <div class="col-md-2"></div>
            <div class="col-md-6 row">
              <div class="col-md-5 row">
              <b-img src="https://drive.google.com/uc?export=download&id=17j6XyBnLRs3TWYQM-mYKDbXZcBrD1KG7" height="150px"></b-img>
              </div>
              <div class="col-md-6">
                <div class="col-md-12 row">
                </div>
                <br>
                <h6>Komang Arinanda</h6>
                <h6>NPM : 150708161</h6>
              </div>
            </div>
            <div class="col-md-4"></div>
          </div>
          <!-- orang2 -->
          <div class="col-md-12 row">
            <div class="col-md-6">
            </div>
            <div class="col-md-6 row">
              <div class="col-md-2"></div>
              <div class="col-md-5 row">
              <b-img src="https://drive.google.com/uc?export=download&id=1qUZhbBQRreRPpqaCD84wTODgexs4OUQp" height="150px"></b-img>
              </div>
              <div class="col-md-5">
                <div class="col-md-12 row">
                </div>
                <br>
                <h6>Calvin Tandra</h6>
                <h6>NPM : 140707799</h6>
              </div>
            </div>
          </div>
          <div class="col-md-12 row">
            <div class="col-md-2"></div>
            <div class="col-md-6 row">
              <div class="col-md-5 row">
              <b-img src="https://drive.google.com/uc?export=download&id=1IZR0uFXO_JWWlm-Dy9QJbS4NHzB_rVii" height="150px"></b-img>
              </div>
              <div class="col-md-6">
                <div class="col-md-12 row">
                </div>
                <br>
                <h6>Elmo Sembada Sarwono</h6>
                <h6>NPM : 140707812</h6>
              </div>
            </div>
            <div class="col-md-4"></div>
          </div>
           <!-- orang2 -->
          <div class="col-md-12 row">
            <div class="col-md-6">
            </div>
            <div class="col-md-6 row">
              <div class="col-md-2"></div>
              <div class="col-md-5 row">
              <b-img rounded blank width="150" height="150" blank-color="#777" alt="img" class="m-1" />
              </div>
              <div class="col-md-5">
                <div class="col-md-12 row">
                </div>
                <br>
                <h6>Antonius Felix Kinarto</h6>
                <h6>NPM : 140707859</h6>
              </div>
            </div>
          </div>
          <div class="col-md-12 row">
            <div class="col-md-2"></div>
            <div class="col-md-6 row">
              <div class="col-md-5 row">
              <b-img src="https://drive.google.com/uc?export=download&id=1peSaLI7JP-DefgNk0APfqAlRn5SmdDCc" height="150px"></b-img>
              </div>
              <div class="col-md-6">
                <div class="col-md-12 row">
                </div>
                <br>
                <h6>Henrica Dea Zevihadeta</h6>
                <h6>NPM : 150708421</h6>
              </div>
            </div>
            <div class="col-md-4"></div>
          </div>
          
        
        </b-card>
      </div>
    </div>
    <br>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      slide: 0,
      sliding: null,
      data : {
        aquatic: 1,
        backbone: 1,
        breathes: 1,
        legs: 0,
        toothed: 1,
      },
      eggs: 1,
      feathers: 1,
      fins: 1,
      milk: 1,
      tail: 1,
      yesOrNo: [
        { text: 'Ya', value: '1' },
        { text: 'Tidak', value: '0' }
      ],
      numbers: [
        { text: '0', value: '0' },
        { text: '2', value: '2' },
        { text: '4', value: '4' },
        { text: '6', value: '6' },
        { text: '8', value: '8' }
      ],
      mammal: [
        'aardvark', 'antelope', 'bear', 'boar', 'buffalo', 'calf', 'cavy', 'cheetah', 'deer',
        'dolphin', 'elephant', 'fruitbat', 'giraffe', 'girl', 'goat', 'gorilla', 'hamster', 'hare',
        'leopard', 'lion', 'lynx', 'mink', 'mole', 'mongoose', 'opossum', 'oryx', 'platypus', 'polecat',
        'pony', 'porpoise', 'puma', 'pussycat', 'raccoon', 'reindeer', 'seal', 'sealion', 'squirrel', 'vampire',
        'vole', 'wallaby', 'wolf'
      ],
      bird: [
        'chicken','crow','dove','duck','flamingo','gull','hawk','kiwi','lark','ostrich','parakeet','penguin','pheasant','rhea','skimmer','skua','sparrow','swan','vulture','wren'
      ],
      reptile: [
        'pitviper', 'seasnake', 'slowworm', 'tortoise', 'tuatara'
      ],
      fish: [
        'bass', 'carp', 'catfish', 'chub', 'dogfish', 'haddock', 'herring', 'pike', 'piranha', 'seahorse', 'sole', 'stingray', 'tuna'
      ],
      amphibian: [
        'frog', 'newt', 'toad'
      ],
      bug: [
        'flea', 'gnat', 'honeybee', 'housefly', 'ladybird', 'moth', 'termite', 'wasp'
      ],
      invertebrate: [
        'clam', 'crab', 'crayfish', 'lobster', 'octopus', 'scorpion', 'seawasp', 'slug', 'starfish', 'worm'
      ],
      response: '0'
    }
  },
  methods: {
    onSlideStart (slide) {
      this.sliding = true
    },
    onSlideEnd (slide) {
      this.sliding = false
    },
    resetData() {
      this.aquatic= 1,
      this.backbone= 1,
      this.breathes= 1,
      this.legs= 0,
      this.toothed= 1
    },
    klasifikasi: function() {
            axios.post('https://mechine-learning-uajy.herokuapp.com/predict/task', this.data)
              .then(response => {
                this.response = response.data
              })
              .catch(error => {
                alert(error)
              })
          }
  }
}
</script>