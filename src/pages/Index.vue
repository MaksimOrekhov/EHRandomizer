<template>
  <div class="wrapper">
    <div class="card-name">{{ randomCard && randomCard.name }}</div>
    <img v-if="randomCard && randomCard.src" class="card-img" :src="randomCard.src">
    <img v-else class="card-img" src="../statics/bg.jpg">
    <select class="card-type-select" v-model="currentCardType" placeholder="Тип карты" @change="resetData">
      <option v-for="type in cardTypes" :value="type.value">{{ type.text }}</option>
    </select>

    <div class="card-spec" v-if="currentCardType === 'items'">
      <div class="form_radio_btn">
        <input type="radio" id="weapon" name="cardSpec" value="weapon" v-model="cardSpec" />
        <label for="weapon">Оружие</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="service" name="cardSpec" value="service" v-model="cardSpec" />
        <label for="service">Услуга</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="ally" name="cardSpec" value="ally" v-model="cardSpec" />
        <label for="ally">Союзник</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="item" name="cardSpec" value="item" v-model="cardSpec" />
        <label for="item">Вещь</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="trinket" name="cardSpec" value="trinket" v-model="cardSpec" />
        <label for="trinket">Безделушка</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="full" name="cardSpec" value="full" v-model="cardSpec" />
        <label for="full">Вся колода</label>
      </div>
    </div>

    <div class="card-spec" v-if="currentCardType === 'artifacts'">
      <div class="form_radio_btn">
        <input type="radio" id="weapon" name="cardSpec" value="weapon" v-model="cardSpec" />
        <label for="weapon">Оружие</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="book" name="cardSpec" value="book" v-model="cardSpec" />
        <label for="book">Книга</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="magic" name="cardSpec" value="magic" v-model="cardSpec" />
        <label for="magic">Волшебная</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="full" name="cardSpec" value="full" v-model="cardSpec" />
        <label for="full">Вся колода</label>
      </div>
    </div>

    <div class="card-spec" v-if="currentCardType === 'spells'">
      <div class="form_radio_btn">
        <input type="radio" id="aura" name="cardSpec" value="aura" v-model="cardSpec" />
        <label for="aura">Аура</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="spell" name="cardSpec" value="spell" v-model="cardSpec" />
        <label for="spell">Чары</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="ritual" name="cardSpec" value="ritual" v-model="cardSpec" />
        <label for="ritual">Ритуал</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="full" name="cardSpec" value="full" v-model="cardSpec" />
        <label for="full">Вся колода</label>
      </div>
    </div>

    <div class="card-spec" v-if="currentCardType === 'conditions'">
      <div class="form_radio_btn">
        <input type="radio" id="madness" name="cardSpec" value="madness" v-model="cardSpec" />
        <label for="madness">Безумие</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="misfortune" name="cardSpec" value="misfortune" v-model="cardSpec" />
        <label for="misfortune">Напасть</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="gift" name="cardSpec" value="gift" v-model="cardSpec" />
        <label for="gift">Дар</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="talent" name="cardSpec" value="talent" v-model="cardSpec" />
        <label for="talent">Талант</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="full" name="cardSpec" value="full" v-model="cardSpec" />
        <label for="full">Вся колода</label>
      </div>
    </div>

    <div class="card-spec" v-if="currentCardType === 'rareItems'">
      <div class="form_radio_btn">
        <input type="radio" id="item" name="cardSpec" value="item" v-model="cardSpec" />
        <label for="item">Вещь</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="rare" name="cardSpec" value="rare" v-model="cardSpec" />
        <label for="rare">Редкая</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="magic" name="cardSpec" value="magic" v-model="cardSpec" />
        <label for="magic">Волшебная</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="weapon" name="cardSpec" value="weapon" v-model="cardSpec" />
        <label for="weapon">Оружие</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="ally" name="cardSpec" value="ally" v-model="cardSpec" />
        <label for="ally">Союзник</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="quest" name="cardSpec" value="quest" v-model="cardSpec" />
        <label for="quest">Задача</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="taro" name="cardSpec" value="taro" v-model="cardSpec" />
        <label for="taro">Таро</label>
      </div>
      <div class="form_radio_btn">
        <input type="radio" id="full" name="cardSpec" value="full" v-model="cardSpec" />
        <label for="full">Вся колода</label>
      </div>
    </div>

    <button :disabled="!cardSpec" class="button" @click="chooseCard">Выбрать карту</button>
  </div>
</template>

<script>
  import { decks } from '../decks.js'

    export default {
        name: 'PageIndex',
        data() {
            return {
                cardTypes: [
                    { text: 'Активы', value: 'items' },
                    { text: 'Артефакты', value: 'artifacts' },
                    { text: 'Заклинания', value: 'spells' },
                    { text: 'Состояния', value: 'conditions' },
                    { text: 'Редкие активы', value: 'rareItems' },
                ],
                currentCardType: 'items',
                cardSpec: null,
                randomCard: null,
                decks: decks
            }
        },
        methods: {
            chooseCard: function() {
                let cardsArr = [];
                this.decks[this.currentCardType].map(deck => {
                    return deck.type.includes(this.cardSpec) && cardsArr.push(deck)
                })
                let res = cardsArr.length ? Math.floor(Math.random() * cardsArr.length) : Math.floor(Math.random() * this.decks[this.currentCardType].length)
                this.randomCard = cardsArr.length ? cardsArr[res] : this.decks[this.currentCardType][res]
            },
            resetData: function() {
                this.randomCard = null;
                this.cardSpec = null;
            }
        }
    }
</script>

<style scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    width: 100%;
    background: url("../statics/cthulhu.jpg") center no-repeat;
    background-size: cover;
    color: #fff;
  }

  .card-name {
    margin-top: 6vh;
    margin-bottom: 3vh;
    font-size: 8vw;
    text-align: center;
    font-weight: bold;
    text-shadow: 3px 3px 1px #000;
    line-height: 35px;
  }

  .card-type-select {
    border: 2px solid #000;
    margin-bottom: 15px;
    width: 60vw;
  }

  .button {
    border: 1px solid #000;
    padding: 20px;
    font-size: 20px;
    font-weight: bold;
    border-radius: 10px;
    background-color: darkolivegreen;
    color: #fff;
  }

  .card-img {
    width: 60vw;
    height: 95vw;
    margin-bottom: 20px;
    border: 5px solid #fff;
    border-radius: 5px;
  }

  .card-spec {
    margin-bottom: 20px;
    width: 100vw;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    justify-content: center;
  }

  .card-spec div {
    display: flex;
    align-items: center;
    font-size: 14px;
    text-shadow: 2px 2px 1px #000;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .card-spec input {
    margin-right: 5px;
  }

  .card-spec label {
    margin-right: 10px;
  }

  .form_radio_btn {
    display: inline-block;
    margin-right: 10px;
  }
  .form_radio_btn input[type=radio] {
    display: none;
  }
  .form_radio_btn label {
    display: inline-block;
    cursor: pointer;
    padding: 0px 10px;
    line-height: 34px;
    border: 1px solid #999;
    border-radius: 6px;
    user-select: none;
    background-color: darkolivegreen;
  }

  /* Checked */
  .form_radio_btn input[type=radio]:checked + label {
    background: darkslategrey;
  }
</style>
