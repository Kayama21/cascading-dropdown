<template>
  <div class="container" >
            <div class="row">
                <div class="col-md-6 col-md-offset-3">
                    <h1>FORM</h1><br>
                    <form role="form" id="reused_form">
                        <div class="row">
                            <div class="col-sm-6 form-group">
                                <label for="name"> Nama Depan:</label>
                                <input type="text" class="form-control" id="firstname" name="firstname" required maxlength="50">
                            </div>
                            <div class="col-sm-6 form-group">
                                <label for="name"> Nama Belakang:</label>
                                <input type="text" class="form-control" id="lastname" name="lastname" required maxlength="50">
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-sm-6 form-group">
                                <label for="email"> Email:</label>
                                <input type="text" class="form-control" id="email" name="email" required maxlength="50">
                            </div>
                            <div class="col-sm-6 form-group">
                                <label for="email"> Phone:</label>
                                <input type="tel" class="form-control" id="phone" name="phone" required maxlength="50">
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-sm-9 form-group">
                                <label for="email"> Alamat:</label>
                                <input type="text" class="form-control" name="address" required maxlength="50">
                            </div>
                            <div class="col-sm-3 form-group">
                                <label for="email"> Kode Pos:</label>
                                <input type="tel" class="form-control" name="postalcode" required maxlength="50">
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-sm-4 form-group">
                                <label for="email"> Kontinen\Benua:</label>
                                <select v-model="selectedContinent">
                                    <option value="">Pilih Kontinen</option>
                                    <option v-for="(country_obj, country) in places" v-bind:key="country">{{country}}</option>
                                </select>
                            </div>
                            <div class="col-sm-4 form-group">
                                <label for="email"> Negara:</label><br>
                                <select :disabled="countries.length == 0" v-model="selectedCountry">
                                    <option value="">Pilih Negara</option>
                                    <option v-for="(city_obj, city) in countries" v-bind:key="city">{{city}}</option>
                                </select>
                            </div>
                            <div class="col-sm-4 form-group">
                                <label for="email"> Kota:</label><br>
                                <select :disabled="cities.length == 0" v-model="selectedCity">
                                    <option value="">Pilih Kota</option>
                                    <option v-for="city in cities" v-bind:key="city" id="dropdown">{{city}}</option>
                                </select>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-sm-12 form-group">
                                <button type="submit" class="btn btn-lg btn-success btn-block" id="btnContactUs">Enter </button>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
</template>

<script>
export default {
  data: function () {
    return {
      places: {
        Asia: {
          China: ['Beijing', 'Shanghai', 'Guangzhou', 'Tianjin'],
          India: ['New Delhi', 'Mumbai', 'Bangalore', 'Chennai'],
          Japan: ['Tokyo', 'Kyoto', 'Nagoya', 'Hiroshima'],
          Indonesia: ['Surabaya', 'Malang', 'Jakarta', 'Balikpapan', 'Bandung'],
          Malaysia: ['Kuala Lumpur', 'Johor Bahru', 'George Town', 'Kota Kinabalu']
        },
        Europe: {
          Germany: ['Berlin', 'Hamburg', 'Munich', 'Cologne', 'Frankfurt', 'Stuttgart'],
          UK: ['London', 'Birmingham', 'Liverpool', 'Bristol'],
          France: ['Paris', 'Marseille', 'Bordeaux', 'Toulouse']
        },
        Australia: {
          Australia: ['Sidney', 'Melbourne', 'Brisbane', 'Adelaide', 'Hobart'],
          'New Zealand': ['Christchurch', 'Wellington', 'Nelson', 'New Plymouth']
        }
      },
      countries: [],
      cities: [],
      selectedContinent: '',
      selectedCountry: '',
      selectedCity: ''
    }
  },
  watch: {
    selectedContinent: function () {
      // Clear previously selected values
      this.countries = []
      this.cities = []
      this.selectedCountry = ''
      this.selectedCity = ''
      // Populate list of countries in the second dropdown
      if (this.selectedContinent.length > 0) {
        this.countries = this.places[this.selectedContinent]
      }
    },
    selectedCountry: function () {
      // Clear previously selected values
      this.cities = []
      this.selectedCity = ''
      // Now we have a continent and country. Populate list of cities in the third dropdown
      if (this.selectedCountry.length > 0) {
        this.cities = this.places[this.selectedContinent][this.selectedCountry]
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
