<template>
  <div class="container" style="width: 100%">
    <div class="container" id="mainContain">
      <div class="container" id="header">
        <h2>BEEBOP</h2>
        <p><i>Password Generator</i></p>
      </div>
      <div class="checkContainer">
        <div class="form-check">
          <input
            @click="checkLower"
            class="form-check-input"
            type="checkbox"
            value=""
            id="lowercase"
          />
          <label class="form-check-label" for="lowercase"> Lowercase </label>
        </div>

        <div class="form-check">
          <input
            @click="checkUpper"
            class="form-check-input"
            type="checkbox"
            value=""
            id="uppercase"
          />
          <label class="form-check-label" for="uppercase"> Uppercase </label>
        </div>

        <div class="form-check">
          <input
            @click="checkNumber"
            class="form-check-input"
            type="checkbox"
            value=""
            id="numbers"
          />
          <label class="form-check-label" for="numbers"> Numbers </label>
        </div>

        <div class="form-check">
          <input
            @click="checkSpecial"
            class="form-check-input"
            type="checkbox"
            value=""
            id="special"
          />
          <label class="form-check-label" for="special"> Special </label>
        </div>
        <div class="form-check">
          <input
            @click="checkEncrypted"
            class="form-check-input"
            type="checkbox"
            value=""
            id="encrypted"
          />
          <label class="form-check-label" for="encrypted">
            SHA256 Encryption
          </label>
        </div>
        <div>
          <input
            ref="input"
            type="text"
            style="margin: 10px auto"
            id="length"
            class="form-control col-12"
            placeholder="Password Length"
            aria-label="Username"
            aria-describedby="basic-addon1"
          />
          <p style="font-size: 12px; text-align: center">
            <i>Password length must be between 5 and 999 characters.</i>
          </p>
        </div>
        <div class="btnDiv">
          <button @click="generatePassword" id="generate" class="btn">
            Generate
          </button>
        </div>
        <div class="form-group">
          <label for="exampleFormControlTextarea1"></label>
          <textarea class="col-12 form-control hidden" id="textarea"></textarea>
          <button class="btn copy hidden" id="generate">
            Copy to clipboard
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PasswordGenerator",
  props: {
    msg: String,
  },

  data() {
    return {
      uppercaseClicked: false,
      lowercaseClicked: false,
      numberClicked: false,
      specialClicked: false,
      encryptedClicked: false,
      message: "",
      uppercaseChar: "QWERTYUIOPASDFGHJKLZXCVBNM",
      lowercaseChar: "qwertyuiopasdfghjklzxcvbnm",
      numberChar: "1234567890",
      specialChar: "!@#$%^&*()_+-=~`{}[]:;'<>?,./",
      passwordArr: [],
    };
  },

  methods: {
    checkLower: function () {
      if (this.lowercaseClicked === false) {
        this.lowercaseClicked = true;
      } else if (this.lowercaseClicked !== false) {
        this.lowercaseClicked = false;
      }
    },
    checkUpper: function () {
      if (this.uppercaseClicked === false) {
        this.uppercaseClicked = true;
      } else if (this.uppercaseClicked !== false) {
        this.uppercaseClicked = false;
      }
    },
    checkNumber: function () {
      if (this.numberClicked === false) {
        this.numberClicked = true;
      } else if (this.numberClicked !== false) {
        this.numberClicked = false;
      }
    },
    checkSpecial: function () {
      if (this.specialClicked === false) {
        this.specialClicked = true;
      } else if (this.specialClicked !== false) {
        this.specialClicked = false;
      }
    },
    checkEncrypted: function () {
      if (this.encryptedClicked === false) {
        this.encryptedClicked = true;
      } else if (this.encryptedClicked !== false) {
        this.encryptedClicked = false;
      }
    },

    generatePassword: function () {
      this.passwordArr = [];
      console.log("yeet");
      let length = this.$refs.input.value;
      if (
        length < 5 ||
        length > 999 ||
        (!this.uppercaseClicked &&
          !this.lowercaseClicked &&
          !this.numberClicked &&
          !this.specialClicked)
      ) {
        alert(
          "Password length must be between 5 and 999 characters. Must have at least one character type selected."
        );
      } else {
        let passwordArr = [];

        let shuffledArr = [];
        let finalPass;
        let randomIndex;

        for (let i = 0; passwordArr.length < length; i++) {
          let checkLength = passwordArr.length < length;

          if (this.lowercaseClicked && checkLength) {
            randomIndex = Math.floor(Math.random() * this.lowercaseChar.length);
            passwordArr.push(this.lowercaseChar[randomIndex]);
          }
          if (this.uppercaseClicked && checkLength) {
            randomIndex = Math.floor(Math.random() * this.uppercaseChar.length);
            passwordArr.push(this.uppercaseChar[randomIndex]);
          }
          if (this.numberClicked && checkLength) {
            randomIndex = Math.floor(Math.random() * this.numberChar.length);
            passwordArr.push(this.numberChar[randomIndex]);
          }
          if (this.specialClicked && checkLength) {
            randomIndex = Math.floor(Math.random() * this.specialChar.length);
            passwordArr.push(this.specialChar[randomIndex]);
          }

          shuffledArr = passwordArr.sort(() => Math.random() - 0.5);
        }
        finalPass = shuffledArr.join("");
        console.log("FINA:", finalPass);
        return finalPass;
      }
    },
  },
};
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

