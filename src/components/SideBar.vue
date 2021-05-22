<template>
  <aside>
    <ul>
      <li><h3>Text Layer</h3></li>
      <li>
        <label for="enterText">Enter Text</label>
        <div class="txt-input">
          <input name="enterText" type="text" /><button @click="addText">
            +
          </button>
        </div>
      </li>
      <li class="d-flex">
        <div class="half-field">
          <label for="fontSize">Font Size</label>
          <input type="number" name="fontSize" />
        </div>
        <div class="half-field">
          <label for="lineHeight">Line Height</label>
          <input type="number" name="lineHeight" />
        </div>
      </li>
      <li>
        <label for="fontFamily">Change Font family</label>
        <select for="fontFamily">
          <option value="volvo">Volvo</option>
          <option value="saab">Saab</option>
          <option value="opel">Opel</option>
          <option value="audi">Audi</option>
        </select>
      </li>
    </ul>
  </aside>
</template>

<script>
export default {
  name: "SideBar",
  methods: {
    addText() {
      console.log("Dodao");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
aside {
  position: absolute;
  display: flex;
  align-items: center;
  width: 300px;
  height: 100%;
  top: 0;
  right: 0;
  background-color: #fff;
  box-shadow: -6px 12px 10px 0px #868686;
}
ul {
  display: flex;
  justify-content: space-evenly;
  flex-direction: column;
  height: 50%;
  padding: 0;
  margin: 0;
  list-style: none;
  color: #0d47a1;
  width: 250px;
  margin: 0 auto;
  text-align: left;
}
.txt-input {
  display: flex;
  justify-content: space-between;
}
.txt-input input {
  width: 80%;
}
button {
  background: #0ad09e;
  border: 0;
  color: white;
}
.d-flex {
  display: flex;
}
.half-field {
  width: 50%;
}
.half-field input {
  width: 80%;
}
input,
label,
select {
  display: block;
}
label {
  margin-bottom: 5px;
}
select {
  width: 100%;
}
</style>