body {
  background-color: #736d964d;
  /* background-image: url("https://images.wallpaperscraft.com/image/spots_background_light_blur_68629_1920x1080.jpg");
  background-repeat: none;
  background-size: cover; */
  font-family: "Open Sans", sans-serif;
  padding: 0 5px;
}

#header {
  width: 80%;
  max-width: 500px;
  text-align: center;
  border-radius: 20px;
  padding: 10px;
  margin: 20px auto;
  font-family: Arial, Helvetica, sans-serif;
  border: 1px solid rgba(255, 255, 255, 0.116);
}

#generate {
  margin: 10px auto;
  border-radius: 20px;
  box-shadow: 5px 5px 10px rgba(151, 151, 151, 0.322);
  box-shadow: 12.61px 12.61px 40px #747474, -12.61px -12.61px 40px #ffffff;
}

.form-control:focus {
  border-color: #ffffff;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(195, 0, 255, 0.233);
}

#mainContain {
  background-color: rgb(248, 248, 248);
  height: 50vh;
  min-height: 650px;
  width: 100%;
  margin: 25px auto;
  border-radius: 10px;
  padding: 19px;
  background: linear-gradient(175deg, #ffffff, #736d964d);
  border-radius: 50px;
  box-shadow: 12.61px 12.61px 40px #9e9e9e, -12.61px -12.61px 40px #ffffff;
}

.btn:hover {
  background-color: #313131;
  color: white;
  transition: 0.4s;
  /* box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.411) !important; */
  box-shadow: 3px 3px 20px #636363, -3px -3px 20px #ffffff !important;
}

h2 {
  color: #313131;
  font-family: "Open Sans", sans-serif;
  text-shadow: 1px 1px 0 rgb(119, 39, 129), 2px 2px 5px rgb(90, 90, 90);
  font-family: Arial, Helvetica, sans-serif;
}

.btnDiv {
  width: 100%;
  background-color: rgba(0, 0, 0, 0);
  display: flex;
  justify-content: center;
}

.checkContainer {
  margin: 0 auto;
  width: 200px;
  padding: 10px;
  width: 80%;
  max-width: 300px;
}

input,
textarea {
  box-shadow: 0px 0px 12px rgba(0, 0, 0, 0.226) inset;
  border-radius: 10px;
  resize: none;
}

textarea {
  text-align: center;
  width: 100%;
  margin: 0 auto;
}

.copy {
  margin: 10px auto;
  width: 100%;
  border-radius: 20px;
  box-shadow: 5px 5px 10px rgba(151, 151, 151, 0.322);
}

#mainContain {
  position: relative;
}

/* #mainContain:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border-radius: 10px;
  background: linear-gradient(120deg, #ffffff, #9dceff, #ffc3ff);
  background-size: 200% 200%;
  clip-path: polygon(
    0% 100%,
    10px 100%,
    10px 10px,
    calc(100% - 10px) 10px,
    calc(100% - 10px) calc(100% - 10px),
    10px calc(100% - 10px),
    10px 100%,
    100% 100%,
    100% 0%,
    0% 0%
  );
}

#mainContain:after {
  animation: frame-enter 1s forwards ease-in-out reverse,
    gradient-animation 4s ease-in-out infinite;
}

/* motion */
@keyframes gradient-animation {
  0% {
    background-position: 15% 0%;
  }
  50% {
    background-position: 85% 100%;
  }
  100% {
    background-position: 15% 0%;
  }
}

.hidden {
  display: none;
}

::selection {
  color: rgb(255, 255, 255);
  background: rgb(0, 0, 0);
}
</style>
